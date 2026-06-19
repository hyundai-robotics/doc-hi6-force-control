## 2.1 F/T Sensor Installation 

When mounting an F/T sensor for precise force control, the physical attachment direction of the sensor must perfectly match the sensor coordinate system configuration within the robot controller. 

If the sensor mounting direction or coordinate system configuration is misaligned, the direction of the force/torque recognized by the controller will differ from the actual direction, which may cause the force control loop to diverge or the robot to malfunction.

---

##### **[Definition of F/T Sensor Coordinate System]**

* **Controller-Based Sensor Coordinate System Rule:** The directions of the `X, Y, and Z axes` of the default sensor coordinate system defined by our robot controller are shown in the figure below.

* **Physical Direction Alignment:** The sensor must be oriented and assembled so that the unique `X, Y, and Z axis` index lines engraved (or printed) on the side of the circular F/T sensor body perfectly align with the direction of the robot's sensor coordinate system.

![](../_assets/_05_fctrl_ctrl_sensor_crd.png)

* **Coordinate System Reference Pose:** The manual figure above shows the sensor coordinate system defined based on the robot being in its standard home position.

* **Precautions during Assembly:** When assembling the sensor mechanism, cross-reference the cable outlet direction or the sensor dowel pin positions with the axis definitions in the manual to ensure it is not mounted in the reverse direction or with an incorrect phase.

---

{% hint style="info" %}

**Tool Load Information Reference:** When identifying dynamic loads and registering tool load information, the center of gravity position must be measured and entered based on the **origin of the F/T sensor reference coordinate system**, not the robot flange coordinate system.

**Prerequisite Check Before Sensor Zero Offset (Bias) Calibration:** Before performing the zero offset (Bias) calibration of the sensor signal, always verify qualitatively on the sensor diagnostic screen that the signs (+/-) of the forces (Fx, Fy, Fz) for the corresponding axes match the actual directions when the robot tool is pushed in a specific direction.

{% endhint %}