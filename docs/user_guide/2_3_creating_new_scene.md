## Creating a new world/scene

In this section, instructions on how to create, modify and save new `.world` and `.scene` file are provided. All the necessary console commands are described in depth, however, it is recommended that the user uses the graphical user interface introduced at the end of this section.

### Using console commands

#### Running template world file

In order to start creating a new world file, first you need to run a launch file with a template world file, i.e.:

```eval_rst
.. prompt:: bash $

   roslaunch sr_world_generator create_world_template.launch
```
This will open Gazebo and Rviz with a robot in place:

```eval_rst
.. image:: ../img/empty_world.png
  :width: 400
  :align: center
```
In most cases, when one of Shadow's robot tables is used, the above command will suffice. However, the launch file can be run with multiple arguments. Arguments available for the launch file:
* **start_home** - if set to `true`, robot will start in a predefined home pose. Default value: `true`
* **scene** - if set to `true`, a scene from world file defined by the world argument will be generated. Default value: `false`
* **initial_z** - value defining positioning of the robot base in the world frame. Default value: `0.7751`
* **world** - path to a world file that will be spawned in gazebo after running the launch file. No default value, needs to be explicitly specified if `scene` argument is set to `true`.

As an example, a launch file starting with robot NOT in home position with a base at 0.5m height would be called as follows:

```eval_rst
.. prompt:: bash $

   roslaunch sr_world_generator create_world_template.launch start_home:=false initial_z:=0.5
```

#### Adding objects to the world

In order to add an existing object to the world, navigate to the left hand side bar in Gazebo and click on the **Insert** tab:

```eval_rst
.. image:: ../img/insert_object.png
  :width: 400
  :align: center
```

A list of objects will appear. Please do not use other objects than the ones kept in sr_description_common (i.e. the ones in second drop down on the list):

```eval_rst
.. image:: ../img/object_list.png
  :width: 400
  :align: center
```

In order to add an object, click on its name and move the cursor back to the scene. A shadow of the object will appear that you can move around. Single left click will put the object in a specified location.

```eval_rst
.. image:: ../img/table_added.png
  :width: 400
  :align: center
```

In order to move the object around, click on the object, then click the following icon found at the top of the panel,

```eval_rst
.. image:: ../img/move_object.png
  :width: 400
  :align: center
```

then click back on the object. You can move it around now. It is usually easier to use the appearing axis frame instead of trying to drag the object itself.

The same process can be done for rotation, after clicking this icon:

```eval_rst
.. image:: ../img/rotate_object.png
  :width: 400
  :align: center
```

It is also possible to set the specific pose of the object in the pose field. You can do that by clicking the object, navigating to the `pose` drop-down on the left-hand side bar and setting desired pose.

```eval_rst
.. image:: ../img/pose_change.png
  :width: 400
  :align: center
```

A video depicting the process described above can be found [here](https://drive.google.com/file/d/1bm6PckbXbUY9ELF_6f4LWAIdXbkIZnQ1/view?usp=sharing).

#### Creating new objects

It is possible to create new object types from both meshes and primitives. First, an object needs to be placed in the scene. You can either drag a mesh that you want to modify as described above or use one of the available primitives that you can see at the top of the panel:

```eval_rst
.. image:: ../img/primitives.png
  :width: 400
  :align: center
```

In this example, we will be using a primitive to create a wall. After inserting the primitive in a scene, it's dimensions can be changed. In order to do that, right click on the model you just inserted and select **Edit model** option:

```eval_rst
.. image:: ../img/edit_model.png
  :width: 400
  :align: center
```

Further, right click the object again and select **Open Link Inspector**.

```eval_rst
.. image:: ../img/link_inspector.png
  :width: 400
  :align: center
```

Inside the **Link Inspector**, go to the **Visual** tab, scroll down to **Geometry** section and select desired dimensions. Further, go to **Collision** tab and do the same. Finally, click OK to confirm the changes. In the below example, a 1x1x1m square was reduced to a thin wall:

```eval_rst
.. image:: ../img/modified_model.png
  :width: 400
  :align: center
```

Next step is to save the model. Go to **File → Save as**. A pop-up window will show:

```eval_rst
.. image:: ../img/save_model.png
  :width: 400
  :align: center
```

For model name, DO NOT use numbers. Other than that, any name would suffice, provided it does not already exist in the models folder. In order to save the model in a proper location, use the **Browse** button and navigate to `models` folder in `sr_description_common` package (should be either `/home/user/projects/shadow_robot/base_deps/src/common_resources/sr_description_common/models` or `/home/user/projects/shadow_robot/base/src/common_resources/sr_description_common/models` directory). When you are ready, use the **Save** button to finish. Your model has now been saved. Go to **File → Exit Model Editor** to close the model editor. Now you can move and rotate the object as discussed in the section above.

As mentioned before, the same process (dimension change and saving) can be used with mesh files.

A video depicting the process described above can be found [here](https://drive.google.com/file/d/1yoLMEdtsf-U4bimTCqofrLLD3mPABT-9/view?usp=sharing).

#### Generating proper world file

When all the models are inserted in the scene and placed in desired position, the world file can be saved. Go to **File → Save World As** and select a name and a path of a world file saved with gazebo. Make sure to remember the path to the file. We recommend using the path `/home/user`. Although the file has now been saved, it has to be modified before being used by our launch files. In order to modify it, first kill the currently running Gazebo launch file and run:

```eval_rst
.. prompt:: bash $

   roslaunch sr_world_generator save_world_file.launch gazebo_generated_world_file_path:=path_to_file output_world_file_name:=file_name
```

where:
* **path_to_file** - path to file that was previously saved through gazebo,
* **file_name** -  desired name of the file (without extension). If not set, defaults to `new_world`.

When a message `World saved!` will appear in the console, kill the launch file. Your world has now been saved in `sr_description_common` package (`worlds` folder) and is ready to be used.

#### Creating a scene file

In order to generate a scene file for collision scene used in non-simulated scenarios, first run the initial launch file with the just created world file passed to the `world` argument:

```eval_rst
.. prompt:: bash $

   roslaunch sr_world_generator create_world_template.launch scene:=true world:=path_to_world
```

where **path_to_world** is the full path to the world file that just has been generated. When Rviz starts, on the left hand side, navigate to the **Scene Objects** tab

```eval_rst
.. image:: ../img/create_scene.png
  :width: 400
  :align: center
```

and click **Export As Text**. A pop-up window will appear asking for a name and path for the file. It is recommended that the file is saved in the sr_description_common package, scenes folder and it's name is the same as the corresponding world file.

A video depicting the process described above can be found [here](https://drive.google.com/file/d/1Uv1MeC2xc1nZ8Ati1cKaegHN8LJzsyhM/view?usp=sharing).

### Using the graphical user interface

A GUI has been implemented to help with the above operations.

```eval_rst
.. image:: ../img/world_generator_gui.png
  :width: 400
  :align: center
```

In order to start it, make sure no Gazebo sessions are up and run:

```eval_rst
.. prompt:: bash $

   roslaunch sr_world_generator world_generator_gui.launch
```

In order to start a new Gazebo session set following parameters to your preference:
* **start home** - choose `yes` if you want the robot to be starting in it's home pose
* **empty world** - choose `yes` if you want to start with an empty world. Choose `no` if you want to start the session with a specific world file loaded. You can type the path to the world file in the edit box or navigate to the file using the `browse` button
* **initial z** - set `z` position of the robot base. Default value corresponds to tables used at Shadow

After setting the above parameters to your preference, click `Open`. A new session of Gazebo will start. After modifying the world to your liking, as in the instructions in the previous sections, go to `File → Save World As` and select a name and a path of a world file. Make sure to remember the path to the file. We recommended the path `/home/user`. Although the file has now been saved, it has to be modified before being used by our launch files. In order to do that, first kill current Gazebo session using the `Close` button in the `Open Gazebo` section of the GUI. Then use the `Transform world file` area to navigate to your newly created Gazebo world file and click `Transform`. A pop-up window will appear asking for the properly formatted world file name. After clicking `Save` your file will be created and will be ready to be used.

You can use the `Open Gazebo` section again to check your newly created world file and export it to the `scene` file as described in the sections above.
