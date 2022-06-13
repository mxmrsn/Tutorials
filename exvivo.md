# Setting Up an Ex Vivo Experiment

## Materials List
-
## Plugging Up the Robot and the Sensors
1. Remove the robot transmission from the case and attach it to the Noga arm, using the screw (found in the top of the tool box). You should use the needle nose pliers to place the screw in the inset and then tighten using an allen key. This is best done with two people, one to manage the screw placement and one to hold the robot.
![robotarm](/imgs/exvivo/robotarmsetup.png)
2. Place the electronics box on the bottom of the cart. Ensure that the large black cables (and thusly the transmission) are properly snaked through the middle of the cart towards the table in order to allow for sufficient travel.
![robotconnections](/imgs/exvivo/robotoutputs.png)
3. Setting Up the EM Tracker Equipment
  - Pull the rigid table with the support arm to the side of the scanner table and attach the white field generator box to the movable arm
  - Place the large driver box on the bottom shelf of the cart (behind and to the left of the robot)
  - Place the breakout boxes on the back of the scanner table
  - Connect the breakout boxes (channel 1, to breakout box 1, which is labeled in red sharpie, this box goes on top) then (channel 2, to breakout box 2, black sharpie, this box goes on the bottom)
  - Connect the driver box to the tracker (silver cord on the front of the box)
  - Connect the driver box to the robot
  - Connect the driver box to Power
  - Connections are shown in the figure below:
  ![emtrackerconnections](/imgs/exvivo/emtrackerconnections.png) **TODO: fix boxes**

## Setting Up the Terminator Window
1. Launch Terminator
2. Enable USB Permissions
  - Option 1: Reverse search USB permissions command using ctrl r
  - Option 2: ``` sudo chmod 666 /dev/ttyUSB0 ```
3. Command ``` roslaunch rosserial_server socket.launch ``` to start the ros serial server
    ![successful server launch](/imgs/exvivo/ROSSerialServerSuccess.png)
4. Split the terminator window horizontally once and then vertically twice
5. Command ``` rqt ``` in both windows to launch the visual interfaces for lung 1 and lung 2
  - Usually the plugin is already selected, if it isn't choose Plugins>MEDLAB>MCB Test
  - Also need to launch the footpedal gui at some point to drive the aiming device **TODO: put instructions on file>medlab>...etc**
    ![rqtgui](/imgs/exvivo/RQTGUI.png)
  - Use another rqt command to enable the foot pedal. Go to plugins>MEDLAB>foot pedal.
6. Turn on the power switch to the electronics box
  - check that the board initialize (if the boards flash blue and the amps flash red that is bad)
  - If the lights ARE flashing there is an error and you should consult [MCB_ROS Repository](github.com/medlabprojects/MCB_ROS) to troubleshoot.
7. In the rqt GUI we want to connect to lung1 and lung2 and Enable ROS Control Mode for both.
8. Manually enable and jog each motor for each control board to ensure everything is working. If the control effort is excessive you need to check the connections and try again.
9. In the lung robot package, ``` lung_robot/launch/lung_robot_TorsionEKF.launch ``` change the ``` log_file_name_note ``` value to be the log file name
10. Split the window again and launch the file using ``` roslaunch lung_robot_TorsionEKF.launch ```
  - the tracker box should beep and all of the lights should change from yellow to green
11. Now you should verify that all of the sensors are working
  - Split the window into six vertical windows (one for each sensor)
  - In the first window command ``` rostopic echo aurora_Pose ``` to echo the needle pose (or whatever is plugged into channel 1)
  - In the subsequent windows command to echo the broch_Pose, lf1_Pose, lf2_Pose, lf3_pose and lf4_Pose respectively
  - In another window you can bring up rqt plot if you want to graph any of the topics (although looking at the numerical values for the poses should be sufficient)
12. In order to be able to change the state of the state machine you'll need another Terminator window. You can do that using ``` rosparam set /control_mode IDLE ```
13. This is about the end of the Terminator Window Set-Up. See the picture below for the final look:
    ![TerminatorWindowSet-Up](/imgs/exvivo/TerminatorWindowSetup.png)

## Setting Up the Lungs
1. Ahead of the experiments, the ex vivo lungs need to be cleaned and prepped in labeled ziploc bags (L1, L2, etc.) The mail order lungs require less prep than the farmer's market but they still need to be prepped.
2. Plug up the quick change adapter to the medical air supply in the wall. This should also be connected to silicone tubing and the ET tube.
3. Confirm that the flat patient table is affixed to the CT scanner table.
4. Add absorbent surgical drapes to the scanner end of the table.
5. Wrap the lunch tray in paper towel and add it to the scanner end of the table.
6. Select one of the lungs and remove it from the plastic bag. Let some of the liquid drip of but do not dry out the lung. Place the lung on the lunch tray with the heart up and the trachea facing the ET tube.
7. With the ET balloon collapsed, insert the ET tube into the trachea. Use the syringe to inflate the ET balloon. At this point you can either inflate the lung to check for leaks (be sure to hold the trachea over the ET tube) or ziptie the trachea to the ET tube and then inflate the lung.
![inflatedlung](/imgs/exvivo/inflatedlung.jgp) **TODO:fix picture embed**
8. At this point you can scan the lung for the first time and check for collapse or fissures which may make the lung undesireable. Make sure that the bronchoscope is inserted into the ET tube so that you get a realalistic idea of the lung volume with the leak.
**insert pic here**
9. If the lung is satisfactory you can attach the fiducials. they should already be plugged into the break out box and you can neatly uncoil them towards the end of the table.
10. Apply a layer of superglue (preferably high viscosity) to the underside of the fiducial and place it on the lung.
11. The order of the fiducials matters, make sure you confirm this with the team. The current layout is as follows:
  -lf1 is ventral, proximal, and superior
  -lf2 is ventral, distal, and inferior
  -lf3 is dorsal, proximal, and superior
  -lf4 is dorsal, distal, and superior
  These fiducials form a cubic region in which the robot sensing is best.
![fiducialplacement](/imgs/exvivo/fiducialplacement.png)
12. Once you are happy with the fiducial placement, you can wrap the lung to fix everything to the table.
