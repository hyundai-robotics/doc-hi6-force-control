### 2.4.2 Force Control Condition Setup - Control

Select the force control axes and set the target force value, stiffness, speed, and pose limit for each direction.

This section is the core of force control and determines the responsiveness of the actual robot movement.

<br>

---

![](../../_assets/_07_fctrl_ctrl_cnd_control.png)


#### **Control Configuration Items**

| Item | Description |
|------------|------|
| **Axis** | Controllable axes (X, Y, Z, Rx, Ry, Rz) |
| **Act** | Whether to activate control for the corresponding axis (Active when checked ✓) |
| **Force / Torque** | Target Force (N) or Torque (Nm)<br>Example: Set 50N for the Z-axis |
| **Stiff** | Stiffness ratio (%), lower values allow more flexible response |
| **Vel** | Movement speed limit during force control (mm/s or deg/s) |
| **(-)Pose / (+)Pose** | Position limits in negative/positive directions (mm or deg)<br>Restricts robot movement when exceeded |

<br>

---

#### **Control Configuration Example**

The following settings are for a **vertical sanding** operation:

| Axis | Act | Force / Torque | Stiff | Vel | Pose Limit |
|------|------|----|------|------|-------------|
| **Z** | ✓ | 50N | 30% | 20 mm/s | -50 ~ +50 mm |
| **Rx** | ✓ | 0 Nm | 10% | 5 deg/s | -10 ~ +10 deg |
| **Ry** | ✓ | 0 Nm | 10% | 5 deg/s | -10 ~ +10 deg |
| **X**, **Y**, **Rz** | - | - | - | - | - | 

→ The robot maintains a force of 50N in the Z-axis direction, while the tool rotation directions (Rx, Ry) respond flexibly.

<br> 

---


{% hint style="info" %}


Detailed control for each axis must be adjusted based on actual working conditions (e.g., surface curvature, precision requirements, etc.). Lower gains result in a more flexible response.

While lower stiffness ratios provide a flexible response, they may cause vibration and noise depending on the robot's responsiveness and the surrounding environment.

{% endhint %}

