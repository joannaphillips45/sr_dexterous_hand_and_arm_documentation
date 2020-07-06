# Setting up a simulated system 

## Gazebo

[Gazebo](http://gazebosim.org/) is our default simultator. Follow the intructions on the next section to install and run a simulation of our robot hands using Gazebo.

### Installing the software (sim)

If you do not actually have a real hand and arm but would like to use them in simulation, then please run the following command:

Running the one-liner requires that you can access bit.ly and raw.githubusercontent.com with your internet connection (bit.ly/run-aurora resolves to https://raw.githubusercontent.com/shadow-robot/aurora/master/bin/run-ansible.sh). If either of those is unreachable in your country, try using a VPN.

ROS Melodic (Recommended):
```eval_rst
.. prompt:: bash $

    bash <(curl -Ls bit.ly/run-aurora) server_and_nuc_deploy --limit 'all!dhcp' product=hand_e reinstall=true upgrade_check=true tag=melodic-release ur_robot_type=ur10e hand_side=right sim_icon=true
```


If you do not have an Nvidia graphics card, you can add nvidia_docker=false.

You can also change reinstall=false in case you do not want to reinstall the docker image and container. When it finishes it will show if it was successful or not and will create desktop icons on your desktop that you can double-click to launch the hand container, save the log files from the active containers to your desktop and perform various actions on the hand (open, close and demo).

When it finishes it will show:
```bash
Operation completed
```
and it will create two icons on your desktop that you can double-click to launch the container with the system or save the log files.

### Starting a robot in simulation

First you need to start the system container by either double clicking the icon "Shadow Advanced Launchers/1 - Launch Server Container" or running the following command:
```eval_rst
.. prompt:: bash $

   docker start dexterous_hand_real_hw
```
Then, inside the container, launch the arm and hand by running:
```eval_rst
.. prompt:: bash $

   roslaunch sr_robot_launch sr_right_ur10arm_hand.launch
```
