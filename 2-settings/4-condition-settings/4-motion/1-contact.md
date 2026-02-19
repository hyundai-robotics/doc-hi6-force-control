#### 2.4.4.1 Force Control Condition Setup - Motion - Contact Detection

This function determines in real-time whether the robot has properly made contact with the surface during a force control operation (in the Tool Z direction).



<br>

---




![](../../../_assets/_12_fctrl_ctrl_cnd_motion_contact.png)


<br>

---

### **Contact Surface Detection Criteria Setup**

Contact is determined to be complete when all of the following conditions are met:

| Item | Description |
|--------------|------|
| **Force Thresh** | Error threshold between the target force and current force (Unit: N) |
| **Dev Angle Thresh** | Instantaneous change in the direction of the Z-axis force relative to the tool coordinates (Unit: deg) |
| **Tilt Angle Thresh** | Angle between the contact surface and the direction of the force (Unit: deg) |
| **Confirm time** | Duration the conditions must be maintained (Unit: sec) |

<br>

---

### **Configuration Example**

- **Criteria**: If contact is maintained according to the following standards for 3 seconds, the contact surface detection is confirmed (OK).

| Item | Value |
|------------------|---------|
| Force Error (Thresh) | 3 N |
| Force Direction Change (Dev Angle) | 20 deg |
| Contact Angle (Tilt Angle) | 30 deg |
| Confirmation Time | 3 sec |

<br>

---

{% hint style="info" %}

- To ensure the **Contact Surface Detection** function operates correctly, the selected coordinate system must be set to the **Tool Coordinate System**.

{% endhint %}

