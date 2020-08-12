# Setting up the arm

1. Unpack the robot arm and the control box (Follow the instructions found on the UR manual included in the box)
2. Mount the arm on the table. If you have a Shadow Stand or Table, the cable socket should point roughly towards the wire hole in the table. Place the base of the robot onto the mounting plate and add screws from the top. 
   ```eval_rst
   .. image:: ../img/ur_position_on_table.png
   ```
3. Place the control box on its foot and under the table so its not trip hazard.
   ```eval_rst
   .. image:: ../img/ur10_control_box.jpg
   ```
4. Plug in the robot cable between the robot and the control box.
   ```eval_rst
   .. image:: ../img/ur10_control_box_cables.jpg
   ```
5. Plug in the mains plug of the control box.

To quickly start up the robot after it has been installed, perform the following steps:
1. Press the power button on the teach pendant.
2. Wait a minute while the system is starting up, displaying text on the touch screen.
3. Press ON button on the touch screen. Wait a few seconds until robot state changes to idle.
4. Press START button on the touch screen. The robot now makes a sound and moves a little while releasing the brakes.

## Configuring the network

In order to use the robot with our driver you need to change the network setup of the robot via the pendant, performing the following steps:
1. To setup the IP of the robot Press Exit on Initialization screen:

   ```eval_rst
   .. image:: ../img/configure_arm_1.jpg
   ```
   
   You should see the following screen:
   ```eval_rst
   .. image:: ../img/configure_arm_2.jpg
   ```
   
2. Press the "Setup Robot" button and you should see the following screen:
   ```eval_rst
   .. image:: ../img/configure_arm_3.jpg
   ```
   
3. Then press the "Network" button. In this screen, you need to enable the network by clicking the "Static Address" radio button. Change the IP address and Subnet mask as shown below:
   * IP address: 192.168.1.1
   * Subnet mask: 255.255.255.0
   
   ```eval_rst
   .. image:: ../img/configure_arm_4.jpg
   ```
4. Press "Apply" when you finish.

## Make sure the mounting settings are correct

In the UR pendant, go to "Installation" and then "Mounting" (Section 13.7 on the UR User Manual).

```eval_rst
.. image:: ../img/ur_mounting_settings.png
```

This serves two purposes:
1. Making the robot arm look right on the screen.
2. Telling the controller about the direction of gravity.

The controller uses an advanced dynamics model to give the robot arm smooth and precise motions, and to make the robot arm hold itself when in Freedrive mode. For
this reason, it is very important that the mounting of the robot arm be set correctly.

The default is that the robot arm is mounted on a flat table which is our case, in which case no change is needed on this screen. Please verify that this is the case. In case you want to mount the robot on the ceiling, a wall or at an agle, change this using the push-buttons.

## UR10e configuration - Set remote control mode

On the UR arm e-Series the robot has to be in remote control mode to be used in headless mode. This has to be switched from the Teach-Pendant in the following way:

1. Turn on the Robot via the Teach-Pendant and then, click on the menu on the right corner of the top bar:

```eval_rst
.. image:: ../img/ur10e1.jpeg
```

2. In the drop down menu, select ‘Settings’:

```eval_rst
.. image:: ../img/ur10e2.jpeg
```

3. On the left side menu select ‘Systems’ and then ‘Remote Control’:

```eval_rst
.. image:: ../img/ur10e3.jpeg
```

4. In the pop-up screen select ‘Enable’:

```eval_rst
.. image:: ../img/ur10e4.jpeg
```

5. After step 4 a new small icon called ‘Local’ will appear on the right side of the top bar menu:

```eval_rst
.. image:: ../img/ur10e5.jpeg
```

6. Click on the Local icon and in the drop down menu select Remote Control:

```eval_rst
.. image:: ../img/ur10e6.jpeg
```

7. The top bar should look like the picture below:

```eval_rst
.. image:: ../img/ur10e7.jpeg
```

### Important Remark

Steps 1-5 needs to be done only once. After these steps are executed, the robot can quickly be switched between Local and Remote Control by using the icon and the drop-down menu shown in step 6.

The change is persistent with rebooting. 

When Remote Control mode is active the UR10e can only be controlled via the Remote machine (Laptop). In order to use the local commands on the pendant (e.g. free-drive mode), the mode needs to be switched back to Local Control.

In order to do this, click on the Remote Control icon on the top right bar and in the pop-up menu select Local Control.

## UR supporting firmware

In the following table, you can find the firmware version of the Universal Robot software and see if it has been tested with our software:

```eval_rst
+---------------------------+-----------------------------------+-----------------------------------+--------------------+--------------------+---------------+-------------+------------+-------------------+
| UR Software Version       | User Interface                    | Robot Controller                  | Safety Processor A | Safety Processor B | Hostname      | IP address  | s/n        | Tested?           |
+---------------------------+-----------------------------------+-----------------------------------+--------------------+--------------------+---------------+-------------+------------+-------------------+
| 3.3.4.310 (Dec 06 2016)   | PolyScope 3.3.4.310 (Dec 06 2016) | URControl 3.3.4.208 (Dec 06 2016) | URSafetyA 504      | URSafetyB 256      | ur-2017304270 | 192.168.1.1 | 2017304270 | `Yes`__           |
+---------------------------+-----------------------------------+-----------------------------------+--------------------+--------------------+---------------+-------------+------------+-------------------+
| 3.4                       |                                   |                                   |                    |                    |               |             |            | Not tested        |
+---------------------------+-----------------------------------+-----------------------------------+--------------------+--------------------+---------------+-------------+------------+-------------------+
| 3.5                       |                                   |                                   |                    |                    |               |             |            | Not tested        |
+---------------------------+-----------------------------------+-----------------------------------+--------------------+--------------------+---------------+-------------+------------+-------------------+
| 3.6                       |                                   |                                   |                    |                    |               |             |            | Yes in Serfow Lab |
+---------------------------+-----------------------------------+-----------------------------------+--------------------+--------------------+---------------+-------------+------------+-------------------+
| 3.7.0.40195 (Aug 22 2018) |                                   |                                   | URSafetyA (3.5.2)  | URSafetyB (3.5.4)  | ur-2018300632 | 192.168.1.1 | 2018300632 | `Yes`__           |
+---------------------------+-----------------------------------+-----------------------------------+--------------------+--------------------+---------------+-------------+------------+-------------------+
| 3.7.2.40245 (Oct 05 2018) |                                   |                                   | URSafetyA (3.5.2)  | URSafetyB (3.5.4)  | ur-2018301419 | 192.168.1.1 | 2018301419 | Demo Room 2       |
+---------------------------+-----------------------------------+-----------------------------------+--------------------+--------------------+---------------+-------------+------------+-------------------+
| 3.8.0.61336 (Nov 22 2018) |                                   |                                   | URSafetyA (3.5.2)  | URSafetyB (3.5.4)  | ur-2018301649 | 192.168.1.1 | 2018301649 | Demo Room 2       |
+---------------------------+-----------------------------------+-----------------------------------+--------------------+--------------------+---------------+-------------+------------+-------------------+
| 3.10.0                    |                                   |                                   | URSafetyA (3.5.2)  | URSafetyB (3.5.4)  |               | 192.168.1.1 |            | Yes               |
+---------------------------+-----------------------------------+-----------------------------------+--------------------+--------------------+---------------+-------------+------------+-------------------+
| 3.11                      |                                   |                                   | URSafetyA (3.5.2)  | URSafetyB (3.5.4)  |               | 192.168.1.1 |            | Yes               |
+---------------------------+-----------------------------------+-----------------------------------+--------------------+--------------------+---------------+-------------+------------+-------------------+

__ https://shadowrobot.atlassian.net/projects/SRC?selectedItem=com.atlassian.plugins.atlassian-connect-plugin:com.kanoah.test-manager__main-project-page#!/testPlayer/SRC-R82

__ https://shadowrobot.atlassian.net/projects/SRC?selectedItem=com.atlassian.plugins.atlassian-connect-plugin:com.kanoah.test-manager__main-project-page#!/testPlayer/SRC-R83
```

Please make sure that when you test a new firmware version to update the file [known_good_firmware](https://github.com/shadow-robot/common_resources/blob/melodic-devel/sr_firmware_checker/config/known_good_firmware.txt) with a PR adding the numbers as shown in the file.
