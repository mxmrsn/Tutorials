# How to Run the Robot
These are the steps for commanding the robot for ex vivo experiments. For robot setup, reference [the robot setup]()

## Streaming Data for Registration
1. In order for the UNC team to register, you need to be streaming data. This occurs in a few different ways.
2. Generally, they will ask you to start streaming data when they need it for registration. It is best practice to descriptively label the log file so that you know what each instance is.
3. For tree snaking someone will deploy the 6 DOF probe through the robot. Before snaking begins, navigate to the launch file and rename the log file to be xxx_presnake1 to run any setup tests. Once you are ready to snake. Coordinate with the team to begin, launch the code so that the data is streaming to the connected devices on the ros network and log the data to the xxx_treesnake1 file (so set that up before), simultaneously someone will start the registration and someone will start snaking the trees. These need to happen at the same time.
  -Snaking the tress is navigating the 6DOF probe through a variety of air ways and collecting those data points to form a unique point cloud.

## Piercing and Aiming
### Piercing
1. At this point there should be 3-5 plans to the goal point. The tools inserted in the robot include the aiming device (wrist) and the piercing stylet.
2. On the computer you should be streaming data to the log file xxx_piercingattempt1.
3. Someone will manually navigate the piercing stylet to the piercing location and push it through the airway. Then the aiming device can be manually threaded over the piercing stylet to hold its place (note that the wrist is a larger, heavier tube and it may deform the airways internally which can lead to registration error)
4. At this point someone can jog the motors until the attachment point is at an appropriate distance for the hardware person to clip the aiming device (wrist) in.
  -You may want to clamp the bronchoscope into its holder and move the robot transmission on the macro scale before jogging the motors.
5. Jog the motor for the AD (wrist) backwards until there is some tension. This is done in the GUI and it is important to make sure that the state machine is not running
6. Kill the code?
7. Swap the stylet for the Needle
  -make a note about aligning the sharpie marks for the 5mm extra needle insertion

## Aiming
8. Restart the code
9. Enable the foot pedal GUI
10. Focus the foot pedal gui and then adjust until the goal point is in the workspace
  -key set1
  -key set 2
  -make a note about enabling vs disabling the foot footpedal
11. Knowing when you're in the workspace
  -red cone means there's an obstruction
  -blue cone means the goal is not in the workspace
  -green cone means no obstructions and the goal is in the workspace
12. At the point we log the start point and run the planner for the final time then move on to steering

## Steering
1. When you are ready to steer, navigate to the launch file and change the notation to XXX_attempt1
2. Once a plan has been found/determined, plan will be sent to the robot when it is in NEEDLE_SETUP
3. The print out in the terminal should print out the trajectory, check the trajectory to make sure that it is a valid plan, and that the start of the trajectory is close to the current needle tip position.
  -**what indicates that the plan is valid?**
4. Enable the motors using the mcb_test gui that correspond to the needle rotation and insertion stages
  -**motor x** corresponds to needle rotation and
  -**motory** corresponds to needle insertion
5. The needle will start steering once you trigger the NEEDLE_STEERING state
6. After the needle steers to the final target, it will stop and print out the error w.r.t. that end point.
7. Usually you will scan the lung + needle for a confirmation of the needle deployment - leave the tracker and robot running, but DISABLE the motors that were enabled when scanning.
8. After scanning, re-enable the motors for the needle stage and toggle the NEEDLE_GOBACK state
9. After the needle stage has returned to its initial position, DISABLE the motors again.
10. DONE.
**add in information about labeling and logging the data and when to flag it**
