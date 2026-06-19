## 6.2 Force Motion Monitoring

This function allows you to comprehensively check the error and behavioral status of the real-time applied force data (F), the control command position (Cmd), and the configured speed limit value (Vmax) during force control operation.

--- 

![](../_assets/_17_fctrl_ctrl_panel_force_motion.png)

##### **Screen Configuration Items**

| Item Name | Description |
| :--- | :--- |
| **F** | The real-time target force. [Unit: N or Nm] |
| **Cmd** | The command position generated in real time by the system to track the force control. [Unit: mm or deg] |
| **Vmax** | The maximum limit speed profile data configured for system stability. [Unit: mm/s] |
| **TLT** | Monitors the **[Tilt Angle Threshold]** status among the contact conditions in real time. |
| **AVG** | Monitors the **[Angle Change Threshold]** status among the contact conditions in real time. |
| **HLD** | Monitors the **[Duration]** count value and retention status among the contact conditions. |

* **Coordinate System Reference:** The direction and axes of all monitored data are aligned based on the reference coordinate system designated in the force control condition settings (`cnd`).

* **Data Update Rule:** The data on this monitoring window updates in real time only when the force control operation command (`fctrl on`) is activated and the real-time control loop is running.

--- 

{% hint style="info" %}

**Teaching Pendant (TP) Navigation Path:** [Window Adjustment] ➔ [F1: Select] ➔ [Force Motion]

**On-Site Verification Tip:** If the robot's behavior is unstable during initial contact, check the `TLT`, `AVG`, and `HLD` status monitoring data on the right. If the `HLD` (duration) fails to reach the target value and resets after contact, it indicates that the `TLT` or `AVG` value is momentarily exceeding the threshold, causing the contact determination to be missed. In this case, the corresponding threshold conditions must be tuned.

{% endhint %}