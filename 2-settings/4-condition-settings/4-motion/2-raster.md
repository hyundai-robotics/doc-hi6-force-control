#### 2.4.4.2 Force Control Condition Setup - Motion - Auto Path Generation

Sets the motion control conditions to be executed during force control operations.

This section is specifically used to configure **Spiral, Bi-directional, and Zig-zag** paths and trajectories.


<br>

---



![](../../../_assets/_13_fctrl_ctrl_cnd_motion_raster1.png)

![](../../../_assets/_15_fctrl_ctrl_cnd_motion_raster3.png)


### **Motion Types**

| Item |
|----------------|
| **Spiral Motion** |
| **Bi-directional Motion** |
| **Zig-zag Motion** |

<br>

---

![](../../../_assets/_14_fctrl_ctrl_cnd_motion_raster2.png)

### **Spiral Motion**

A function that generates a spiral path and trajectory.

| Item | Description |
|--------------|------|
| **Velocity** | Rotational linear velocity (mm/s) |
| **Radius** | Maximum radius setting (mm) - The final size of the spiral |
| **Revolutions** | Number of revolutions (rev) - Total count of rotations |


<br>

---


### **Bi-directional Motion**

A function that generates a bi-directional path and trajectory.

| Item | Description |
|--------------|------|
| **Velocity** | Linear velocity (mm/s) |
| **Mov Dir** | Movement Direction (+X, -X, +Y, -Y) |
| **Mov Length** | Movement Length (mm) |
| **Shift Dir** | Shift Direction (+X, -X, +Y, -Y) |
| **Shift Length** | Shift (Pitch) Length (mm) |
| **Num Lines** | Number of lines to be generated in the movement direction |

<br>

---

### **Zig-zag Motion**

A function that generates a zig-zag path and trajectory.

| Item | Description |
|--------------|------|
| **Velocity** | Linear velocity (mm/s) |
| **Mov Dir** | Movement Direction (+X, -X, +Y, -Y) |
| **Mov Length** | Movement Length (mm) |
| **Shift Dir** | Shift Direction (+X, -X, +Y, -Y) |
| **Shift Length** | Shift (Pitch) Length (mm) |
| **Num Lines** | Number of lines to be generated relative to the movement direction |

<br>

---

{% hint style="info" %}

- This motion generates a path based on the **XY plane** relative to the coordinate system selected in **2.4.1 (Force Control Condition Setup - Basic)**.

{% endhint %}