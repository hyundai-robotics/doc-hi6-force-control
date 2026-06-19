### 4.5.1 Motion: Contact Conditions

This function detects and determines in real time whether the robot tool center point (TCP) has stably made contact with (settled onto) the surface of the task object during force control operation.

[F2: System] ➔ [4: Application Parameter] ➔ [24: Force Control] ➔ [3: Force Control Options] ➔ **Select [Motion] Tab**

---


![](../_assets/_12_fctrl_ctrl_cnd_motion_contact.png)


##### **[Key Configuration Items]**

The system determines the status as 'Contact Complete' only when all four conditions configured below are satisfied.

| Configuration Item | Description |
| :--- | :--- |
| **Force Threshold [N]** | The minimum applied force criterion required to acknowledge contact. |
| **Angle Change Threshold [deg]** | The allowable limit for the instantaneous change (variation width) in the direction of the force vector occurring at the moment of initial contact. |
| **Tilt Angle Threshold [deg]** | The allowable angular limit of the force vector to determine stable contact under the slope of the task surface or the tilted state of the tool. |
| **Duration [s]** | The minimum duration for which all three threshold conditions above (force, angle change, and tilt angle) must be continuously maintained. |

---

##### **[Configuration Example]** * **Operational Behavior:** If the conditions below are **simultaneously satisfied for 3 seconds**, it is finally determined that the tool has settled onto the contact surface.

| Configuration Item | UI Value | Behavior Determination Criterion |
| :--- | :--- | :--- |
| **Force Threshold** | `3 N` | When the external force detected by the F/T sensor reaches 3 N or higher |
| **Angle Change Threshold** | `10 deg` | When the instantaneous change in the force direction during contact stabilizes within 10° |
| **Tilt Angle Threshold** | `20 deg` | When the tilt trajectory of the force vector relative to the target angle is within 20° |
| **Duration** | `3 s` | When the above state is maintained for 3 seconds without interruption |

---

{% hint style="info" %}

**Coordinate System Configuration Rule:** Since the contact condition algorithm requires precise mapping of the tool's behavior direction and component forces, it operates normally only when the reference coordinate system is designated as the **Tool Coordinate System**.

**On-Site Tuning Tip:** If the robot pauses and fails to proceed to the next motion after making contact, it is highly likely due to the impact of the collision or surface irregularities. In this case, increasing the **[Angle Change Threshold]** and **[Tilt Angle Threshold]** by about 5° to 10° each will resolve the issue and allow normal operation.

{% endhint %}