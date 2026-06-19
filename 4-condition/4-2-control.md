### 4.2 Control Parameters

This menu is used to select the degrees of freedom (axes) to apply force control, and to configure the target force/torque, responsiveness of the virtual system, viscous resistance (damping), and speed and displacement limit values. These are key parameters that determine the flexibility and reaction speed of the actual robot when it comes into contact with the environment.

[F2: System] ➔ [4: Application Parameter] ➔ [24: Force Control] ➔ [3: Force Control Options] ➔ **Select [Settings] Tab**

---

![](../_assets/_07_fctrl_ctrl_cnd_control.png)


##### **[Control Configuration Items]**


| Item | Description |
| :--- | :--- |
| **Axis** | Indicates the 6-DOF axes targeted for control. (X, Y, Z: Linear velocity directions / Rx, Ry, Rz: Rotational directions) |
| **Active** | Specifies whether to activate force control for the corresponding axis. When activated, the box lights up in **yellow**. |
| **Target** | Enter the target force (Unit: N) or target torque (Unit: Nm). |
| **Response** | Adjusts the initial responsiveness (%) of the robot to external forces or target value changes. The **lower the set value, the faster the control response speed, allowing it to reach the target value agilely**. |
| **Damping** | The damping ratio (%) that matches the virtual viscous damping coefficient. The **lower the set value, the more flexibly it conforms** and responds to external forces. |
| **Limit** | Limits the maximum output speed that can occur during force control operation. (Linear axis: mm/s, Rotational axis: deg/s) |
| **-Pos / +Pos** | The bidirectional travel limit (soft limit) range within which the robot can be forcibly pushed or moved during force control operation. (mm or deg) |


{% hint style="info" %}

**Coordinate System Reference:** The direction definition of each axis (X, Y, Z, Rx, Ry, Rz) is mapped based on the **task coordinate system selected in the preceding [Settings] tab**.

**Response Tuning Guide:**
  * **When set to 0%:** This is advantageous for mitigating the impact generated during initial contact, stably controlling the movement, and suppressing vibrations. (However, a larger damping value results in a slower response.)
  * **When set to 1% or higher:** The target control speed and tracking performance are improved, allowing for a more agile response. However, within certain ranges, the deviation in responsiveness according to the change in the set value may be subtle.

**Speed and Position Limit Management:** If the balance between response and damping settings is incorrect, or if the speed limit value is set excessively high, the robot may accelerate rapidly upon contact with an object, causing system vibrations. During initial tuning, always ensure safety by **setting the [Limit] speed value low**, and then gradually increase control performance.

{% endhint %}

---

##### **Control Configuration Example (Vertical Direction Sanding Task)**

This is a UI configuration matching example for a typical sanding/grinding process that maintains the posture of the actual tool while applying pressure.


| Axis | Active | Target | Response | Damping | Limit | Position Limit (- / +) |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **X** | Off | 0 N | 0 % | 100 % | 0 mm/s | 0 / 0 mm |
| **Y** | Off | 0 N | 0 % | 100 % | 0 mm/s | 0 / 0 mm |
| **Z** | **On** | **20 N** | **10 %** | **20 %** | **5 mm/s** | **0 / 30 mm** |
| **Rx** | **On** | **0 Nm** | **0 %** | **10 %** | **5 deg/s** | **-20 / 20 deg** |
| **Ry** | **On** | **0 Nm** | **0 %** | **10 %** | **5 deg/s** | **-20 / 20 deg** |
| **Rz** | Off | 0 Nm | 0 % | 100 % | 0 deg/s | 0 / 0 deg |

* **Z-axis Control:** Gently settles onto the surface while maintaining a **constant force of 20N** in the normal direction (pressurizing axis).
* **Rx, Ry-axis Control:** Soft motion compliance occurs as the tool is coupled with a **target torque of 0Nm and low damping (10%)** to allow it to remain flat in response to curved or warped machining surface edges.
* The coordinate system must be configured to "Tool".

---

{% hint style="warning" %}

**Vibration and Noise Notice:** Lowering the damping and response ratios allows for a flexible response to external environment changes. However, if the static stiffness of the target object is too high or combined with high-speed robot operation conditions, it may cause **vibrations and high-frequency noise** due to control phase lag, so an adequate damping margin must be secured.

{% endhint %}