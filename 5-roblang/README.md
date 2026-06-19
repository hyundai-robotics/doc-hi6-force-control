# 5. Commands

This document provides descriptions of the major system commands and status variables (system variables) related to the force control function. Each command is used for force control configuration, motion control, status verification, and receiving F/T sensor data.

---

##### **1. Commands (Version V70.02-00 or Later)**

In versions V70.02-00 and later, a standardized format is used where execution commands (`fctrl`) and built-in status variables (`_fctrl`) are separated for clear distinction.

##### **[Commands]**

| Command | Description | Argument | Remarks |
| :--- | :--- | :--- | :--- |
| `fctrl on, cnd=` | Starts force control operation and applies the designated control condition. | `cnd=Condition Number` (e.g., `cnd=1`) | Mandatory execution when starting force control |
| `fctrl control, cnd=` | Modifies only the control parameter conditions in real time while maintaining the force control operation. | `cnd=Condition Number` (e.g., `cnd=2`) | Used to switch control conditions without stopping motion |
| `fctrl off` | Safely terminates force control operation and returns to normal position control. | None | - |
| `fctrl motion_on` | Starts the designated automatic path generation motion (Spiral, Bidir, Unidir). | None | Only valid while `fctrl on` is active |
| `fctrl motion_off` | Immediately stops the automatic path generation motion currently running. | None | The force control (`fctrl on`) state is maintained |

{% hint style="info" %}

**`fctrl control` Changeable Parameters (Specifications):** When switching conditions in real time using this command, only the control conditions (selected axes, activation status, target force, responsiveness, damping gain, limit speed, and $\pm$ position limit ranges) can be changed. The reference coordinate system, tool number, and filtering/profile/motion settings do not change and maintain the configuration previously set by (`fctrl on, cnd`).

{% endhint %}

##### **[Monitoring-Related System Variables]**

| System Variable | Description | Data Type | Remarks |
| :--- | :--- | :--- | :--- |
| `_fctrl.motion` | Returns the current operation status of the automatic path generation motion. | (0: In operation, 1: Motion complete) | Used to check motion operation status (e.g., `wait _fctrl.motion==0`) |
| `_fctrl.contact` | Returns the current contact determination status with the surface of the task object. | (0: No contact, 1: Contact complete) | Used to verify if contact conditions are satisfied (e.g., `wait _fctrl.contact`) |
| `_fctrl.force_x` | Receives the force along the X-axis direction based on the tool coordinate system currently being measured by the F/T sensor. | (Unit: N) | - |
| `_fctrl.force_y` | Receives the force along the Y-axis direction based on the tool coordinate system currently being measured by the F/T sensor. | (Unit: N) | - |
| `_fctrl.force_z` | Receives the force along the Z-axis direction based on the tool coordinate system currently being measured by the F/T sensor. | (Unit: N) | Primary variable for monitoring the pressurizing control axis |
| `_fctrl.torque_rx` | Receives the rotational torque about the X-axis based on the tool coordinate system currently being measured by the F/T sensor. | (Unit: Nm) | - |
| `_fctrl.torque_ry` | Receives the rotational torque about the Y-axis based on the tool coordinate system currently being measured by the F/T sensor. | (Unit: Nm) | - |
| `_fctrl.torque_rz` | Receives the rotational torque about the Z-axis based on the tool coordinate system currently being measured by the F/T sensor. | (Unit: Nm) | - |


---

##### **2. Commands (Below Version V70.02-00)**

In controller units and legacy program codes below version V70.02-00, the following global variable and built-in function standards are used. Please pay close attention during maintenance.

| Command / Function | Description | Arguments and Specific Rules | Remarks |
| :--- | :--- | :--- | :--- |
| `motion_state` | Returns the current operation status of the automatic path generation motion. | None | Identical to `_fctrl.motion` in version V70.02-00 |
| `contact_state` | Returns the current contact determination status with the surface of the task object. | None | Identical to `_fctrl.contact` in version V70.02-00 |


---

##### **3. F/T Sensor Value Reception Function**

This data reception function is compatible across all software versions.

| Command / Function | Description | Arguments and Specific Rules | Remarks |
| :--- | :--- | :--- | :--- |
| `cfo(crd, type)` | Receives F/T sensor data based on the designated coordinate system. | `crd` : Reference coordinate system number configured in the force control condition (cnd)<br>`type` : Fixed to `"sensor"` | Refer to the precautions below |


---

{% hint style="info" %}

**Precautions for Using `cfo()`:** If the entered coordinate system (`crd`) differs from the reference coordinate system of the currently applied force control condition (`cnd`), the data will not update. To receive data in real time, the `type` argument must be entered in lowercase as `"sensor"`.

**Recommendation:** It is highly recommended to use the dedicated system variables for **versions V70.02-00 and later (`_fctrl.force_x`, etc.)**, which eliminate the risk of argument matching errors.

{% endhint %}