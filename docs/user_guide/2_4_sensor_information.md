## Sensor information
### Force/Torque feedback (only applicable for UR10e)
The UR10e comes equipped with a force/torque sensor on the end effector with the following specifications:

```eval_rst
+----------------------------+---------+
| F/T Sensor - Force, x-y-z  |         |
+----------------------------+---------+
| Range                      | 100 N   |
+----------------------------+---------+
| Resolution                 | 2.0 N   |
+----------------------------+---------+
| Accuracy                   | 5.5 N   |
+----------------------------+---------+

+----------------------------+---------+
| F/T Sensor - Torque, x-y-z |         |
+----------------------------+---------+
| Range                      | 10 Nm   |
+----------------------------+---------+
| Resolution                 | 0.02 Nm |
+----------------------------+---------+
| Accuracy                   | 0.60 Nm |
+----------------------------+---------+
```

To read the data from the sensor use the topic:
```eval_rst
.. prompt:: bash $

   rostopic echo /wrench
```

It is of type WrenchStamped as defined [here](http://docs.ros.org/melodic/api/geometry_msgs/html/msg/WrenchStamped.html).
