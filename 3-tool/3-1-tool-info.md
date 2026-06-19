## 3.1 Tool Data Settings

This step improves the accuracy of the force control algorithm by registering the physical specifications and offset values of the tool mounted at the end of the robot flange. The force and torque recognized by the sensor are calibrated in real time according to the configured tool weight and center of gravity values.

The force control tool information settings can be accessed through the following path: 

[F2: System] - 4: Application Parameter - 24: Force Control - 2: Tool Data

---

![](../_assets/_04_fctrl_ctrl_tool_data.png)

##### **[UI Configuration and Status Display Items]**

| Item | Description |
|---|---|
| **Name** | Identification number and name of the tool data (Automatically entered) |
| **Description** | Description or purpose of the tool (Optional entry) |
| **Weight [kg]** | The actual weight of the mounted tool. Used as the reference value for gravity compensation during force error calculation. |
| **Center [X, Y, Z]** | The position of the tool center of gravity based on the F/T sensor coordinate system (Unit: mm) |
| **Force Zero [X, Y, Z]** | The zero reference value to cancel out the initial force offset of the sensor itself with the tool mounted (Unit: N) |
| **Torque Zero [X, Y, Z]** | The zero reference value to cancel out the initial torque offset of the sensor itself with the tool mounted (Unit: Nm) |
| **Sensor Coord.** | Definition of the direction of the sensor reference coordinate system |
| **Dynamic Load Identification** | A function to estimate the weight and center of gravity of the tool installed in front of the F/T sensor |

{% hint style="info" %}

- From version V70.02-00 and later, up to 4 sets of tool information can be configured. 
- The sensor-based load estimation function previously provided in Hi5a has been replaced by the "Dynamic Load Identification" function from version V70.02-00 and later. 

{% endhint %}