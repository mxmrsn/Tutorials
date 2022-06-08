# Setting Up an Ex Vivo Experiment

## Materials List
-
## Plugging Up the Robot and the Sensors
![robotarm](/imgs/exvivo/robotarmsetup.png)

## Setting Up the Terminator Window
1. Launch Terminator
2. Enable USB Permissions
  - Option 1: Reverse search USB permissions command using ctrl r
  - Option 2: ``` sudo chmod 666 /dev/ttyUSB0 ```
3. Command ``` roslaunch rosserial_server socket.launch ``` to start the ros serial server
    ![successful server launch](/imgs/exvivo/ROSSerialServerSuccess)
4. Split the terminator window horizontally once and then vertically once
5. Command ``` rqt ``` in both windows to launch the visual interfaces for lung 1 and lung 2
  - Usually the plugin is already selected, if it isn't choose Plugins>MEDLAB>MCB Test
  - Also need to launch the footpedal gui at some point to drive the aiming device
    ![rqtgui](/imgs/exvivo/RQTGUI)
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
    ![TerminatorWindowSet-Up](/imgs/exvivo/TerminatorWindowSetUp)
