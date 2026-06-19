## 6.1 Force Data Monitoring

This function allows for real-time monitoring of external forces and torque data applied to the robot during operation. It must be referenced to verify the precise application status when the force control function is running.

--- 

![](../_assets/_16_fctrl_ctrl_panel_force_data.png)

##### **Screen Configuration Items**

| Item Name | Description |
| :--- | :--- |
| **Cartesian Coordinates (X, Y, Z, RX, RY, RZ)** | The 3-axis directional forces (N) and 3-axis rotational torque (Nm) values acting on the robot end-effector within the selected reference coordinate system. |
| **Joint Coordinates (J1, J2, J3, J4, J5, J6)** | This item monitors the physical load status applied to each individual joint axis (Joint 1 to Joint 6) of the robot, converted in real time. |

* **Coordinate System Reference:** The direction and reference axes of the [Cartesian Coordinates] data follow and match the reference coordinate system designated by the user in the force control condition settings (`cnd`) menu.

* **Data Update Rule:** The data on this monitoring window updates in real time only when the force control operation command (`fctrl on`) is activated and the control loop is running.


--- 

{% hint style="info" %}

**Teaching Pendant (TP) Navigation Path:** [Window Adjustment] ➔ [F1: Select] ➔ [Force Data]

**On-Site Verification Tip:** If the data is not near `0.000` while the robot is stationary, verify the dead weight compensation (Gravity Compensation) or the sensor zero setting (Zeroing).

**Output Criteria:** During force control operation, F/T sensor data is output in real time exclusively to the **[Cartesian Coordinates]** item, while the **[Joint Coordinates]** item remains fixed at `0.0`.

{% endhint %}