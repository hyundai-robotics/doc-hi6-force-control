### 4.1 Basic Settings

This menu is used to configure the name according to the force control operation conditions, and to set the task coordinate system, tool number, and sensor zero point (offset) function that will serve as the control reference. 

The force control option condition settings can be accessed through the path below, and up to 15 conditions can be configured.

[F2: System] ➔ [4: Application Parameter] ➔ [24: Force Control] ➔ [3: Force Control Options] ➔ **Select [Settings] Tab**

---

![](../_assets/_06_fctrl_ctrl_cnd_default.png)

![](../_assets/_27_fctrl_option_basic_usr.png) 


##### **[Basic Configuration Items]**

| Item | Description |
| :--- | :--- |
| **Name** | The identification name of the force control condition. It is automatically entered when selected from the list on the right. (e.g., `cnd_1`) |
| **Description** | Enter the purpose or task description of the current control condition. (e.g., `Contact`, `Sanding`, etc.) |
| **Coordinate System** | Select the reference coordinate system to which the force control loop will be applied.<br>• **Base** <br>• **Robot** <br>• **Tool** <br>• **User** |
| **User Coord. No.** | Activated when the coordinate system is set to **[User]**, and designates the unique ID number of the user coordinate system to be applied. |
| **Tool No.** | Select the tool data number to be applied to the current control. (The weight and center of gravity information configured for the corresponding tool is linked to the control algorithm in real time) |
| **Zero Point** | Uses a toggle switch to set whether to force-cancel the initial offset of the sensor data when force control starts.<br>• **On (Enabled):** Resets the sensor value to 0 immediately before operation (Software Bias processing)<br>• **Off (Disabled):** Maintains the existing sensor data without any separate zero calibration |

---

{% hint style="info" %}

**Precautions for User Coordinate System Entry:** If the user coordinate system is selected but the number (ID) is left as **Unconfigured (None)**, it will be mapped and calculated identically to the **Robot Coordinate System**.

**Tool Number Integration:** The tool number (ID) selected here refers to the physical parameters of the tool data pre-registered in the `[F2: System] ➔ [4: Application Parameter] ➔ [24: Force Control] ➔ [2: Tool Data]` menu.

**Operation when Zero Point Function is Off:** If the zero point function is not used (Off), a statically calibrated value is utilized where the tool dead weight is canceled based solely on the tool data information (weight, center of gravity, force/torque zero) pre-mapped to the raw sensor output data.

{% endhint %}