### 2.4.1 Force Control Condition Setup - Basic

Select the axes to be controlled according to the task, and set the force target value, stiffness, speed, and pose limit for each axis.  
These items are the core of force control and determine the responsiveness of the actual robot movement.

<br>

---


![](../../_assets/_06_fctrl_ctrl_cnd_default.png)


#### **Default Configuration Items**

| Item | Description |
|------------------|------|
| **Name** | Condition name (e.g., cnd_12) - Automatically entered by selecting from the list |
| **Description** | Task description (e.g., Sanding) - Used to identify the purpose of the current condition |
| **Coordinate System (Crd)** | Select the coordinate system where force control will be applied:<br>• Base (Base Coordinates)<br>• Robot (Robot Coordinates)<br>• Tool (Tool Coordinates)<br>• User (User-defined Coordinates) |
| **User Coordinate System (UCS ID)** | User-defined coordinate system number - Used when Crd is set to User |
| **Tool ID** | Current tool number (Linked to tool weight and center of gravity information) |
| **Zeroing Function (Zeros)** | Force sensor initial value calibration (Zeroing)<br>• On: Execute zero calibration<br>• Off: Maintain original values |

<br> 

---

{% hint style="info" %}

- If a User Coordinate System is selected and a non-existent User Coordinate System ID is entered, an error (**E1336**) will be output during force control operation.

- If the User Coordinate System is selected and the ID is set to 0, it is identical to the Robot Coordinate System.

- The Tool ID refers to the tool number configured in:  
  **"[F2: System] – 4: Application Parameters – 17: Force Control – 2: Force Control Tool Data"**

- If the Zeroing function is not used (**Off**), the system outputs values calibrated based on the tool information (weight and center of gravity) assigned to the set tool number, relative to the raw output from the sensor.

{% endhint %}

<br> 

---

{% hint style="info" %}

#### **Default Item Configuration Example**

**Applied Task:** Sanding

- **Name**: cnd_12  
- **Description**: Sanding operation conditions  
- **Coordinate System (Crd)**: Select Tool Coordinate System  
- **Tool ID**: Use Force Control Tool Data ID 0 (Mass and Center of Gravity applied)  
- **Zeroing Function (Zeros)**: ON → Initializes the sensor value to 0 when force control starts 

{% endhint %}

---