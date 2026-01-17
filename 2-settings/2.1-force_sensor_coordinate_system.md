## 2.1 Force Sensor Coordinate System

When mounting the force/torque (FT) sensor, the sensor coordinate system **must be aligned with the robot model's coordinate system**.

If the sensor frame is misaligned, the measured force/torque directions will not match reality, leading to **severely degraded control performance**.

<br>

---

### **Robot Sensor Coordinate Frame**

> The X, Y, and Z axes of the sensor coordinate system, as defined by our standard, are shown in the figure below:  
>
> The directions of the X, Y, and Z axes defined in the sensor model **must match** the robot's sensor coordinate system.

![](../_assets/_05_fctrl_ctrl_sensor_crd.png)

⚠️ The robot in the above diagram is in its default posture.  
⚠️ Most circular FT sensors have coordinate direction markings on the sensor body.  

<br>

### 💡 Configuration Tips

- **If the axes are inverted**: apply axis inversion or transformation in the software.
- **When entering the tool center of mass**: use the sensor's coordinate frame.
- **Before zeroing the sensor**: verify that the coordinate direction is correct.

---