### 4.4.2 Profile: Velocity Clamp

During force control operation, if the speed is excessively high when the robot makes contact with the environment (object), excessive overshoot and divergence (vibration) of the control system will occur. This function is designed to fundamentally suppress mechanical vibrations and impacts of the system by forcibly clamping the robot's maximum operating speed (Vmax) to a lower level the moment the currently detected force/torque value exceeds a user-configured threshold.

[F2: System] ➔ [4: Application Parameter] ➔ [24: Force Control] ➔ [3: Force Control Options] ➔ **Select [Profile] Tab**

---

![](../_assets/_10_fctrl_ctrl_vel_clamp.png)

##### **[Key Configuration Items]**

| Configuration Item | Description |
| :--- | :--- |
| **Function Activation** | Specifies whether to use the function via the checkbox. |
| **Linear Velocity - Force Condition [% Target]** | Trigger condition for the linear velocity axes (X, Y, Z). When the current force reaches the set percentage (%) relative to the final target force configured in the [Settings] tab, the speed limit is executed immediately. |
| **Linear Velocity - Limit Ratio [% Limit Speed]** | Defines the attenuation ratio (%) to scale down the maximum limit speed per axis previously configured in the [Settings] tab, once the force condition is satisfied. |
| **Angular Velocity - Torque Condition [% Target]** | Trigger condition for the rotational axes (Rx, Ry, Rz). When the current torque reaches the set percentage (%) relative to the final target torque, the speed limit is executed. |
| **Angular Velocity - Limit Ratio [% Limit Speed]** | Defines the attenuation ratio (%) to scale down the maximum limit speed of the rotational axes previously configured in the [Settings] tab, once the torque condition is satisfied. |

![](../_assets/_14_fctrl_ctrl_vmax_clamp.png)


##### **[Understanding through Operation Example]**

* **Default Limit Speed:** `2.0 mm/s` (Set value in the [Settings] tab)
* **Final Target Force:** `10 N` (Set value in the [Settings] tab)
* **Force Condition [% Target]:** `50 %` (Triggers the function when reaching `5 N`, which is 50% of the final target)
* **Limit Ratio [% Limit Speed]:** `30 %` (Clamps downward to `0.6 mm/s`, which is `30%` of the existing speed limit)

---

###### **Step 1. Initial Entry and Force Trigger**
After the robot descends and makes contact with the object, the speed limit algorithm forcibly intervenes the moment the actual measured force data rises rapidly and surpasses the trigger reference point of **5 N**.

###### **Step 2. Velocity Clamping and Vibration Suppression**
Before the function is activated, the robot displays vibrations up to around the maximum Vmax of `2.0 mm/s` in order to track the target force. 

However, the moment the force condition is satisfied and the limit ratio is newly applied, the robot's operating speed is **powerfully clamped within the predefined limit line of `0.6 mm/s` (30% of the original limit)**. As a result, excessive behavior of the control system is restricted, and the force data below also stops vibrating and stably converges to the target value of 10 N.

---

{% hint style="info" %}

**On-Site Tuning Guide (Vibration Control):** Activate this function when initial contact vibrations (bouncing phenomena) cannot be resolved solely by adjusting response or damping. By **adjusting the [Limit Ratio] downward to an appropriate level**, the physical speed margin is restricted, allowing you to suppress vibrations effectively.

{% endhint %}

{% hint style="warning" %}

**Side Effects of Excessive Restriction:**
If the [Limit Ratio] is set too low (e.g., 5% or less), the vibration will be suppressed, but the robot will lack the speed required to push into the target force. 

{% endhint %}