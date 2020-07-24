## Table-Arm Calibration Procedure

```eval_rst
.. Note:: Follow these steps if you need to calibrate the arm with the table e.g. position objects on the table on a known position. You should have a table and a stylus provided by Shadow Robot. It should only be run once when the table is setup for the first time. 
```

1. The arm should be mounted on the table but without hand. First, mount the calibration stylus as shown below:

   ```eval_rst
   .. image:: ../img/arm_calibration_stylus.png
     :width: 200
     :align: center
   ```

2. Attach the ar_marker base to the table without the markers on
   
3. Type CTRL+ALT+T to open a terminal and start arm with command:
    
   ```eval_rst
   .. prompt:: bash $

       roslaunch sr_robot_launch sr_ur10arm_box.launch sim:=false
   ```
   
4. Open another terminal (CTRL+ALT+T) and set the payload with the following command:
   
   ```eval_rst
   .. prompt:: bash $ 
   
       rosservice call /ra_sr_ur_robot_hw/set_payload "mass_kg: 0.0 centre_of_mass_m: x: 0.0 y: 0.0 z: 0.0"
   ```
   
5. Then, in the same terminal, change the control to `teach_mode` running the following:
   ```eval_rst
   .. prompt:: bash $
   
       rosservice call /teach_mode "teach_mode: 1 robot: 'right_arm'"
   ```
   Now you should be able to move the arm freely

6. For each marker to be calibrated:
   * Run:
     ```eval_rst
     .. prompt:: bash $
     
         roslaunch sr_workspace_calibrator calibrator.launch [calibration_frame:=FRAME_NAME]
     ```
     * For multi marker setups, `FRAME_NAME` should be unique. For a single marker setup (most cases), this can be omitted and the default name `ra_calibration_marker` will be used.
     * Follow on screen instructions, touching carefully the tip of stylus into each hole. 
       ```eval_rst
       .. image:: ../img/arm_calibration_holes.png
         :width: 300
         :align: center
       ```
       
       <br>
     
       ```eval_rst
       .. Note:: Hole 0 is nearest to arm base and numbers increase ANTI CLOCKWISE from 0.
       ```
       
   * Repeat 10 times for each hole (0,1,3).    
     
     ```eval_rst
     .. Note:: Hole 2 (shown in red) does not get probed.
     ```
  
7. The output of the process will be a yaml file named FRAME_NAME.yaml stored in sr_workspace_calibrator/config

8. Finally to finish, change the control back running the following command:
   ```eval_rst
   .. prompt:: bash $
       
       rosservice call /teach_mode "teach_mode: 0 robot: 'right_arm'"
   ```
   Now you should not be able to move the arm

If you want to use an existing calibration, a calibration tf can be broadcast by running:
```eval_rst
.. prompt:: bash $
    
    roslaunch sr_workspace_calibrator calibration_tf.launch [calibration_frame:=FRAME_NAME]
```

As before, for single marker setups, FRAME_NAME can be omitted and the default ra_calibration_marker will be used. The launch command can of course also be included in other launch files.
