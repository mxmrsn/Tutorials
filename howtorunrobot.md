# How to Run the Robot
These are the steps for commanding the robot for ex vivo experiments. For robot setup, reference [the robot setup]()

## Streaming Data for Registration
1. In order for the UNC team to register, you need to be streaming data. This occurs in a few different ways.
2. Generally, they will ask you to start streaming data when they need it for registration. It is best practice to descriptively label the log file so that you know what each instance is.
3. For tree snaking someone will deploy the 6 DOF probe through the robot. Before snaking begins, navigate to the launch file and rename the log file to be xxx_presnake1 to run any setup tests. Once you are ready to snake. Coordinate with the team to begin, launch the code so that the data is streaming to the connected devices on the ros network and log the data to the xxx_treesnake1 file (so set that up before), simultaneously someone will start the registration and someone will start snaking the trees. These need to happen at the same time.
  -Snaking the tress is navigating the 6DOF probe through a variety of air ways and collecting those data points to form a unique point cloud.

## Test Fitting the Tools
Before we insert any of our nesting tools we need to check the fit. Some of this can be done ahead of time by inserting the stylet (0.69mm OD) through the tip of the wrist (i.e. tip to tip). More precise test fitting should happen on site. This involves plugging the tools into the robot. With tension applied to the aiming device, gently insert the steerable needle into the channel with the bevel facing away from the tendon (you can rotate to figure this out, it only smoothly inserts in one orientation). BE VERY GENTLE WHEN DOING THIS. DO NOT PUSH THROUGH IF THERE IS ANY RESISTANCE. Push the steerable needle out until 5mm is exposed from the aiming device tip (measure this with calipers). Then make a sharpie mark on the shaft of the needle where it meets the back end of the wrist tube to denote how far it should be inserted. Note that if you have difficulty inserting either the stylet or the needle it could be due to a blockage such as soft tissue, blood, superglue (particularly from the bushing) or a twisted tendon. You can clear any blockages using an alcohol (isopropyl) rinse with a syringe followed by a water rinse with a syringe, or you can use a number 69 hand drill to mechanically clear the blockage. Note that if you need to totally restring the wrist it is okay to flush with acetone but it will dissolve the acetone that attaches the bushing, compromising an assembled wrist.

## Piercing and Aiming
### Piercing
1. At this point there should be 3-5 plans to the goal point. The tools inserted in the robot include the aiming device (wrist) and the piercing stylet.
2. On the computer you should be streaming data to the log file xxx_piercingattempt1.
3. Someone will manually navigate the piercing stylet to the piercing location and push it through the airway. Then the aiming device can be manually threaded over the piercing stylet to hold its place (note that the wrist is a larger, heavier tube and it may deform the airways internally which can lead to registration error)
  - You can flag this position if you want and label the point (I think by toggling between the AIMING and IDLE states)
4. Kill the Code, Ctrl C in the state machine window
5. At this point someone can jog the motors until the attachment point is at an appropriate distance for the hardware person to clip the aiming device (wrist) in.
  - You may want to clamp the bronchoscope into its holder and move the robot transmission on the macro scale before jogging the motors.
6. Jog the motor for the AD (wrist) backwards until there is some tension. This is done in joint space in the GUI and it is important to make sure that the state machine is not running
7. Swap the stylet for the Needle
  - Align the sharpie mark with the back of the wrist. If the stage needs adjusted, have someone command the stage forward using the GUI.
  - Once the needle is properly aligned in the translation direction, it may need to be rotated. Consult the diagram below to determine how the needle needs to be oriented relative to the tracker.
  **TODO: Insert Efe's diagram with the tracker and needle**

## Aiming
8. Restart the code, in the state machine window type ```roslaunch lung_robot lung_robot_TorsionEKF.launch``` or you can likely use the up arrow to navigate to the code in command history.
9. Command the PUNCTURE state in order to tele operate
10. Focus the foot pedal gui and then adjust until the goal point is in the workspace. To do this you can:
  - Bulk Rotate: Arrow keys left and right rotate wrt a body frame on the needle tip
  - Bulk Translate: Arrow keys up and down bulk translate forward and backward
  - Tension the Aiming Device: Q tensions and W de-tensions
  - If necessary you can also aim the device outside of the puncture state. This includes:
    - Navigating to the dithering state. Command the state machine to **WINDUP_RELEASE_WINDUP** this relieves some force on the tissue by moving the needle back in forth, it may also move the aiming device.
    - If you have rotated the needle away from its necessary alignment with the EM Tracker, go into the IDLE state, kill the code, and use the MCB GUI to rotate the needle (motor 2) back to its aligned position INDEPENDENT OF THE AD.
11. Knowing when you're in the workspace:
  - red cone means there's an bronchial tree obstruction (bad starting pose, you're in the airway)
  - blue cone means the goal is not in the workspace
  - green cone means you have a good start pose and the goal is in the workspace
12. At the point we log the start point and run the planner for the final time then move on to steering

## Steering
1. When you are ready to steer, navigate to the launch file and change the notation to XXX_attempt1
2. Once a plan has been found/determined, plan will be sent to the robot when it is in NEEDLE_SETUP
3. The print out in the terminal should print out the trajectory, check the trajectory to make sure that it is a valid plan, and that the start of the trajectory is close to the current needle tip position.
  - The window will say "Trajectory is good!" and tell you the number of points, speed, etc.
4. Enable the motors using the mcb_test gui that correspond to the needle rotation and insertion stages
  - Motor 2 corresponds to needle rotation and needle insertion in the rotation and translation windows respectively
5. The needle will start steering once you trigger the NEEDLE_STEERING state
6. After the needle steers to the final target, it will stop and print out the error w.r.t. that end point.
7. Usually you will scan the lung + needle for a confirmation of the needle deployment - leave the tracker and robot running, but DISABLE the motors that were enabled when scanning.
8. After scanning, re-enable the motors for the needle stage and toggle the NEEDLE_GOBACK state
9. After the needle stage has returned to its initial position, DISABLE the motors again.
10. DONE.
