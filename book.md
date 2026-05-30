
[__SOURCE](README.md)
# ${cont_model} Controller - Force Control with sensors Manual

[__SOURCE](0-about-this-manual/precautions.md)
# Precautions

{% include file="en/precautions.md" %}

[__SOURCE](1-intro/README.md)
# 1. Introduction

This manual provides instructions for using the sensor-based force control system.  
The system utilizes a force/torque sensor mounted on a robot to perform responsive control to external forces,  
enabling precise and safe contact operations.

--- 

### **Features Covered**

- Sensor environment configuration  
- Force control parameter setup  
- Command structure  
- Monitoring interface  
- Basic usage examples

--- 

### **Purpose**

This document is intended for end-users and maintenance engineers.  
It describes all necessary procedures for configuring the system and understanding its operational status.

This feature is available from version V60.32-01 and requires a separate functional license.
[__SOURCE](2-settings/README.md)
# 2. Configuration

To use the sensor-based force control functionality, the following basic components must be configured first.  
These settings are entered through the user interface (UI) and serve as the foundation for all control features.

- Force Sensor Coordinate System  
- Force Control Environment Setup  
- Force Control Tool Information  
- Force Control Conditions  

[__SOURCE](2-settings/1-force-sensor-coordinate-system.md)
## 2.1 Force Sensor Coordinate System

When mounting the force/torque (FT) sensor, the sensor coordinate system **must be aligned with the robot model's coordinate system**.

If the sensor frame is misaligned, the measured force/torque directions will not match reality, leading to **severely degraded control performance**.

<br>

---

### **Robot Sensor Coordinate Frame**

- The X, Y, and Z axes of the sensor coordinate system, as defined by our standard, are shown in the figure below:  
- The directions of the X, Y, and Z axes defined in the sensor model **must match** the robot's sensor coordinate system.

![](../_assets/_05_fctrl_ctrl_sensor_crd.png)

- The robot in the above diagram is in its default posture.  
- Most circular FT sensors have coordinate direction markings on the sensor body.  

<br>

---

{% hint style="info" %}

- **If the axes are inverted**: apply axis inversion or transformation in the software.
- **When entering the tool center of mass**: use the sensor's coordinate frame.
- **Before zeroing the sensor**: verify that the coordinate direction is correct.

{% endhint %}
[__SOURCE](2-settings/2-force-control-environment-settings.md)
## 2.2 Force Control Environment Setup

To use sensor-based force control functions, the following key items must be configured.  
These settings serve as the **starting point** for all controller operations. 

You can access the Force Control Environment Setup through the following path: 

`[F2: System] - 4: Application Parameters - 24: Force Control - 1: User Environment Setup`

<br>

---


### **Enable Function**

Set whether to use the sensor-based force control function.

- Enable: Function **Activated**
- Disable: Function **Deactivated**

The setting must be set to Enable for the force control function to operate.

<br>

---

### **Sensor Manufacturer and Model**

Select the **manufacturer and model of the force sensor** to be used.

- Examples:
  - ATI: Standard ATI models
  - ATI: Delta-SI-660-60
  - ATI: Theta-SI2500-400
  - ATI: Omega-SI7200-1400 
  - OnRobot: HEX-E 
  - Robotiq: FT-300S 

The **data format and communication method** vary depending on the sensor, so an accurate selection is required.

{% hint style="info" %}

The following ATI models are supported in **version V60.32-05 or later**.  
- Standard ATI models  
- Theta-SI2500-400  
- Omega-SI7200-1400

{% endhint %}

<br>

--- 

### **Communication Protocol**

Set the **communication method** provided by the selected sensor.

- UDP
- SCI
- TCP

Configure the port settings and internal parsing methods according to the protocol as follows:

<br>

--- 

### **Configuration Method by ATI Model**

- **Communication Protocol**: UDP
- **IP Address**: 192.168.1.2
- **Remote Port**: 49152

<br>

#### **ATI(Delta-SI-660-60)**  

![](../_assets/_01_01_fctrl_env_setting_ATI_Delta_UDP.png)

<br>

#### **ATI(Theta-SI2500-400)**
![](../_assets/_01_02_fctrl_env_setting_ATI_Theta_UDP.png)

<br>

#### **ATI(Omega-SI7200-1400)**
![](../_assets/_01_03_fctrl_env_setting_ATI_Omega_UDP.png)

<br>

#### **ATI(Generic ATI Model)**
![](../_assets/_01_04_fctrl_env_setting_ATI_Generic_UDP.png)

- Instead of registering models individually, this method involves the **user manually entering and applying the scaling values provided by ATI for each specific model.**

<br>

---

### **OnRobot HEX-E Configuration Method**

- **Communication Protocol**: UDP
- **IP Address**: 192.168.1.1
- **Remote Port**: 49152

![](../_assets/_02_fctrl_env_setting_OnRobot_HEX_E_UDP.png)


<br>


---

### **SCI Communication Method: Robotiq(FT-300S)**
![](../_assets/_03_01_fctrl_env_setting_Robotiq_FT300S_SCI.png)

`[F2: System] - 2: Control Parameters - 3: Serial Port - 1: Configuration`

![](../_assets/_03_02_fctrl_env_setting_Robotiq_FT300S_SCI_CFG.png)

<br>


---


{% hint style="info" %}
 
- These settings are examples based on standard models.  
- **Some ATI models may use network values that differ from the settings above.**

{% endhint %}


[__SOURCE](2-settings/3-tool-information-settings-for-force-control.md)
## 2.3 Force Control Tool Information

By entering the physical characteristics of the tool mounted on the robot, the accuracy of the force control algorithm is improved.  
The force and torque perceived by the sensor are calibrated based on the tool's weight and center of gravity coordinates. 

The Force Control Tool Information setup can be accessed through the following path: 

`[F2: System] - 4: Application Parameters - 24: Force Control - 2: Force Control Tool Data`

<br>

---

![](../_assets/_04_fctrl_ctrl_tool_data.png)

| Item | Description |
|--------------|------|
| **Name** | Tool data name (Automatically entered) |
| **Description** | Tool description or purpose (Optional entry) |
| **Weight [kg]** | Weight of the tool. Used for gravity compensation when calculating force errors. |
| **Center [X, Y, Z]** | Position of the tool's center of gravity (Based on the sensor, Unit: mm) |
| **Sensor coordinate** | Direction of the sensor reference coordinate system (Refer to the image on the right of the UI) |


{% hint style="info" %}

 - Up to 10 sets of tool information can be configured. 
 - The sensor-based load estimation function provided in Hi5a is currently not supported. 

{% endhint %}
[__SOURCE](2-settings/4-condition-settings/README.md)
## 2.4 Force Control Condition Settings

To use the force control function effectively, it is essential to configure the control conditions properly based on the task requirements,  
including target force, control direction, and sensitivity.

These settings determine how the robot responds to external forces and directly affect the quality of the task.

Access the force control condition settings via:

`[F2: System] - 4: Application Parameters - 24: Force Control - 3: Force Control Option`
[__SOURCE](2-settings/4-condition-settings/1-basic.md)
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
  `[F2: System] - 4: Application Parameters - 24: Force Control - 2: Force Control Tool Data`

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
[__SOURCE](2-settings/4-condition-settings/2-control.md)
### 2.4.2 Force Control Condition Setup - Control

Select the force control axes and set the target force value, stiffness, speed, and pose limit for each direction.

This section is the core of force control and determines the responsiveness of the actual robot movement.

<br>

---

![](../../_assets/_07_fctrl_ctrl_cnd_control.png)


#### **Control Configuration Items**

| Item | Description |
|------------|------|
| **Axis** | Controllable axes (X, Y, Z, Rx, Ry, Rz) |
| **Act** | Whether to activate control for the corresponding axis (Active when checked ✓) |
| **Force / Torque** | Target Force (N) or Torque (Nm)<br>Example: Set 50N for the Z-axis |
| **Stiff** | Stiffness ratio (%), lower values allow more flexible response |
| **Vel** | Movement speed limit during force control (mm/s or deg/s) |
| **(-)Pose / (+)Pose** | Position limits in negative/positive directions (mm or deg)<br>Restricts robot movement when exceeded |

<br>

---

#### **Control Configuration Example**

The following settings are for a **vertical sanding** operation:

| Axis | Act | Force / Torque | Stiff | Vel | Pose Limit |
|------|------|----|------|------|-------------|
| **Z** | ✓ | 50N | 30% | 20 mm/s | -50 ~ +50 mm |
| **Rx** | ✓ | 0 Nm | 10% | 5 deg/s | -10 ~ +10 deg |
| **Ry** | ✓ | 0 Nm | 10% | 5 deg/s | -10 ~ +10 deg |
| **X**, **Y**, **Rz** | - | - | - | - | - | 

→ The robot maintains a force of 50N in the Z-axis direction, while the tool rotation directions (Rx, Ry) respond flexibly.

<br> 

---


{% hint style="info" %}


Detailed control for each axis must be adjusted based on actual working conditions (e.g., surface curvature, precision requirements, etc.). Lower gains result in a more flexible response.

While lower stiffness ratios provide a flexible response, they may cause vibration and noise depending on the robot's responsiveness and the surrounding environment.

{% endhint %}


[__SOURCE](2-settings/4-condition-settings/3-filtering.md)
### 2.4.3 Force Control Condition Setup - Filtering

Filtering functions are provided to reduce noise from the force sensor and ensure that input values can be used stably for control.

Additionally, it offers scaling options to adjust control intensity within a specific force/torque range, as well as a bypass option to make the response to force input more sensitive.

<br>

---

![](../../_assets/_08_fctrl_ctrl_cnd_filtering_smooth_force.png)

#### **Force Filtering**

Applies a **filter** to the sensor's force signals to eliminate jitter and smooth the output.

| Item | Description |
|------|------|
| **Enable** | Apply filter when checked |
| **Frequency (Freq)** | Set the filter cutoff frequency (e.g., 20 Hz)<br>→ Lower values result in smoother motion but slower response. |

<br>

---

![](../../_assets/_09_fctrl_ctrl_cnd_filtering_smooth_scaling.png)


#### **Force Scaling**

This function smoothly scales the control intensity within a specific force or torque range.  
It is useful for tasks requiring sensitivity adjustments and is typically kept off.

It can be designed to suppress control for minute force changes and respond sensitively only to forces above a certain level.

| Item | Description |
|------|------|
| **Enable** | When checked, scaling is applied only within the ranges below |
| **Force Range** | Force range (e.g., 2 ~ 8 N) |
| **Torque Range** | Torque range (e.g., 0 ~ 0 Nm) |

![](../../_assets/_11_fctrl_ctrl_cnd_filtering_scaling_graph.png)

{% hint style="info" %}

- When entering the force range, if the input force is smaller than the **Start Force**, the output force is 0. If it is greater than the **End Force**, the original input force value is output.

- If the **Start Force** and **End Force** are equal, the scaling function will not operate.

{% endhint %}

<br>

--- 


![](../../_assets/_10_fctrl_ctrl_cnd_filtering_cmd_flow.png)

#### **Command Method**

Sets the **processing method** for the command signals transmitted to the robot.

| Item | Description |
|------|------|
| **Mode** | **Normal**: Standard command transmission method. <br>**Bypass**: Command transmission method for highly sensitive responses. |
| **Freq** | Filter frequency setting used in Bypass mode (Hz). |

{% hint style="info" %}

- **Bypass** mode is used when you want to **reflect sensor data immediately**.
- It is recommended only for experimental situations requiring extremely sensitive control.
- Since there is a **risk of noise or vibration**, it is recommended to use **Normal** mode for general operations.

{% endhint %}

<br> 

--- 

### **Configuration Guide**

| Task Type | Recommended Settings |
|------------------|-----------------------------|
| Polishing / Sanding | Smooth Force = ON, Freq = 20 Hz |
| Smooth Assembly | Smooth Scaling = ON, Conservative range setting |
| High-speed Response / Research | Command Flow = Bypass |

--- 

{% hint style="info" %}

- **Filtering**, **Scaling**, and **Command Flow** settings all work together; therefore, they must be **tuned integrally** according to the specific objective of the task.

{% endhint %}

[__SOURCE](2-settings/4-condition-settings/4-motion/README.md)
### 2.4.4 Force Control Condition - Motion

During force control operations, motion-related conditions can also be configured.

You can define a **surface contact detection** criterion to determine whether the tool has made full contact with the surface, based on tool orientation.  

Additionally, without using a separate `move` command, the system can automatically generate **spiral**, **bidirectional**, or **zigzag** trajectories  

[__SOURCE](2-settings/4-condition-settings/4-motion/1-contact.md)
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


[__SOURCE](2-settings/4-condition-settings/4-motion/2-raster.md)
#### 2.4.4.2 Force Control Condition Setup - Motion - Auto Path Generation

Sets the motion control conditions to be executed during force control operations.

This section is specifically used to configure **Spiral, Bi-directional, and Zig-zag** paths and trajectories.


<br>

---



![](../../../_assets/_13_fctrl_ctrl_cnd_motion_raster1.png)

![](../../../_assets/_15_fctrl_ctrl_cnd_motion_raster3.png)


### **Motion Types**

| Item |
|----------------|
| **Spiral Motion** |
| **Bi-directional Motion** |
| **Zig-zag Motion** |

<br>

---

![](../../../_assets/_14_fctrl_ctrl_cnd_motion_raster2.png)

### **Spiral Motion**

A function that generates a spiral path and trajectory.

| Item | Description |
|--------------|------|
| **Velocity** | Rotational linear velocity (mm/s) |
| **Radius** | Maximum radius setting (mm) - The final size of the spiral |
| **Revolutions** | Number of revolutions (rev) - Total count of rotations |


<br>

---


### **Bi-directional Motion**

A function that generates a bi-directional path and trajectory.

| Item | Description |
|--------------|------|
| **Velocity** | Linear velocity (mm/s) |
| **Mov Dir** | Movement Direction (+X, -X, +Y, -Y) |
| **Mov Length** | Movement Length (mm) |
| **Shift Dir** | Shift Direction (+X, -X, +Y, -Y) |
| **Shift Length** | Shift (Pitch) Length (mm) |
| **Num Lines** | Number of lines to be generated in the movement direction |

<br>

---

### **Zig-zag Motion**

A function that generates a zig-zag path and trajectory.

| Item | Description |
|--------------|------|
| **Velocity** | Linear velocity (mm/s) |
| **Mov Dir** | Movement Direction (+X, -X, +Y, -Y) |
| **Mov Length** | Movement Length (mm) |
| **Shift Dir** | Shift Direction (+X, -X, +Y, -Y) |
| **Shift Length** | Shift (Pitch) Length (mm) |
| **Num Lines** | Number of lines to be generated relative to the movement direction |

<br>

---

{% hint style="info" %}

- This motion generates a path based on the **XY plane** relative to the coordinate system selected in **2.4.1 (Force Control Condition Setup - Basic)**.

{% endhint %}
[__SOURCE](3-roblang/README.md)
# 3. Force Control Commands

This section provides an overview of the main commands related to the force control feature.  
Each command is used to configure force settings, start/stop control, and execute motions like spiral, bidirectional anc zig-zag movement.

<br>

---

### List of Force Control Commands

| Command               | Description                              | Argument                | Note                     |
|------------------------|------------------------------------------|--------------------------|--------------------------|
| `fctrl on, cnd=`       | Start force control with given condition | `cnd=condition number`   | Required to start control |
| `fctrl control, cnd=`  | Change control condition only            | `cnd=condition number`   | Changes only control set during operation |
| `fctrl off`            | Stop force control                       | None                     | -                        |
| `fctrl motion_on`      | Start raster motion                      | None                     | Uses preset raster motion |
| `fctrl motion_off`     | Stop raster motion                       | None                     | Stops immediately        |
| `motion_state()`         | Check raster motion status               | None                     | -                        |
| `contact_state()`         | Check contact status               | None                     | -                        |
| `cfo(crd, type)` | Retrieves current FT sensor data | `crd`: coordinate frame defined in cnd<br>`type`: must be `"sensor"` | If the coordinate frame does not match the one configured in cnd, values will not update. The type parameter must be `"sensor"` to acquire FT sensor data. |

<br>

[__SOURCE](3-roblang/1-example-2-axis-directional-force-control.md)
## 3.1 Example: Z-axis Force Control

The following is an example of a Job program using the **Sensor-based Force Control function**.
This example is designed to wait until the **external force applied in the Z-axis direction reaches 35N or more** before performing the task.

<br>

---

### **Operation Overview**

- By using a **delay** command to secure time before starting force control, you can suppress sensor noise or initial vibrations, enabling more stable force control.

- When selecting a coordinate system in the **CFO (Force Control Output)** command, it must match the coordinate system selected in the **Force Control Settings** to properly receive force data.

<br>

---

### **JOB Program Example**

```python
delay 1.0                           # Wait for stabilization before starting control
fctrl on,cnd=2                      # Start force control (Using condition set No. 2)
delay 0.5

#get_current_force
var force = cfo("tool", "sensor")   # Receive external force data based on the Tool coordinates

# Conditional Loop: Wait until the Z-axis external force reaches 35N or more
if abs(force.z) < 35 then *get_current_force
delay 5                             # Wait for external force stabilization 
fctrl off                           # End force control 
[__SOURCE](3-roblang/2-example-change-control-settings.md)
## 3.2 Example: Modifying Control Settings

The following is a Job program example for **modifying only the 'Control' parameters** within the force control conditions.  
This method is useful when you want to change only the external force response characteristics during real-time operation while maintaining other settings such as filters, coordinate systems, and motion profiles.

<br>

---

### **Operation Overview**

- **fctrl on, cnd=2**: Applies the complete configuration from set No. 2 when starting force control.
- **fctrl control, cnd=1**: Changes **only the 'Control' parameters** to those of set No. 1.
  (Other settings such as coordinate system, filters, and motion profiles remain as they were in set No. 2.)

<br>

---

### **JOB Program Example**

```python
delay 1.0                           # Wait for stabilization before starting control
fctrl on, cnd=2                     # Start force control (Initial: Using set No. 2)
delay 0.5

fctrl control, cnd=1                # Update ONLY 'Control' parameters (Switch to set No. 1)
                                    # (Coordinates, Filters, and Motion remain from No. 2)

delay 5                             # Wait for stabilization of external force
fctrl off                           # End force control

[__SOURCE](3-roblang/3-example-motion-contact.md)
## 3.3 Example: Contact Surface Detection

The following is a Job program example for using the **Contact Surface Detection** function in the robot. 

<br>

---

### **Operation Overview**

Configure the **Contact Check** conditions in the **Settings** as follows:

- **Criteria**: If contact is maintained according to the standards below for 5 seconds, the contact surface detection is confirmed (OK).

| Item | Value |
|------------------|---------|
| Force Error (Thresh) | 3 N |
| Force Direction Change (Dev Angle) | 20 deg |
| Contact Angle (Tilt Angle) | 40 deg |
| Confirmation Time | 5 sec |

<br> 

---

### **JOB Program Example** 

```python
delay 1.0                           # Wait for stabilization before starting control
fctrl on, cnd=1                     # Start force control (Using condition set No. 1)
delay 0.5                           # Wait 0.5s before executing contact detection

wait contact_state()                # Execute contact detection; wait until "OK"

fctrl off                           # End force control


[__SOURCE](3-roblang/4-example-motion-spiral.md)
## 3.4 Example: Spiral Motion

This is a Job program example that uses the **Spiral Motion** feature in the robotic force control system.  
The robot maintains a constant **external force of 20N in the Z-axis direction** while performing the spiral path.

<br>

---

### **Operation Overview**

- Make sure to set the **Motion Type** to **Spiral** in the **configuration settings**.

- It is recommended to insert a **delay** command before **fctrl motion_on** to suppress vibration and ensure more stable force control.

<br>

---

### **JOB Program Example** 

```python
delay 1.0                            # Wait to stabilize before starting control
fctrl on,cnd=1                       # Start force control (using condition set No. 1)
delay 0.5                            # Wait before starting spiral motion

fctrl motion_on                      # Start spiral motion
wait motion_state() == 0             # Wait until spiral motion is complete
fctrl motion_off                     # Stop spiral motion

fctrl off                            # Stop force control

[__SOURCE](4-monitoring/README.md)
# 4. Monitoring

While the sensor-based force control function is active,  
users can monitor the following status information in real-time through the UI.

[__SOURCE](4-monitoring/1-force-data-monitoring.md)
## 4.1 Force Data Monitoring

This function allows you to monitor the external force applied to the robot in real time.  
It is essential to check this information when using the Force Control function.

<br>

---

![](../_assets/_16_fctrl_ctrl_panel_force_data.png)

| Item         | Description |
|--------------|-------------|
| **Cartesian** | External force (N or Nm) displayed in the selected coordinate system |
| **Joint**     | Not used in force control |

- The coordinate system of the Cartesian external force follows the coordinate frame defined in the force control condition (cnd).
- Data is updated **only when force control (fctrl) is active**.

<br>

--- 

{% hint style="info" %}

**TP Navigation Path**

[pane layout] - [F1: select] - [force data]

{% endhint %}
[__SOURCE](4-monitoring/2-force-motion-monitoring.md)
## 4.2 Force Motion Monitoring

This function allows for real-time monitoring of the external forces applied to the robot, the error relative to the target force, and the commanded position during operation.

<br>

--- 

![](../_assets/_17_fctrl_ctrl_panel_force_motion.png)

| Item | Description |
|--------------|------|
| **Fext** | Force Error (Error between target force and external force) [N or Nm] |
| **Cmd** | Command Position for force control (mm or deg) |

- The coordinate system for **Fext** and **Cmd** follows the coordinate system selected in the settings (cnd).
- This data is only active while **fctrl on** is in effect.

<br>

--- 

{% hint style="info" %}

**TP Navigation Path**

[pane layout] - [F1: select] - [force motion]

{% endhint %}
[__SOURCE](5-error/README.md)
# 5. Errors & Troubleshooting

During force control operation with an external FT sensor,  
the user can monitor the **status and exception events** in real time via the UI.

---

### Force Control Exception Events & Corrective Actions

| Error Code | Primary Cause | Guide |
|:--:|---|---|
| E0260 | Force control disabled | Enable force control in the configuration |
| E0353 | Invalid force control tool number | Configure a valid tool number for force control |
| E1336 | Invalid user coordinate frame number | Configure or add a valid user coordinate frame |
| E0259 | FT sensor communication issue | Check sensor and cable connections |
| E0272 | Unsupported FT sensor | Contact customer support (sensor interface required) |
| E0273 | FT sensor communication issue | Check sensor and cable connections |
| E0274 | FT sensor communication issue | Check sensor and cable connections |

> In all exception cases, the system performs a **temporary Safe-Stop** operation as the highest priority.

---

### Troubleshooting Workflow

1. Check the FT sensor connection  
2. Verify the tool number and coordinate frame  
3. Confirm whether the sensor is supported  
4. Review and back up logs  

---
