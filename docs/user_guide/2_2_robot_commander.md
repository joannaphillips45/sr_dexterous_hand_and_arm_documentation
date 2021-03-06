## Robot commander

The robot commander provides a high level interface to easily control the different robots supported by Shadow Robot. It encapsulates functionality provided by different ROS packages, especially the moveit_commander, providing access via a simplified interface.

There are three clases available:
* [SrRobotCommander](https://github.com/shadow-robot/sr_interface/blob/melodic-devel/sr_robot_commander/src/sr_robot_commander/sr_robot_commander.py): base class. Documentation can be found in the following [link](https://dexterous-hand.readthedocs.io/en/latest/user_guide/2_software_description.html#srrobotcommander).
* [SrHandCommander](https://github.com/shadow-robot/sr_interface/blob/melodic-devel/sr_robot_commander/src/sr_robot_commander/sr_hand_commander.py): hand management class. Documentation can be found in the following [link](https://dexterous-hand.readthedocs.io/en/latest/user_guide/2_software_description.html#srhandcommander).
* [SrArmCommander](https://github.com/shadow-robot/sr_interface/blob/melodic-devel/sr_robot_commander/src/sr_robot_commander/sr_arm_commander.py): hand management class

### SrArmCommander

The SrArmCommander inherits all methods from the [robot commander](https://dexterous-hand.readthedocs.io/en/latest/user_guide/2_software_description.html#srrobotcommander) and provides commands specific to the arm. It allows movement to a certain position in cartesian space, to a configuration in joint space
or move using a trajectory.

#### Setup
```eval_rst
Import the arm commander along with basic rospy libraries and the arm finder:

.. code:: python

    import rospy
    from sr_robot_commander.sr_arm_commander import SrArmCommander
    from sr_utilities.arm_finder import ArmFinder

The constructors for ``SrArmCommander`` take a name parameter that should match the group name of the robot to be used and has the option to add ground to the scene.

.. code:: python

   arm_commander = SrArmCommander(name="right_arm", set_ground=True)
   
Use the ArmFinder to get the parameters (such as prefix) and joint names of the arm currently running on the system:

.. code:: python

   arm_finder = ArmFinder()
   
   # To get the prefix or mapping of the arm joints. Mapping is the same as prefix but without underscore.
   arm_finder.get_arm_parameters().joint_prefix.values()
   arm_finder.get_arm_parameters().mapping.values()
   
   # To get the arm joints
   arm_finder.get_arm_joints()
```

#### Getting basic information
```eval_rst
To return the reference frame for planning in cartesian space:

.. code:: python

   reference_frame = arm_commander.get_pose_reference_frame()
```

#### Plan/move to a position target
```eval_rst
Using the method ``move_to_position_target``, the end effector of the arm can be moved to a certain point
in space represented by (x, y, z) coordinates. The orientation of the end effector can take any value.

Parameters:

-  *xyz* desired position of end-effector
-  *end\_effector\_link* name of the end effector link (default value is
   empty string)
-  *wait*  indicates if the method should wait for the movement to end or not
   (default value is True)
```
##### Example
```eval_rst

.. code:: python

   rospy.init_node("robot_commander_examples", anonymous=True)
   arm_commander = SrArmCommander(name="right_arm", set_ground=True)

   new_position = [0.25527, 0.36682, 0.5426]
    
   # To only plan
   arm_commander.plan_to_position_target(new_position)
    
   # To plan and move
   arm_commander.move_to_position_target(new_position)
```

#### Plan/move to a pose target
```eval_rst
Using the method ``move_to_pose_target`` allows the end effector of the arm to be moved to a certain pose
(position and orientation) in the space represented by (x, y, z, rot\_x,
rot\_y, rot\_z).

Parameters:

-  *pose* desired pose of end-effector: a Pose message, a PoseStamped
   message or a list of 6 floats: [x, y, z, rot\_x, rot\_y, rot\_z] or a
   list of 7 floats [x, y, z, qx, qy, qz, qw]
-  *end\_effector\_link* name of the end effector link (default value is
   empty string)
-  *wait* indicates if the method should wait for the movement to end or not
   (default value is True)
```
##### Example
```eval_rst

.. code:: python

   rospy.init_node("robot_commander_examples", anonymous=True)
   arm_commander = SrArmCommander(name="right_arm", set_ground=True)

   new_pose = [0.5, 0.3, 1.2, 0, 1.57, 0]
   
   # To only plan
   arm_commander.plan_to_pose_target(new_pose)
   
   # To plan and move
   arm_commander.move_to_pose_target(new_pose)

```
