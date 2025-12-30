# ${cont_model} Robot Controller – Force Control with sensors Manual

The information provided in this manual is the intellectual property of HD Hyundai Robotics.

No part of this document may be reproduced, distributed, or disclosed to third parties in any form without the prior written consent of HD Hyundai Robotics. Use of the contents for any purpose other than its intended use is strictly prohibited.

This manual is subject to change without prior notice.

<br><br><br><br>

**Copyright ⓒ 2025 by HD Hyundai Robotics**
# 🧩 1. Introduction

This manual provides instructions for using the sensor-based force control system.  
The system utilizes a force/torque sensor mounted on a robot to perform responsive control to external forces,  
enabling precise and safe contact operations.

## Features Covered

- Sensor environment configuration  
- Force control parameter setup  
- Command structure  
- Monitoring interface  
- Basic usage examples

## Purpose

This document is intended for end-users and maintenance engineers.  
It describes all necessary procedures for configuring the system and understanding its operational status.

This feature is available from version V60.32-01 and requires a separate functional license.# 🧩 2. Configuration

To use the sensor-based force control functionality, the following basic components must be configured first.  
These settings are entered through the user interface (UI) and serve as the foundation for all control features.

- Force Sensor Coordinate System  
- Force Control Environment Setup  
- Force Control Tool Information  
- Force Control Conditions  
## 🧩 2.1 Force Sensor Coordinate System

When mounting the force/torque (FT) sensor, the sensor coordinate system **must be aligned with the robot model's coordinate system**.

If the sensor frame is misaligned, the measured force/torque directions will not match reality, leading to **severely degraded control performance**.

<br>

---

### **Robot Sensor Coordinate Frame**

> The X, Y, and Z axes of the sensor coordinate system, as defined by our standard, are shown in the figure below:  
>
> The directions of the X, Y, and Z axes defined in the sensor model **must match** the robot’s sensor coordinate system.

![](../_assets/_05_fctrl_ctrl_sensor_crd.png)

⚠️ The robot in the above diagram is in its default posture.  
⚠️ Most circular FT sensors have coordinate direction markings on the sensor body.  

<br>

### 💡 Configuration Tips

- **If the axes are inverted**: apply axis inversion or transformation in the software.
- **When entering the tool center of mass**: use the sensor's coordinate frame.
- **Before zeroing the sensor**: verify that the coordinate direction is correct.

---## 🧩 2.2 Force Control Environment Setup

To enable sensor-based force control, the following key parameters must be configured.  
These parameters serve as the **starting point** for all force control operations.

Access the force control environment settings via:

📂 System → ⚙️ 4: Application Parameters → 💪 17: Force Control → 🛠 1: Environment Settings

<br>

---

### ✅ **Function Use**

Enable or disable the force control functionality.

- `Enable`: Activate the function  
- `Disable`: Deactivate the function

> ⚠️ The function must be set to **Enable** for force control to operate.

---

### ✅ **Sensor Type**

Select the **manufacturer and model** of the force sensor to be used.

- Examples:
  - `ATI : Delta-SI-660-60`  
  - `OnRobot : HEX-E`  
  - `Robotiq : FT-300S`  

The **data format and communication method** vary by sensor, so selection must be accurate.

> 💡 Sensor names are provided via a predefined list in the user interface.

---

### ✅ **Comm. Protocol**

Configure the **communication protocol** supported by the selected sensor.

- `UDP`  
- `SCI`  
- `TCP`  

⚙️ Port numbers and internal parsing methods differ based on the selected protocol.

---

### ✅ **UDP Protocol: OnRobot (HEX-E)**

![](../_assets/_01_fctrl_env_setting_udp.png)

---

### ✅ **UDP 통신 방식 : ATI(Delta-SI-660-60)**
![](../_assets/_18_fctrl_env_setting_ATI_udp.png)

- The IP address and remote port number may vary depending on the ATI sensor model. Please verify before entering the values.

- **Delta-SI-660-60** model
  - IP Address: 192.168.1.2  
  - Remote Port: 49152
---

### ✅ **SCI 통신 방식 : Robotiq(FT-300S)**

![](../_assets/_02_fctrl_env_setting_sci.png)

<br>

📂 System → 🔧 2: Control Parameters → 🔌 3: Serial Port → 🛠 1: Environment Settings

![](../_assets/_03_fctrl_ctrl_para_sci.png)

<br>

> 💡 Make sure to correctly configure **Function Use**, **Sensor Type**, **Comm. Protocol**, and **IP address** for proper sensor operation.
## 🧩 2.3 Tool Data for Force Control

Entering the physical properties of the tool mounted on the robot improves the accuracy of the force control algorithm.  
The force and torque measured by the sensor are compensated based on the tool's weight and center of mass.

Access the tool data settings via:

📂 System → ⚙️ 4: Application Parameters → 💪 17: Force Control → 🧰 2: Tool Data Settings

<br>

---

![](../_assets/_04_fctrl_ctrl_tool_data.png)

| Item                | Description |
|---------------------|-------------|
| **Name**            | Tool data name (auto-generated) |
| **Description**     | Optional description or purpose of the tool |
| **Weight [kg]**     | Weight of the tool. Used for gravity compensation in force correction |
| **Center [X, Y, Z]**| Center of mass position (relative to the sensor frame, in mm) |
| **Sensor coordinate** | Sensor coordinate system direction (refer to the image on the right in the UI) |

> 💡 Up to 10 tool data entries can be configured.

> 💡 The sensor-based load estimation function available on Hi5a is not supported on this system.
## 🧩 2.4 Force Control Condition Settings

To use the force control function effectively, it is essential to configure the control conditions properly based on the task requirements,  
including target force, control direction, and sensitivity.

These settings determine how the robot responds to external forces and directly affect the quality of the task.

Access the force control condition settings via:

📂 System → ⚙️ 4: Application Parameters → 💪 17: Force Control → 🎛 4: Condition Settings
## 🧩 2.4.2 Force Control Condition – Default Settings

Depending on the task, select the control axes and configure the target force, stiffness, velocity, and pose limits for each axis.  
These parameters form the core of the force control system and determine the robot’s responsiveness during operation.

<br>

---

![](../_assets/_06_fctrl_ctrl_cnd_default.png)

<br>

### ✅ **Default Setting Items**

| Item                | Description |
|---------------------|-------------|
| **Name**            | Condition name (e.g., `cnd_12`) – auto-filled upon selection from the list |
| **Description**     | Task description (e.g., `Sanding`) – used to distinguish the condition’s purpose |
| **Coordinate (Crd)**| Coordinate system to apply force control:<br>• `Base`<br>• `Robot`<br>• `Tool`<br>• `User` |
| **User Coordinate (UCS ID)** | User-defined coordinate system ID – required if `User` is selected for Crd |
| **Tool Coordinate (Tool ID)** | Tool number currently in use (linked with weight and center info) |
| **Zeroing (Zeros)** | Zero-offset calibration for the force sensor:<br>• `On`: Perform zeroing<br>• `Off`: Retain original values |

> 💡 If `User` is selected and the specified coordinate ID does not exist, an error (E1336) will occur during force control execution.  
> 💡 If `User` is selected and the coordinate ID is set to `0`, the robot coordinate frame is used instead.  
> 💡 The Tool ID refers to the tool number configured under:<br>📂 System → ⚙️ 4: Application Parameters → 💪 17: Force Control → 🧰 2: Tool Data Settings  
> 💡 If zeroing is disabled (`Off`), the output is compensated using the selected tool’s weight and center of mass.

<br>

### ✅ Example: Default Condition Setup

> Example: `Condition for Sanding Task`
>
> - **Name**: `cnd_12`  
> - **Description**: `Sanding`  
> - **Coordinate (Crd)**: Select `Tool` coordinate system  
> - **Tool Coordinate (Tool ID)**: Use Tool ID `0` (includes mass and center of mass)  
> - **Zeroing (Zeros)**: `ON` – Use sensor data initialized to zero at the start of force control  
## 🧩 2.4.2 Force Control Condition – Control Parameters

Select the axes to be used for force control, and configure the target force (or torque), stiffness, velocity, and pose limits for each direction.

These settings are central to force control and determine the robot’s responsiveness during operation.

<br>

---

![](../_assets/_07_fctrl_ctrl_cnd_control.png)

### ✅ **Control Parameter Items**

| Item             | Description |
|------------------|-------------|
| **Axis**         | Controllable axes (X, Y, Z, Rx, Ry, Rz) |
| **Act**          | Activation checkbox – enables control on the selected axis |
| **Force / Torque** | Target force (N) or torque (Nm)<br>e.g., 50 N on Z-axis |
| **Stiff**        | Stiffness ratio (%); lower values result in more compliant behavior |
| **Vel**          | Velocity limit during force control (mm/s or deg/s) |
| **(–)Pose / (+)Pose** | Negative/positive pose limits (mm or deg); motion is restricted if exceeded |

---

### ✅ Example Interpretation

<br>

> 💡 The following settings are designed for a **vertical sanding** task:

| Axis  | Control | Force | Stiffness | Velocity | Pose Limit         |
|-------|---------|--------|-----------|----------|--------------------|
| **Z**   | `✓`     | 50 N   | 30%       | 20 mm/s  | -50 ~ +50 mm       |
| **Rx**  | `✓`     | 0 Nm   | 10%       | 5 deg/s  | -10 ~ +10 deg      |
| **Ry**  | `✓`     | 0 Nm   | 10%       | 5 deg/s  | -10 ~ +10 deg      |
| **X**, **Y**, **Rz** | –       | –      | –         | –        | –                  |

→ The robot maintains 50 N in the Z-direction while allowing compliant rotation around the Rx and Ry axes.

---

✅ Each axis should be configured based on task-specific requirements (e.g., surface curvature, precision).  
Lower stiffness values provide greater compliance.

> ⚠️ While low stiffness enables flexible interaction, it may cause vibration or noise depending on the robot response and environment.
## 🧩 2.4.3 Force Control Condition – Filtering

Filtering functions are provided to reduce noise from the force sensor and ensure stable input for control.  
Additional features include a **scaling option** that adjusts control intensity within a specific force/torque range,  
and a **bypass option** for more sensitive response to minor inputs.

<br>

---

![](../_assets/_08_fctrl_ctrl_cnd_filtering_smooth_force.png)

### ✅ Smooth Force (Filtering)

Applies a **filter** to the sensor’s force signal to reduce fluctuation and ensure smoother control.

| Item              | Description |
|-------------------|-------------|
| **Enable**        | Apply filtering when checked |
| **Frequency (Freq)** | Cutoff frequency of the filter (e.g., 20 Hz)<br>→ Lower values provide smoother output but slower response |

<br>

---

![](../_assets/_09_fctrl_ctrl_cnd_filtering_smooth_scaling.png)

### ✅ Smooth Scaling

Smoothly adjusts the control response within a defined range of force or torque.  
Useful in tasks requiring fine sensitivity tuning; typically left disabled by default.  
The system can be configured to ignore minor force changes and only respond to forces above a certain threshold.

| Item              | Description |
|-------------------|-------------|
| **Enable**        | Apply scaling within the range when checked |
| **Force Range**   | Target force range (e.g., 2 ~ 8 N) |
| **Torque Range**  | Target torque range (e.g., 0 ~ 0 Nm) |

![](../_assets/_11_fctrl_ctrl_cnd_filtering_scaling_graph.png)

> 💡 If the input force is below the start value, the output is set to 0.  
> 💡 If the input force is above the end value, the original input value is used.  
> ⚠️ If the start and end values are the same, scaling will not be applied.

<br>

---

![](../_assets/_10_fctrl_ctrl_cnd_filtering_cmd_flow.png)


### ✅ Command Flow

Configures how command signals are processed and delivered to the robot.

| Item     | Description |
|----------|-------------|
| **Mode** | `Normal`: Standard command delivery method<br>`Bypass`: Immediate and sensitive command response |
| **Freq** | Filter frequency used in `Bypass` mode (Hz) |

> **Bypass** mode is used to **reflect sensor data immediately** and is recommended only for highly sensitive or experimental use cases.  
> ⚠️ May cause **noise or vibration**, so `Normal` mode is recommended for standard operations.

---

<br>

### ✅ Recommended Settings Guide

| Task Type           | Recommended Settings                            |
|---------------------|-------------------------------------------------|
| Polishing / Sanding | `Smooth Force = ON`, `Freq = 20 Hz`             |
| Delicate Assembly   | `Smooth Scaling = ON`, with conservative range  |
| High Responsiveness / Testing | `Command Flow = Bypass`               |

---

📎 **Filtering**, **Scaling**, and **Command Flow** settings all work together.  
They should be **tuned as a whole** depending on the specific task requirements.## 🧩 2.4.4 Force Control Condition – Motion

During force control operations, motion-related conditions can also be configured.

You can define a **surface contact detection** criterion to determine whether the tool has made full contact with the surface, based on tool orientation.  

Additionally, without using a separate `move` command, the system can automatically generate **spiral**, **bidirectional**, or **zigzag** trajectories  
## 🧩 2.4.4.1 Force Control Condition – Motion – Surface Contact Detection

Real-time evaluation of whether the robot has properly contacted the surface during force control motion (along the tool Z-axis).

---

![](../_assets/_12_fctrl_ctrl_cnd_motion_contact.png)

<br>

### ✅ Surface Contact Detection Criteria

Contact is considered established when **all** the following conditions are satisfied:

| Item               | Description |
|--------------------|-------------|
| **Force Thresh**       | Allowable error between target and actual force (unit: N) |
| **Dev Angle Thresh**   | Instantaneous deviation angle of force direction along tool Z-axis (unit: deg) |
| **Tilt Angle Thresh**  | Angle between contact surface and force direction (unit: deg) |
| **Confirm Time**       | Duration the condition must be held (unit: sec) |

---

<br>

### ✅ Example Setting

> Example: If the following conditions are maintained for 3 seconds, surface contact is considered valid.

| Item             | Value     |
|------------------|-----------|
| Force Error      | `3 N`     |
| Force Direction Change | `20 deg`  |
| Contact Angle    | `30 deg`  |
| Hold Time        | `3 sec`   |

<br>

📌 To use the **Surface Contact Detection** function properly,  
the coordinate system must be set to **Tool** coordinate frame.
## 🧩 2.4.4.2 Force Control Condition – Motion – Auto Trajectory Generation

Motion control conditions can be configured to run in conjunction with force control operations.

In particular, this section allows the configuration of **Spiral**, **Bidirectional**, and **Zigzag** path trajectories.

<br>

---

![](../_assets/_13_fctrl_ctrl_cnd_motion_raster1.png)  
![](../_assets/_15_fctrl_ctrl_cnd_motion_raster3.png)

### ✅ Motion Type

| Type             |
|------------------|
| **Spiral Motion** |
| **Bidirectional Motion** |
| **Zigzag Motion** |

---
![](../_assets/_14_fctrl_ctrl_cnd_motion_raster2.png)

<br>

### ✅ Spiral Motion

Generates a spiral path and trajectory.

| Item            | Description |
|------------------|-------------|
| **Velocity**      | Linear rotational velocity (mm/s) |
| **Radius**        | Maximum spiral radius (mm) – defines the final spiral size |
| **Revolutions**   | Number of full rotations (rev) |

---

### ✅ Bidirectional Motion

Generates a linear raster path that alternates direction line-by-line.

| Item            | Description |
|------------------|-------------|
| **Velocity**       | Linear velocity along the path (mm/s) |
| **Mov Dir**        | Movement direction (+X, -X, +Y, -Y) |
| **Mov Length**     | Length of each movement line |
| **Shift Dir**      | Line shift direction (+X, -X, +Y, -Y) |
| **Shift Length**   | Distance between raster lines |
| **Num Lines**      | Number of lines to generate in movement direction |

---

### ✅ Zigzag Motion

Generates a raster path that alternates direction every line (zigzag pattern).

| Item            | Description |
|------------------|-------------|
| **Velocity**       | Linear velocity along the path (mm/s) |
| **Mov Dir**        | Movement direction (+X, -X, +Y, -Y) |
| **Mov Length**     | Length of each movement line |
| **Shift Dir**      | Line shift direction (+X, -X, +Y, -Y) |
| **Shift Length**   | Distance between raster lines |
| **Num Lines**      | Number of lines to generate in movement direction |

---

📌 The above motions generate XY-plane trajectories relative to the coordinate system selected in **Section 2.4.1**.
# 🧩 3. Force Control Commands

This section provides an overview of the main commands related to the force control feature.  
Each command is used to configure force settings, start/stop control, and execute motions like spiral, bidirectional anc zig-zag movement.

<br>

---

## ✅ List of Force Control Commands

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
## 🧩 3.1 Example: Z-Axis Force Control

The following is a Job program example that uses the **sensor-based force control** function.  
This example is designed to **wait until the external force along the Z-axis exceeds 35N**,  
and then proceed with the task execution.

<br>

---

### 📄 Operation Overview

> 💡 It is recommended to use the `delay` command before enabling force control,  
> to suppress sensor noise and initial vibrations for more stable force response.

> ⚠️ In the `cfo` command, make sure the coordinate system matches the one selected  
> in the force control condition settings in order to receive force data correctly.

<br>

---

### 📁 Job File Example

```python
delay 1.0                           # Wait to stabilize before starting control
fctrl on,cnd=2                      # Start force control (using condition No. 2)
delay 0.5

#get_current_force
var force = cfo("tool", "sensor")   # Get current external force in tool coordinates

# Wait until Z-axis force exceeds 35N
if abs(force.z) < 35 then *get_current_force
delay 5                             # Wait for force stabilization
fctrl off                           # Stop force control
## 🧩 3.2 Example: Control Setting Update

The following is a Job program example where **only the 'Control' section of the force control condition** is updated.  
This approach is useful when you want to change only the force response characteristics during operation,  
while keeping the coordinate system, filters, and motion settings unchanged.

<br>

---

### 📄 Operation Overview

- `fctrl on,cnd=2`: Starts force control using **condition set No. 2** (full configuration)
- `fctrl control,cnd=1`: Replaces **only the 'Control' section** with set No. 1  
  (Coordinate system, filter, and motion remain as in condition set No. 2)

<br>

---

### 📁 Job File Example

```python
delay 1.0                           # Wait to stabilize before starting control
fctrl on,cnd=2                      # Start force control (use condition set No. 2)
delay 0.5

fctrl control,cnd=1                 # Update only the Control section (use condition set No. 1)

delay 5                             # Wait for force stabilization
fctrl off                           # Stop force control
## 🧩 3.3 Example: Contact Surface Detection

This is a Job program example that uses the **contact surface detection** feature in a robotic force control system.

<br>

---

### ✅ Configuration Example

Set the **contact check** condition in the configuration as follows:

> Example: If the following conditions are maintained for 5 seconds,  
> contact is considered successful.

| Parameter              | Value     |
|------------------------|-----------|
| Force Error Threshold  | `3 N`     |
| Force Direction Change | `20 deg`  |
| Contact Angle          | `40 deg`  |
| Hold Duration          | `5 sec`   |

<br>

---

### 📁 Job File Example

```python
delay 1.0                            # Wait to stabilize before starting control
fctrl on,cnd=1                       # Start force control (using condition set No. 1)
delay 0.5                            # Brief wait before executing contact check

wait contact_state()                 # Execute contact check, wait until contact is confirmed

fctrl off                            # Stop force control
## 🧩 3.4 Example: Spiral Motion

This is a Job program example that uses the **Spiral Motion** feature in the robotic force control system.  
The robot maintains a constant **external force of 20N in the Z-axis direction** while performing the spiral path.

<br>

---

### 📄 Operation Overview

> ⚠️ Make sure to set the **Motion Type** to **Spiral** in the **configuration settings**.

> ⚠️ It is recommended to insert a `delay` command before `motion_on`  
> to suppress vibration and ensure more stable force control.

<br>

---

### 📁 Job File Example

```python
delay 1.0                            # Wait to stabilize before starting control
fctrl on,cnd=1                       # Start force control (using condition set No. 1)
delay 0.5                            # Wait before starting spiral motion

fctrl motion_on                      # Start spiral motion
wait motion_state() == 0             # Wait until spiral motion is complete
fctrl motion_off                     # Stop spiral motion

fctrl off                            # Stop force control
# 🧩 4. Monitoring

While the sensor-based force control function is active,  
users can monitor the following status information in real-time through the UI.
## 🧩 4.1 Force Data Monitoring

This function allows you to monitor the external force applied to the robot in real time.  
It is essential to check this information when using the Force Control function.

---

![](../_assets/_16_fctrl_ctrl_panel_force_data.png)

| Item         | Description |
|--------------|-------------|
| **Cartesian** | External force (N or Nm) displayed in the selected coordinate system |
| **Joint**     | Not used in force control |

> ⚠️ The coordinate system of the `Cartesian` external force follows the coordinate frame defined in the force control condition (`cnd`).

> ⚠️ Data is updated **only when force control (fctrl) is active**.

### TP Navigation Path

**[Operation]** → **[Select]** → **[Force Data Monitoring]**
## 🧩 4.2 Force Motion Monitoring

![](../_assets/_17_fctrl_ctrl_panel_force_motion.png)

| Item  | Description |
|-------|-------------|
| **Fext** | Force error (difference between target force and external force) [N or Nm] |
| **Cmd**  | Command position for force control (mm or deg) |

> ⚠️ The coordinate system for `Fext` and `Cmd` follows the coordinate frame defined in the force control condition (`cnd`).

> ⚠️ This data is updated **only when force control (fctrl) is ON**.

### TP Navigation Path

**[Operation]** → **[Select]** → **[Force Motion Monitoring]**
# 🧩 5. Errors & Troubleshooting

During force control operation with an external FT sensor,  
the user can monitor the **status and exception events** in real time via the UI.

---

## Force Control Exception Events & Corrective Actions

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

## Troubleshooting Workflow

1. Check the FT sensor connection  
2. Verify the tool number and coordinate frame  
3. Confirm whether the sensor is supported  
4. Review and back up logs  

---
