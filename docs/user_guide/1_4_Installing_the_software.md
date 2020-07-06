# Installing the software

We have created a one-liner that is able to install Docker, download the image and create a new container for you. It will also create two desktop icons, one to start the container and launch the hand and another one to save the log files locally. To use it, you first need to have a PC with Ubuntu installed on it (version 18.04) then follow these steps:

## Check your hand interface ID

Before setting up the docker container, the EtherCAT interface ID for the hand needs to be discovered. In order to do so, after plugging the hand’s ethernet cable into your machine and powering it up, please run

```eval_rst
.. prompt:: bash $

   sudo dmesg
```
command in the console. At the bottom, there will be information similar to the one below:

```bash
[490.757853] IPv6: ADDRCONF(NETDEV_CHANGE): enp0s25: link becomes ready
```
In the above example, ‘enp0s25’ is the interface ID that is needed.

## Get ROS Upload login credentials

If you want to upload technical logged data (ROS logs, backtraces, crash dumps etc.) to our server and notify the Shadow’s software team to investigate your bug, then you need to enable logs uploading in the one-liner. In order to use this option you need to obtain a unique upload key. It can be found in the delivering instructions or by emailing sysadmin@shadowrobot.com. When you receive the key you can use it when running the one-liner installation tool. To enable the logs uploading you need to add the command line option --read-secure customer_key to the one-liner after server_and_nuc_deploy. After executing the one-liner, it will prompt you to enter your “Secure data input for customer_key”. Please copy and paste here your key.

## Check your hand configuration branch

You should have the name of your [sr_config](https://github.com/shadow-robot/sr-config) hand branch which contains the specific configuration of your hand (calibration, controller tuning etc…).
Usually it is something like this: ``shadowrobot_XXXXXX``. Where XXXXXX are the 6 digits contained in the serial number of the hand labelled underneath the robot base.

If you are unsure please contact us at support@shadowrobot.com.

## Run the one-liner

The one-liner will install Docker, pull the image from Docker Hub, and create and run a container with the parameters specified. 

Running the one-liner requires that you can access bit.ly and raw.githubusercontent.com with your internet connection (bit.ly/run-aurora resolves to https://raw.githubusercontent.com/shadow-robot/aurora/master/bin/run-ansible.sh). If either of those is unreachable in your country, try using a VPN.

In order to use it, follow these instructions:

Connect the ethernet between the NUC-CONTROL and the new PC using the instructions above
Power on the new PC
Connect an ethernet cable providing external internet connection to the back of the new PC
Power on the NUC-CONTROL
Connect the arm to the NUC to the NUC's onboard ethernet port
Install the hand and arm software on the new PC by running the following on a terminal (Ctrl+Alt+T):

```eval_rst
.. Note:: Please remember to replace [EtherCAT interface ID] with your Interface ID and [sr_config_branch] with your unique sr_config branch
```

ROS Melodic (Recommended) for right hand and arm:

```eval_rst
.. prompt:: bash $

    bash <(curl -Ls bit.ly/run-aurora) server_and_nuc_deploy product=hand_e ethercat_interface=[EtherCAT interface ID] config_branch=[sr_config_branch] reinstall=true upgrade_check=true tag=melodic-release ethercat_right_arm=[NUC right arm ethernet interface ID] arm_ip_right="192.168.1.1" ur_robot_type=ur10e hand_side=right
```

ROS Melodic (Recommended) for left hand and arm:

```eval_rst
.. prompt:: bash $

    bash <(curl -Ls bit.ly/run-aurora) server_and_nuc_deploy product=hand_e ethercat_left_hand=[EtherCAT interface ID] config_branch=[sr_config_branch] reinstall=true upgrade_check=true tag=melodic-release ethercat_left_arm=[NUC left arm ethernet interface ID] arm_ip_left="192.168.2.1" ur_robot_type=ur10e hand_side=left
```

ROS Melodic (Recommended) for both left and right arms and hands:

```eval_rst
.. prompt:: bash $

    bash <(curl -Ls bit.ly/run-aurora) server_and_nuc_deploy product=hand_e ethercat_interface=[EtherCAT right hand interface ID] ethercat_left_hand=[EtherCAT left hand interface ID] config_branch=[sr_config_branch] reinstall=true upgrade_check=true tag=melodic-release ethercat_right_arm=[NUC right arm ethernet interface ID] ethercat_left_arm=[NUC left arm ethernet interface ID] arm_ip_right="192.168.1.1" arm_ip_left="192.168.2.1" ur_robot_type=ur10e bimanual=true
```

Examples:
For Interface ID ```ens0s25``` and sr_config_branch ```shadow_12345``` for right arm and hand:

```eval_rst
.. prompt:: bash $

    bash <(curl -Ls bit.ly/run-aurora) server_and_nuc_deploy product=hand_e ethercat_interface=ens0s25 config_branch=shadow_12345 reinstall=true upgrade_check=true tag=melodic-release ethercat_right_arm=[NUC right arm ethernet interface ID] arm_ip_right="192.168.1.1" ur_robot_type=ur10e
```  

Same as above but with ROS logs upload enabled for right arm and hand:

```eval_rst
.. prompt:: bash $

    bash <(curl -Ls bit.ly/run-aurora) server_and_nuc_deploy --read-secure customer_key product=hand_e ethercat_interface=ens0s25 config_branch=shadow_12345 reinstall=true upgrade_check=true tag=melodic-release ethercat_right_arm=[NUC right arm ethernet interface ID] arm_ip_right="192.168.1.1" ur_robot_type=ur10e
```  

If you do not have an Nvidia graphics card, you can add nvidia_docker=false.

You can also change reinstall=false in case you do not want to reinstall the docker image and container. When it finishes it will show if it was successful or not and will create desktop icons on your desktop that you can double-click to launch the hand container, save the log files from the active containers to your desktop and perform various actions on the hand (open, close and demo).


When the one-liner finishes it will show:

```bash
Operation completed
```

and it will create two desktop icons on your desktop that you can double-click to launch the system or save the log files from the active containers to your desktop.

# Starting the driver

Launch the driver for the Shadow Hand using the desktop icon 'Launch Shadow Right Hand' or 'Launch Shadow Left Hand' or 'Launch Shadow Bimanual Hands'.

## Lights in the hand
When the ROS driver is running you should see the following lights on the Palm:

```eval_rst
========================   =============       ================    =================================
Light                      Colour              Activity            Meaning
========================   =============       ================    =================================
Run                        Green               On                  Hand is in Operational state
CAN1/2 Transmit            Blue                V.fast flicker      Demand values are being sent to the motors
CAN1/2 Receive             Blue                V.fast flicker      Motors are sending sensor data
Joint sensor chip select   Yellow              On                  Sensors being sampled
========================   =============       ================    =================================
```

After killing the driver, the lights will be in a new state:
```eval_rst
========================   =============       ================    =================================
Light                      Colour              Activity            Meaning
========================   =============       ================    =================================
Run                        Green               Blinking            Hand is in Pre-Operational state
CAN1/2 Transmit            Blue                Off                 No messages transmitted on CAN 1/2
CAN1/2 Receive             Blue                Off                 No messages received on CAN 1/2
Joint sensor chip select   Yellow              Off                 Sensors not being sampled
========================   =============       ================    =================================
```

# Saving log files and uploading data to our server
After running the one-liner, you will also notice a second icon named `Shadow ROS Logs Saver and Uploader` that is used to retrieve and copy all the available logs files from the active containers locally to your Desktop. This icon will create a folder that matches the active container's name and the next level will include the date and timestamp it was executed. When it starts, it will prompt you if you want to continue, if you press yes it will close all active containers. After pressing "yes", you will have to enter a description of the logging event and will start copying the bag files, logs and configuration files from the container and then exit. Otherwise, the window will close and no further action will happen. If you provided an upload key with the one-liner installation then the script will also upload your LOGS in compressed format to our server and notify the Shadow's software team about the upload. This will allow the team to fully investigate your issue and provide support where needed.
