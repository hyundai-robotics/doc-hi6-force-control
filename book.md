# ${cont_model} Controller - Force Control with sensors Manual
# About the Manual
# Precautions

{% include file="en/precautions.md" %}
# Safety Cautions

{% include file="en/safety-notice.md" %}
## 1. Overview

This manual provides guidance on how to use the sensor-based force control system.  
The system utilizes a force/torque sensor mounted on the robot to perform control that responds to external forces, enabling more precise and safer contact operations.

This manual covers the following features:

- Sensor configuration methods
- Tool data configuration methods
- Force control condition settings
- Commands
- Monitoring configuration
- Basic examples

This document describes all procedures necessary for users or maintenance engineers to configure the features and understand the operational status.

This feature is available from version V60.32-01 and requires a separate feature license.## 2. Configuration

To use the sensor-based force control function, the following key items must be configured. These items serve as the **criteria** for all controller operations.

---

#### **Setting Menu Access Path**

The force control environment settings can be accessed through the following path on the teaching pendant.

> [F2: System] ➔ 4: Application Parameter ➔ 24: Force Control ➔ 1: System Config 

---

#### **Function Enable/Disable Settings**

Determines whether to globally activate the sensor-based force control function. To normally operate the force control loop within the system, it **must be set to `Enable`**.

* **Enable:** Activates the force control function (runs the real-time loop)
* **Disable:** Deactivates the force control function (operates in normal position control mode)

<br>

**[Setting Screen Example]**

* **Function Deactivated State `Disable`**
  
  ![](../_assets/_19_fctrl_func_off.png)

* **Function Activated State `Enable`**
  
  ![](../_assets/_20_fctrl_func_on.png)

<br>

After activating the function by setting the function usage to **`Enable`**, proceed with the configuration of the sensor communication information and tool offset (length).

---

{% hint style="info" %}

**Prerequisites**
The function usage must be changed to `Enable` and applied before you can proceed with the subsequent steps of sensor parameter configuration, communication connection, and dynamic load identification (calibration).

{% endhint %}## 2.1 F/T Sensor Installation 

When mounting an F/T sensor for precise force control, the physical attachment direction of the sensor must perfectly match the sensor coordinate system configuration within the robot controller. 

If the sensor mounting direction or coordinate system configuration is misaligned, the direction of the force/torque recognized by the controller will differ from the actual direction, which may cause the force control loop to diverge or the robot to malfunction.

---

##### **[Definition of F/T Sensor Coordinate System]**

* **Controller-Based Sensor Coordinate System Rule:** The directions of the `X, Y, and Z axes` of the default sensor coordinate system defined by our robot controller are shown in the figure below.

* **Physical Direction Alignment:** The sensor must be oriented and assembled so that the unique `X, Y, and Z axis` index lines engraved (or printed) on the side of the circular F/T sensor body perfectly align with the direction of the robot's sensor coordinate system.

![](../_assets/_05_fctrl_ctrl_sensor_crd.png)

* **Coordinate System Reference Pose:** The manual figure above shows the sensor coordinate system defined based on the robot being in its standard home position.

* **Precautions during Assembly:** When assembling the sensor mechanism, cross-reference the cable outlet direction or the sensor dowel pin positions with the axis definitions in the manual to ensure it is not mounted in the reverse direction or with an incorrect phase.

---

{% hint style="info" %}

**Tool Load Information Reference:** When identifying dynamic loads and registering tool load information, the center of gravity position must be measured and entered based on the **origin of the F/T sensor reference coordinate system**, not the robot flange coordinate system.

**Prerequisite Check Before Sensor Zero Offset (Bias) Calibration:** Before performing the zero offset (Bias) calibration of the sensor signal, always verify qualitatively on the sensor diagnostic screen that the signs (+/-) of the forces (Fx, Fy, Fz) for the corresponding axes match the actual directions when the robot tool is pushed in a specific direction.

{% endhint %}## 2.2 F/T Sensor Communication Settings

This section describes how to activate real-time data communication with the force/torque (F/T) sensor, which serves as the reference for the control loop during actual force control operations, and how to configure the connection parameters.

[F2: System] ➔ [4: Application Parameter] ➔ [24: Force Control] ➔ [1: System Environment] ➔ **Select [Communication] Tab**

---

![](../_assets/_20_fctrl_func_on.png)



##### **[Key Configuration Items Guide]**

| Configuration Item | Description |
| :--- | :--- |
| **Function Use** | Selects whether to activate the force control loop. To use the function normally, it must be set to **[Enable]**. |
| **Sensor Type** | Selects the F/T sensor manufacturer profile that matches the hardware interface. `(ATI, OnRobot, Robotiq, AIDIN)` |
| **Protocol** | Specifies the method for transmitting and receiving real-time data packets between the sensor controller and the robot controller. Available options are `[UDP]`, `[TCP]`, and `[SCI]`. |
| **Bias** | An offset filter used to cancel the tool dead weight and residual noise at the time of sensor initialization.<br>**⚠️ Note:** In the current version, this is in a **Disabled state** where only the UI component is placed. (Sequential support is planned for the future) |
| **Network Parameters** | • **IP Address:** Enter the unique IP address assigned to the F/T sensor controller.<br>• **Local Port:** The data reception port number on the robot controller side. (Mainly 50001, 50100 are used)<br>• **Remote Port:** The data transmission port number on the F/T sensor side. (Enter the fixed port specified in the manufacturer's specification manual) |## 2.2.1 ATI Configuration

The model-specific configuration methods and communication parameters for ATI sensors are as follows.

---

##### **[Default Communication Parameters]**
All ATI sensor models use the same communication settings below.

* **Protocol:** UDP
* **IP Address:** 192.168.1.2
* **Remote Port:** 49152

---

##### **[Model-Specific Configuration Methods]** <br>

##### **1. ATI (Generic Model)**
This method does not register an individual model separately, but instead **the user manually enters and applies the model-specific scaling values provided by ATI**.

![](../_assets/_01_04_fctrl_env_setting_ATI_Generic_UDP.png)

---

##### **2. ATI (Delta-SI-660-60)**
By using the dedicated Delta model profile pre-registered in the controller, optimized scaling values for the corresponding model are automatically applied.

![](../_assets/_01_01_fctrl_env_setting_ATI_Delta_UDP.png)

---

##### **3. ATI (Theta-SI2500-400)**
By using the dedicated Theta model profile pre-registered in the controller, optimized scaling values for the corresponding model are automatically applied.

![](../_assets/_01_02_fctrl_env_setting_ATI_Theta_UDP.png)

---

##### **4. ATI (Omega-SI7200-1400)**
By using the dedicated Omega model profile pre-registered in the controller, optimized scaling values for the corresponding model are automatically applied.

![](../_assets/_01_03_fctrl_env_setting_ATI_Omega_UDP.png)

{% hint style="info" %}

Since the Delta, Theta, and Omega models (excluding the Generic model) provide predefined parameters, malfunctions caused by incorrectly entered scaling values can be prevented.

{% endhint %}## 2.2.2 OnRobot Configuration

The configuration method and communication parameters for OnRobot sensors are as follows.

---

##### **[Default Communication Parameters]**
Enter the settings below accurately to connect the OnRobot sensor with the controller.

* **Protocol:** UDP
* **IP Address:** 192.168.1.1
* **Remote Port:** 49152

---

##### **OnRobot HEX (HEX-E / HEX-H) Configuration**

This is the configuration screen for using OnRobot HEX sensor models. After entering the communication parameters, verify that the settings have been applied normally.

![](../_assets/_02_fctrl_env_setting_OnRobot_HEX_E_UDP.png)
## 2.2.3 Robotiq Configuration

Since Robotiq sensors (such as the FT 300S) utilize serial communication (SCI), you must complete both the force control environment configuration and the serial port settings.

---

##### **[Step 1: Force Control Sensor Configuration]**
First, specify the communication protocol as serial communication (SCI) on the force control user environment configuration screen.

![](../_assets/_03_01_fctrl_env_setting_Robotiq_FT300S_SCI.png)

---

##### **[Step 2: Serial Port Environment Configuration]**
To activate serial communication, navigate to the following path and configure the communication port parameters of the controller.

> **[F2: System]** → **2: Control Parameter** → **3: Serial Port** → **1: Environment Settings**

![](../_assets/_03_02_fctrl_env_setting_Robotiq_FT300S_SCI_CFG.png)

{% hint style="info" %}

Instead of entering a separate IP address, it is essential for the Robotiq sensor to match the physical serial port (SCI) channel and Baud rate located on the back or inside of the controller.

After specifying the sensor in Step 1, you must complete the serial port configuration in Step 2 without omission to prevent communication errors from occurring.

{% endhint %}## 2.2.4 AIDIN Configuration

The configuration method and communication parameters for AIDIN sensors are as follows.

---

##### **[Default Communication Parameters]**

Enter the settings below accurately to connect the AIDIN sensor with the controller.

* **Protocol:** UDP
* **IP Address:** 192.168.1.199
* **Remote Port:** 50000

---

##### **AIDIN Sensor Configuration**

This is the configuration screen for using AIDIN 6-axis force/torque sensor models. Enter the designated IP address and remote port values without typos, and then save the settings.

![](../_assets/_21_fctrl_env_set_AIDIN.png)

{% hint style="info" %}

Unlike other sensors, the AIDIN sensor **uses `50000` as its remote port number**. Please note that communication will not connect if you use the controller default values or a port from another manufacturer (49152).

Verify that the assigned unique IP address (`192.168.1.199`) does not conflict within the controller network band before proceeding with the configuration.

{% endhint %}## 2.3 F/T Sensor Offset Settings

This section describes how to configure the **task coordinate system**, which serves as the reference for the control loop during actual force control operations, and how to enter the positional offset from the robot flange to the sensor.

[F2: System] ➔ [4: Application Parameter] ➔ [24: Force Control] ➔ [1: System Environment] ➔ **Select [Mounting] Tab**

---

![](../_assets/_22_fctrl_env_set_offset_sensor.png)


##### **[Force Control Operation Frame Settings]**

Specifies the sensor data reference coordinate system used to track the target force when the force control algorithm operates. 

* **Based on Sensor Frame:**
  Performs force control based on the **unique coordinate system of the F/T sensor (Sensor Frame)** mounted at the end-effector of the robot. This is not suitable for environments where force needs to be controlled based on the tool center point (TCP).
* **Based on Tool Frame:**
  Performs force control by **transforming the force/torque data measured by the F/T sensor into the final TCP coordinate system**. Select this option when precise force control is required based on the tool tip.

--- 

##### **[Prerequisites for Tool Frame Configuration]**

To perform normal coordinate transformation operations by setting the operation frame to the **'Tool Frame'**, the following **two geometric parameters must be configured beforehand**.



###### **1. Sensor Offset Length Settings**
Enter the precise physical distance (Z) from the center of the robot flange surface to the center of the F/T sensor coordinate system. Currently, this function is supported only when the flange rotation center axis aligns with the center of the sensor.

* **Configuration Range:** `0.0` ~ `1000.0` (mm)

![](../_assets/_23_fctrl_env_set_offset_tool.png)


###### **2. Motion Tool Data Settings**
The **TCP length and direction** of the tool number designated for the corresponding program step (Move command) where force control is executed must be entered accurately. The controller calculates the relative coordinates from the flange to the TCP tip based on this data.

[F2: System] ➔ [3: Robot Parameter] ➔ [1: Tool Data]

![](../_assets/_24_fctrl_env_set_offset_motion_tool_data.png)

{% hint style="warning" %}

If an invalid tool number is used while the operation frame is set to the **Tool Frame**, or if the tool data (TCP) values differ from the actual setup, the system may malfunction or diverge during force control operations due to coordinate transformation errors.

After changing the parameter settings, always press the **[Apply/OK]** button at the bottom of the screen to apply them to the controller.

{% endhint %}## 3. Tool Data

This is a basic configuration that must be performed before using the force control function. It serves as the foundation for **precisely calculating only the pure force/torque** generated during contact with the environment by removing the weight component of the tool itself from the F/T sensor measurements.

---

##### **[Tool Data Settings]**

This is the step where the user manually registers the physical specifications of the tool mounted at the end of the robot flange.

---

##### **[Dynamic Load Identification]** 

This function directly measures physical parameters through automatic robot motions when it is difficult to know the exact specifications of the tool.## 3.1 Tool Data Settings

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

{% endhint %}## 3.2 Dynamic Load Identification

This function analyzes the data from the F/T sensor mounted at the end of the robot in real time to precisely identify the physical characteristics of the attached tool (Payload)—such as **mass, center of gravity, and sensor bias**—through a series of calibration motions.

{% hint style="info" %}

This function is supported from controller software version **V70.02-00 or later**.

{% endhint %}

The Dynamic Load Identification function can be accessed through the following path:

[F2: System] - 4: Application Parameter - 24: Force Control - 2: Tool Data ➔ **[F1: Dynamic Load Identification]**

---

![](../_assets/_25_fctrl_dyna_id_main.png)



##### **[UI Configuration and Status Display Items]**

| Execution Item | Description |
| :--- | :--- |
| **Force Control Tool No.** | The target number to identify and save the dynamic load parameters. This refers to the **pure tool (Payload) physically attached to the front end of the F/T sensor**. |
| **Robot Motion Tool No.** | The reference tool number used when running the dynamic identification motion. This refers to the **integrated tool information that physically includes the position and weight of the F/T sensor itself**. |
| **Current / Target Angle** | Displays the current real-time angle of each robot axis and the matching target pose angle during the identification run (Verification/Normal Operation). |
| **Sensor Data** | Displays the real-time force and torque data feedback collected from the F/T sensor during operation. |
| **Limit Min / Max** | The minimum and maximum operational limit angles for each robot axis, restricted by software to ensure the identification motion runs safely. |
| **Verification Operation** | A test run performed prior to the actual load identification to check in advance for any surrounding interference along the robot's movement path and the tension (pulling) of the sensor cable. |
| **Normal Operation** | Activated after the Verification Operation completes normally without alarms. This is the actual identification run that collects F/T sensor data at high speed to calculate the load parameters. |


{% hint style="info" %}

**Robot Motion Tool Entry Sequence Guide:**

  1. **Before Identification:** First, enter only the approximate weight information into the 'Robot Motion Tool No.' and then proceed with the run.

  2. **After Identification:** Once the dynamic load identification is complete, update the data by finally adding the measured results to the dead weight and center of gravity (CoG) of the F/T sensor itself.

{% endhint %}

---

##### **[Identification Motion and Poses]** During the execution of the Verification Operation and Normal Operation, the robot's wrist axes (Axes 4, 5, and 6) automatically run through a sequence of 6 predefined default poses to accurately acquire multi-axis gravity direction matching data from the F/T sensor.

* **P1:** `[0, 90, 0, 0, -90, 0]`
* **P2:** `[0, 90, 0, 0, 90, 0]`
* **P3:** `[0, 90, 0, 0, 0, 0]`
* **P4:** `[0, 90, 0, 0, 0, 180]`
* **P5:** `[0, 90, 0, 0, 0, 90]`
* **P6:** `[0, 90, 0, 0, 0, -90]`

![](../_assets/_26_fctrl_dyna_id_mot.png)

{% hint style="warning" %}

**Prerequisites for Manual Operation:** To execute the Verification/Normal Operation, the controller mode switch must be in the **[MANUAL]** state, the motors must be ON, and the **enabling switch (Deadman Switch)** on the teaching pendant (TP) must be maintained in the On (pressed) state.

**Surrounding Environment Inspection:** Before starting the operation, check the clearance length of the F/T sensor cable to ensure there is no twisting or pulling during rotation, and secure a sufficient work area within the motion radius so that the robot body and tool do not collide with surrounding structures or safety fences.

{% endhint %}

##### **[Operation Sequence and Procedures]** ###### **Step 1: Verification Operation**
* **Purpose:** A step to first check the surrounding space and for any interference so that the robot's movement during tracking can be performed safely.

* **Role:** Before the full-scale identification motion, the robot moves at a low speed to verify that there are no collision paths with surrounding facilities or mechanisms.

###### **Step 2: Normal Operation**
* **Purpose:** Runs the multi-axis identification motion to calculate the tool's weight and center of gravity position in real time based on the F/T sensor data.

* **Role:** The robot changes its pose into various configurations with predefined angular displacements to measure the component forces of the dead weight applied to the sensor.

###### **Step 3: Check Results**
* When the measurement is complete, a pop-up window displays the currently applied `Existing Value` and the newly calculated `Estimated Value` based on the sensor.

![](../_assets/_31_fctrl_dyna_id_result.png)

| Execution Item | Description |
| :--- | :--- |
| **Weight [Kg]** | The total estimated mass of the tool. |
| **Center [mm]** | The center of gravity position of the tool along the X, Y, and Z directions relative to the origin of the sensor coordinate system. |
| **Force/Torque Bias** | The accumulated zero offset (Bias) value unique to the sensor. |
| **Error Rate [%]** | Indicates the data reliability and error rate within the identification trajectory, displayed separately for Force and Torque. |


###### **Step 4: Apply Data**
* Pressing the **[✓ OK]** button at the bottom right of the screen finally saves and reflects the newly estimated `Estimated Value` information into the corresponding force control tool data.

{% hint style="info" %}

**Safety Notice:** During Step 2 `Normal Operation`, the robot performs multi-axis reversal movements. Therefore, the operation must be executed only after completely securing the interference-free zone around the tool.

**Error Rate Compliance Criterion:** The measured **error rate must be within 5%**.

**Troubleshooting Tip:** If the error rate exceeds 5% and is abnormally high, there may have been external interference during measurement or tension acting on the sensor cable. Recheck the clearance and interference of the sensor cable, and then measure again.

{% endhint %}

---## 4. Force Control Options 

This menu is used to process sensor signals according to task conditions and to configure the robot's response and behavior control methods in detail, aiming to improve the quality of the force control process and system stability. 

In addition to basic force/torque control settings, it provides advanced control options such as noise filtering, profiles, contact condition detection, and automatic path generation.

[F2: System] ➔ [4: Application Parameter] ➔ [24: Force Control] ➔ [3: Force Control Options]

---

{% hint style="info" %}

**Precautions:** Individual parameters within the force control options are interdependent. During initial tuning, set the robot's operation speed limit low, and gradually determine the optimal values while verifying the filter and profile performances.

{% endhint %}### 4.1 Basic Settings

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

{% endhint %}### 4.2 Control Parameters

This menu is used to select the degrees of freedom (axes) to apply force control, and to configure the target force/torque, responsiveness of the virtual system, viscous resistance (damping), and speed and displacement limit values. These are key parameters that determine the flexibility and reaction speed of the actual robot when it comes into contact with the environment.

[F2: System] ➔ [4: Application Parameter] ➔ [24: Force Control] ➔ [3: Force Control Options] ➔ **Select [Settings] Tab**

---

![](../_assets/_07_fctrl_ctrl_cnd_control.png)


##### **[Control Configuration Items]**


| Item | Description |
| :--- | :--- |
| **Axis** | Indicates the 6-DOF axes targeted for control. (X, Y, Z: Linear velocity directions / Rx, Ry, Rz: Rotational directions) |
| **Active** | Specifies whether to activate force control for the corresponding axis. When activated, the box lights up in **yellow**. |
| **Target** | Enter the target force (Unit: N) or target torque (Unit: Nm). |
| **Response** | Adjusts the initial responsiveness (%) of the robot to external forces or target value changes. The **lower the set value, the faster the control response speed, allowing it to reach the target value agilely**. |
| **Damping** | The damping ratio (%) that matches the virtual viscous damping coefficient. The **lower the set value, the more flexibly it conforms** and responds to external forces. |
| **Limit** | Limits the maximum output speed that can occur during force control operation. (Linear axis: mm/s, Rotational axis: deg/s) |
| **-Pos / +Pos** | The bidirectional travel limit (soft limit) range within which the robot can be forcibly pushed or moved during force control operation. (mm or deg) |


{% hint style="info" %}

**Coordinate System Reference:** The direction definition of each axis (X, Y, Z, Rx, Ry, Rz) is mapped based on the **task coordinate system selected in the preceding [Settings] tab**.

**Response Tuning Guide:**
  * **When set to 0%:** This is advantageous for mitigating the impact generated during initial contact, stably controlling the movement, and suppressing vibrations. (However, a larger damping value results in a slower response.)
  * **When set to 1% or higher:** The target control speed and tracking performance are improved, allowing for a more agile response. However, within certain ranges, the deviation in responsiveness according to the change in the set value may be subtle.

**Speed and Position Limit Management:** If the balance between response and damping settings is incorrect, or if the speed limit value is set excessively high, the robot may accelerate rapidly upon contact with an object, causing system vibrations. During initial tuning, always ensure safety by **setting the [Limit] speed value low**, and then gradually increase control performance.

{% endhint %}

---

##### **Control Configuration Example (Vertical Direction Sanding Task)**

This is a UI configuration matching example for a typical sanding/grinding process that maintains the posture of the actual tool while applying pressure.


| Axis | Active | Target | Response | Damping | Limit | Position Limit (- / +) |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **X** | Off | 0 N | 0 % | 100 % | 0 mm/s | 0 / 0 mm |
| **Y** | Off | 0 N | 0 % | 100 % | 0 mm/s | 0 / 0 mm |
| **Z** | **On** | **20 N** | **10 %** | **20 %** | **5 mm/s** | **0 / 30 mm** |
| **Rx** | **On** | **0 Nm** | **0 %** | **10 %** | **5 deg/s** | **-20 / 20 deg** |
| **Ry** | **On** | **0 Nm** | **0 %** | **10 %** | **5 deg/s** | **-20 / 20 deg** |
| **Rz** | Off | 0 Nm | 0 % | 100 % | 0 deg/s | 0 / 0 deg |

* **Z-axis Control:** Gently settles onto the surface while maintaining a **constant force of 20N** in the normal direction (pressurizing axis).
* **Rx, Ry-axis Control:** Soft motion compliance occurs as the tool is coupled with a **target torque of 0Nm and low damping (10%)** to allow it to remain flat in response to curved or warped machining surface edges.
* The coordinate system must be configured to "Tool".

---

{% hint style="warning" %}

**Vibration and Noise Notice:** Lowering the damping and response ratios allows for a flexible response to external environment changes. However, if the static stiffness of the target object is too high or combined with high-speed robot operation conditions, it may cause **vibrations and high-frequency noise** due to control phase lag, so an adequate damping margin must be secured.

{% endhint %}### 4.3 Filtering

This menu is used to configure the filter function, which suppresses signal noise in F/T sensor data to establish a stable control environment, and the Agility Mode, which maximizes the system's tracking performance.

[F2: System] ➔ [4: Application Parameter] ➔ [24: Force Control] ➔ [3: Force Control Options] ➔ **Select [Filtering] Tab**

---

![](../_assets/_08_fctrl_ctrl_filtering.png)


##### **[Smooth Force]**

Attenuates high-frequency noise from the force/torque signals collected from the sensor to prevent shakiness in robot motion and control smooth contact behavior.

| Item | Description |
| :--- | :--- |
| **Force Filtering** | When activated, the checkbox lights up in **yellow**. |


{% hint style="warning" %}

If filtering is excessively applied when using an F/T sensor with excellent signal quality, a phase delay (Time Delay) may occur within the control loop. Since this can cause degradation in control performance during high-speed force tracking applications, determine whether to apply it after verifying the actual signal characteristics in high-speed applications.

{% endhint %}

---

##### **[Agility Mode]**

This mode drastically improves the robot's initial control response speed to reach the target force. It is essential in precise force control processes where the tool (TCP) moves at high speed and needs to respond immediately to changes in the environment.

| Configuration Item | Description |
| :--- | :--- |
| **Agility Mode** | When activated, the checkbox lights up in **yellow**. |
| **Frequency [Hz]** | Specifies the bandwidth operating frequency of the Agility Mode. The **higher the set frequency value, the faster the robot's response speed** and the higher the agility. |

{% hint style="warning" %}

**Agility Mode Termination Characteristics**

* **Caution Specification:** When `fctrl off` (termination) is executed, Agility Mode unconditionally **pauses in place for 0.5 seconds before terminating**.

* **On-Site Issue:** If the robot pauses for 0.5 seconds while maintaining contact with the product, continuous pressure is applied to the surface, which may damage the product or leave marks.

* **Mitigation Method:** Refer### 4.4.1 Profile: Soft Start

This function is designed to prevent a rapid impact force that may occur when the robot initially makes contact with and enters the task object. When reaching the target control value, the target value is gradually applied in the form of a smooth curve (Profile Curve) rather than a step command.

[F2: System] ➔ [4: Application Parameter] ➔ [24: Force Control] ➔ [3: Force Control Options] ➔ **Select [Profile] Tab**

---

![](../_assets/_09_fctrl_ctrl_soft_start.png)

##### **[Key Configuration Items]**

| Configuration Item | Description |
| :--- | :--- |
| **Function Activation** | Specifies whether to use the function via the checkbox. |
| **Start Ratio [%]** | Sets the force/torque threshold at the moment the function is triggered (operation start) as a percentage (%) of the final target value. Profile control begins when the sensor measurement reaches this ratio. |
| **Time [s]** | Defines the profile curve time (Unit: seconds) required from the moment the start ratio is satisfied until the final target force/torque value is completely reached. |

![](../_assets/_28_fctrl_soft_start.png)

##### **[Understanding through Operation Example]**

This is an example of the actual robot's tuning behavior based on the settings below.

* **Final Target Force:** `10 N` (Z-axis set value in the Settings tab)
* **Start Ratio:** `50 %` (Triggers the function when reaching **5 N**, which is 50% of the final target)
* **Profile Time:** `5 s`

###### **Step 1. Initial Contact and Standby (Initial Contact Phase)**
As the robot descends and begins contact with the task object, the current force measured by the sensor starts to rise. At this moment, the Soft Start function is officially activated as soon as the actual measured data reaches the trigger reference point of **5 N**.

###### **Step 2. Entering Profile Interval (Profile Control Phase)**
From the moment the function is activated, the controller does not abruptly increase the command force in a step form. It gradually increases the force command in a smooth curve over the designated **5 seconds**, stably settling the robot until the final target value of 10 N is reached.

{% hint style="info" %}

**On-Site Application Tip:** This setting is essential when assembling parts with a high risk of damage (glass, displays, etc.) or when initially settling onto precise machined surfaces to prevent product defects and scratches caused by contact impact.

**On-Site Troubleshooting Guide:** If an abrupt impact still occurs during initial entry, **lower the [Start Ratio]** to activate the function earlier, or **increase the [Time] value** to adjust the pressurizing curve more gently.

{% endhint %}### 4.4.2 Profile: Velocity Clamp

During force control operation, if the speed is excessively high when the robot makes contact with the environment (object), excessive overshoot and divergence (vibration) of the control system will occur. This function is designed to fundamentally suppress mechanical vibrations and impacts of the system by forcibly clamping the robot's maximum operating speed (Vmax) to a lower level the moment the currently detected force/torque value exceeds a user-configured threshold.

[F2: System] ➔ [4: Application Parameter] ➔ [24: Force Control] ➔ [3: Force Control Options] ➔ **Select [Profile] Tab**

---

![](../_assets/_10_fctrl_ctrl_vel_clamp.png)

##### **[Key Configuration Items]**

| Configuration Item | Description |
| :--- | :--- |
| **Function Activation** | Specifies whether to use the function via the checkbox. |
| **Linear Velocity - Force Condition [% Target]** | Trigger condition for the linear velocity axes (X, Y, Z). When the current force reaches the set percentage (%) relative to the final target force configured in the [Settings] tab, the speed limit is executed immediately. |
| **Linear Velocity - Limit Ratio [% Limit Speed]** | Defines the attenuation ratio (%) to scale down the maximum limit speed per axis previously configured in the [Settings] tab, once the force condition is satisfied. |
| **Angular Velocity - Torque Condition [% Target]** | Trigger condition for the rotational axes (Rx, Ry, Rz). When the current torque reaches the set percentage (%) relative to the final target torque, the speed limit is executed. |
| **Angular Velocity - Limit Ratio [% Limit Speed]** | Defines the attenuation ratio (%) to scale down the maximum limit speed of the rotational axes previously configured in the [Settings] tab, once the torque condition is satisfied. |

![](../_assets/_14_fctrl_ctrl_vmax_clamp.png)


##### **[Understanding through Operation Example]**

* **Default Limit Speed:** `2.0 mm/s` (Set value in the [Settings] tab)
* **Final Target Force:** `10 N` (Set value in the [Settings] tab)
* **Force Condition [% Target]:** `50 %` (Triggers the function when reaching `5 N`, which is 50% of the final target)
* **Limit Ratio [% Limit Speed]:** `30 %` (Clamps downward to `0.6 mm/s`, which is `30%` of the existing speed limit)

---

###### **Step 1. Initial Entry and Force Trigger**
After the robot descends and makes contact with the object, the speed limit algorithm forcibly intervenes the moment the actual measured force data rises rapidly and surpasses the trigger reference point of **5 N**.

###### **Step 2. Velocity Clamping and Vibration Suppression**
Before the function is activated, the robot displays vibrations up to around the maximum Vmax of `2.0 mm/s` in order to track the target force. 

However, the moment the force condition is satisfied and the limit ratio is newly applied, the robot's operating speed is **powerfully clamped within the predefined limit line of `0.6 mm/s` (30% of the original limit)**. As a result, excessive behavior of the control system is restricted, and the force data below also stops vibrating and stably converges to the target value of 10 N.

---

{% hint style="info" %}

**On-Site Tuning Guide (Vibration Control):** Activate this function when initial contact vibrations (bouncing phenomena) cannot be resolved solely by adjusting response or damping. By **adjusting the [Limit Ratio] downward to an appropriate level**, the physical speed margin is restricted, allowing you to suppress vibrations effectively.

{% endhint %}

{% hint style="warning" %}

**Side Effects of Excessive Restriction:**
If the [Limit Ratio] is set too low (e.g., 5% or less), the vibration will be suppressed, but the robot will lack the speed required to push into the target force. 

{% endhint %}### 4.4.3 Profile: Force/Torque Scaling

This function blocks the force control loop from responding when the F/T sensor data is below a certain magnitude, and smoothly connects the output to the original target control line via a smooth curve or step form once it exceeds the threshold, thereby enhancing overall contact stability.

[F2: System] ➔ [4: Application Parameter] ➔ [24: Force Control] ➔ [3: Force Control Options] ➔ **Select [Profile] Tab**

---

![](../_assets/_11_fctrl_ctrl_smooth_scaling.png)

##### **[Key Configuration Items]**

| Configuration Item | Description |
| :--- | :--- |
| **Function Activation** | Specifies whether to use the function via the checkbox. |
| **Force Range - Start [N]** | The lower limit where the deadband is applied. Measurements below this value are output as `0 N`. |
| **Force Range - End [N]** | The upper limit where the data synchronizes 1:1 with the original data. Measurements above this value are output directly without calibration. |
| **Torque Range - Start [Nm]** | The lower limit where the deadband is applied. Measurements below this value are output as `0 Nm`. |
| **Torque Range - End [Nm]** | The upper limit where the data synchronizes 1:1 with the original data. Measurements above this value are output directly without calibration. |

---

##### **[Understanding through Operation Examples]**

<br> 

###### **Scaling (Start < End)**
* **Configuration Example:** Start `5 N` / End `15 N`

![](../_assets/_12_fctrl_ctrl_scaling_graph.png)

* **Operation Analysis:**
  
  A. **5 N or less:** The deadband is applied, outputting `0 N` to block fine noise and vibrations.
  
  B. **5 to 15 N:** The data is interpolated in the form of a smooth curve to prevent sudden data spikes.
  
  C. **15 N or more:** The original sensor values are reflected directly (1:1 linear) into the control loop without filtering.

---

###### **Step Scaling (Start ≥ End)**
* **Configuration Example:** Start `5 N` / End `0 N` (When the start value is greater than or equal to the end value)

![](../_assets/_13_fctrl_ctrl_scaling_threshold_graph.png)

* **Operation Analysis:**

  A. **Less than 5 N:** Treated as `0 N` because the measurement has not reached the threshold.
  
  B. **5 N or more:** Immediately jumps (Steps) to the original data line upon satisfying the criterion, and outputs the original values directly thereafter.

---

{% hint style="info" %}

**Automatic Mode Switching:** If the [Start] value is greater than or equal to the [End] value, it operates in `Dead-Zone` mode without curve interpolation.

**On-Site Tuning Tip:** To block sensor noise caused by robot vibrations or external shaking, set the **[Start] value slightly higher than the maximum measured noise level** to secure an adequate deadband.

{% endhint %}### 4.5.1 Motion: Contact Conditions

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

{% endhint %}### 4.5.2 Motion: Automatic Path Generation

This function automatically generates and moves along a specific pattern trajectory on a designated plane while maintaining the force control state.

[F2: System] ➔ [4: Application Parameter] ➔ [24: Force Control] ➔ [3: Force Control Options] ➔ **Select [Motion] Tab**

---

![](../_assets/_15_fctrl_motion_type.png)

##### **[Motion Type]**

Provides a total of three trajectory generation modes depending on the purpose of use.

* **Spiral (Spiral Motion):** Generates a trajectory that expands outward in circles from a center point. (e.g., Grinding, Polishing processes)
* **Bidir (Bidirectional Motion):** Generates a reciprocating trajectory to fill a surface. (e.g., Surface machining of large areas)
* **Unidir (Unidirectional Motion):** Generates a trajectory that repeatedly runs in one direction and returns. (e.g., Sanding, Dispensing processes)

---

###### **1. Spiral (Spiral Motion)**

This function generates a path that starts from a center point and expands its radius in a concentric circular form.

| Item Name | Description |
| :--- | :--- |
| **Speed** | The TCP linear velocity moving along the spiral trajectory (Unit: mm/sec) |
| **Radius** | The maximum radius of the spiral to be expanded finally (Unit: mm) |
| **No. of Revolutions** | The total number of rotations from the start point to the end point (Unit: rev) |

---

###### **2. Bidir (Bidirectional Motion)**

This function generates a continuous linear path in a reciprocating form while changing the direction of the end-effector machining.

![](../_assets/_16_fctrl_ctrl_motion_bidirectional.png)

| Item Name | Description |
| :--- | :--- |
| **Speed** | The TCP linear velocity moving along the path (Unit: mm/sec) |
| **Travel Direction** | The main machining operation direction (+X, -X, +Y, -Y) |
| **Travel Length** | The single-run scale distance of the main machining path (Unit: mm) |
| **Line Break Direction** | The pitch movement direction skipping to the next line (+X, -X, +Y, -Y) |
| **Line Break Length** | The pitch distance between adjacent lines (Unit: mm) |
| **Corner Radius** | The rounding radius of the corner section where the line changes direction (Unit: mm) |

{% hint style="info" %}

**Corner Radius Configuration Limit:** The maximum value of the corner radius cannot exceed half of the smaller value between the [Travel Length] and the [Line Break Length].

{% endhint %}

---

###### **3. Unidir (Unidirectional Motion)**

To always maintain a constant forward operation, this function generates a path that shifts to the next line by returning to the starting axis after a one-way travel.

![](../_assets/_17_fctrl_ctrl_motion_unidirectional.png)

| Item Name | Description |
| :--- | :--- |
| **Speed** | The TCP linear velocity moving along the path (Unit: mm/sec) |
| **Travel Direction** | The unidirectional machining operation direction (+X, -X, +Y, -Y) |
| **Travel Length** | The distance of a single one-way machining path (Unit: mm) |
| **Line Break Direction** | The pitch movement direction skipping to the next line (+X, -X, +Y, -Y) |
| **Line Break Length** | The pitch distance between adjacent lines (Unit: mm) |
| **No. of Lines** | The total number of lines to be generated according to the designated travel direction and line break length (Unit: ea) |

---

{% hint style="info" %}

**Coordinate System Guide:** All automatic path generation functions (Spiral, Bidir, Unidir) calculate 2D trajectories based on the **XY plane of the reference coordinate system** specified in the force control coordinate system configuration item.

{% endhint %}# 5. Commands

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

{% endhint %}## 5.1 Z-Axis Force Control 

The following is an example of a Job program that uses the **sensor-based force control function** on a robot.  
This example is designed to wait until the **external force applied along the Z-axis reaches 35N or higher** before executing the subsequent tasks.

---

##### **[Operation Overview]**

- Securing time prior to starting force control via the delay command helps suppress sensor noise or initial vibrations, enabling more stable force control operation.

---


##### **[JOB Program]** 

```python
delay 1.0                           # Stabilization wait before starting control
fctrl on,cnd=2                      # Start force control (Uses condition number 2)
delay 0.5

#get_current_force
var force = _fctrl.force_z          # Current force in the Z direction based on the coordinate system configured in cnd=2

# Condition Loop: Wait until the Z-axis external force becomes 35N or higher
if abs(force.z) < 35 then *get_current_force
delay 5                             # Wait for external force stabilization
fctrl off                           # Terminate force control## 5.2 Changing Control Settings 

The following is a Job program example that **modifies only the 'Control' items among the force control conditions** on a robot.  
This approach is useful when you want to change only the external force response characteristics during real-time operation while keeping the filter, coordinate system, and motion settings as they are.

---

##### **[Operation Overview]**

- fctrl on,cnd=2: Applies the entire configuration set number 2 when starting force control.
- fctrl control,cnd=1: Changes **only the control parameters** to configuration set number 1.  
  (The coordinate system, filter, motion, etc., remain in the state configured by set number 2.)

---

##### **[JOB Program]** 

```python
delay 1.0                           # Stabilization wait before starting control
fctrl on,cnd=2                      # Start force control (Uses condition number 2)
delay 0.5

fctrl control,cnd=1                 # Change force control configuration (control parameters only) (Uses condition number 1)

delay 5                             # Wait for external force stabilization
fctrl off                           # Terminate force control## 5.3 Contact Surface Detection Function 

The following is an example of a Job program that uses the **contact surface detection function** on a robot.

---

##### **[Operation Overview]**

Configure the **contact** conditions in the **settings** as follows:

- Example: If contact is maintained based on the criteria below for 5 seconds, the contact surface detection is determined as OK.

| Item | UI Value |
|---|---|
| Force Error | 3 N |
| Force Direction Variation | 20 deg |
| Contact Angle | 40 deg |
| Duration | 5 sec |


---

##### **[JOB Program]**

```python
delay 1.0                            # Stabilization wait before starting control
fctrl on,cnd=1                       # Start force control (Uses condition number 1)
delay 0.5                            # Wait for 0.5 seconds before executing the contact surface detection condition

wait _fctrl.contact, 20              # Execute contact surface detection condition, wait until contact surface detection is OK, check for a maximum of 20 seconds

fctrl off                            # Terminate force control## 5.4 Spiral Motion 

The following is an example of a Job program that uses **Spiral Motion** on a robot.  
This example is designed to execute tasks while maintaining an **external force applied along the Z-axis at 20N**.

---

##### **[Operation Overview]**

- The **motion type** must be configured to Spiral in the **settings**. 

- Including a mandatory delay command before the fctrl motion_on command helps suppress vibrations, enabling more stable force control operation.

---

##### **[JOB Program]** 

```python
delay 1.0                            # Stabilization wait before starting control
fctrl on,cnd=1                       # Start force control (Uses condition number 1)
delay 0.5                            # Wait before starting spiral motion

fctrl motion_on                      # Start spiral motion
wait _fctrl.motion==0                # Wait until spiral motion terminates
fctrl motion_off                     # Terminate spiral motion

fctrl off                            # Terminate force control## 5.5 Continuous Switching of Control Conditions Using For Loop

This is an example of sequentially and automatically switching multiple force control conditions (`cnd`) using a `for` loop statement in the robot script language.

---

##### **[Precautions During Manual Mode Step Forward/Backward]**

* **Mandatory Prior Variable Declaration:** If a variable is specified as an argument in the program, such as `fctrl on, cnd=idx_cnd`, the controller will only recognize it normally if the corresponding variable is declared and initialized beforehand (`var idx_cnd=1`).
* **Cause of Error:** If you execute only the `fctrl on` command line independently via manual step (forward/backward) without running the variable initialization line, the controller cannot determine whether the value assigned to the `idx_cnd` variable is valid (i.e., whether it is a registered condition number in the UI). As a result, it interprets it as an unknown value (garbage value) in memory, which **causes a system error**.
* **Corrective Action:** When testing or verifying line operations manually, always execute the variable initialization statement (`var idx_cnd=1`) first to assign a valid condition number to the variable before running the `fctrl on` line.


---

##### **[JOB Program]** 

```python
S1   move P,spd=5%,accu=0,tool=0  
S2   move L,spd=5%,accu=0,tool=0   # Move to home position and approach position
     delay 2
     
     var idx_cnd=1                 # Declare force control condition number variable
     for idx_cnd=1 to 3            # Loop operation: Sequentially apply registered force control conditions 1 through 3 

       delay 3
       fctrl on,cnd=idx_cnd
       delay 20
       fctrl off
S3   move L,spd=5%,accu=0,tool=0  

     next
     
     end## 5.6 Methods to Work Around Agility Mode Termination Characteristics

Agility Mode has a specification where it unconditionally **pauses for 0.5 seconds** at that specific point before terminating when the `fctrl off` (termination) command is executed. 

* **Expected Issue:** If control is terminated while maintaining contact with the surface immediately after machining or dispensing is completed, the pressure is maintained for 0.5 seconds, which may damage the product surface or leave marks.

* **Solution:** Since position offset commands (`shift`) cannot be used during force control, you must switch in real time to a **workaround condition (cnd) that applies a force in the direction opposite to the pressurizing direction** before executing `fctrl off` to detach the robot from the surface first. Afterwards, it safely terminates following a 0.5-second pause in a non-contact (air) state.

---

##### **[Condition Settings Configuration]**

* **Main Control Condition (cnd=4):** A condition that activates Agility Mode to perform surface machining and automatic path motions.

* **Workaround Condition (cnd=5):** A condition configured to escape in the direction opposite to the main pressurizing direction to prevent product damage.

![](../_assets/_29_agility_main_cnd.png)
*▲ Figure: Main force control condition (cnd=4) configuration screen with Agility Mode activated*

![](../_assets/_30_agility_escape_cnd.png)
*▲ Figure: Workaround condition (cnd=5) configuration screen set to apply an external force in the opposite direction for surface detachment*


---

##### **[JOB Program]**

```python
# Move to home position and machining approach position
S1   move P,spd=5%,accu=0,tool=0  
S2   move L,spd=5%,accu=0,tool=0  
     delay 2
     
# Execute main force control and automatic path
     fctrl on,cnd=4                # Start main force control (Agility Mode)
     wait _fctrl.contact,20        # Wait for surface contact completion (Timeout 20 seconds)
     fctrl motion_on               # Start automatic path generation motion
     wait _fctrl.motion==0         # Wait until motion path is complete
    
# Escape sequence in the opposite direction for product protection
     fctrl control,cnd=5           # Switch in real time to the workaround condition in the direction opposite to the contact surface (air)
     delay 2                       # Wait until the robot completely detaches from the surface
     
# Safe termination in a non-contact state
     fctrl off                     # Terminate force control (Since it is in a non-contact state, the 0.5-second pause has no impact on the product)
     delay 1
  
end# 6. Monitoring

This monitoring menu allows you to intuitively verify and diagnose the robot's real-time operational status and F/T sensor data while the force control function is running. 

Through real-time data analysis, you can optimize control parameters and safely diagnose abnormal behaviors that may occur during the on-site teaching process.


---


##### **Monitoring Menu Configuration**

Two dedicated monitoring screens are provided depending on the purpose of use. Please select and utilize them according to your task conditions and debugging needs.

###### **[Force Data Monitoring]**
* **Purpose:** Used when you want to check the raw force and torque data measured by the F/T sensor itself.

* **Primary Verification Items:** Verifies the current force data in Cartesian coordinates (X, Y, Z, RX, RY, RZ) based on the designated reference coordinate system.


###### **[Force Motion Monitoring]**
* **Purpose:** Comprehensively diagnoses the real-time pressurizing state, the robot's tracking behavior, speed limit constraints, and contact determination status.

* **Primary Verification Items:** Real-time target force (F), position command (Cmd), maximum limit speed (Vmax), and contact condition threshold matching status (TLT, AVG, HLD).

---

{% hint style="info" %}

**Safety Monitoring Guidelines:** When tuning a new process, it is highly recommended to constantly monitor the **Vmax (Maximum Limit Speed)** and **HLD (Duration)** counts on the `6.2 Force Motion Monitoring` window to check in real time whether the robot is experiencing unintended divergent vibrations or is paused due to a missing contact determination.

{% endhint %}## 6.1 Force Data Monitoring

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

{% endhint %}## 6.2 Force Motion Monitoring

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

{% endhint %}# 7. Errors and Troubleshooting

This section provides the causes and on-site corrective action guides for major exceptional situations (error codes) occurring within the controller and F/T sensor unit during the force control process.

---

##### **[Force Control Exception Situations and Response Guide]**

| Error Code | Error Name & Primary Cause | On-Site Corrective Action Guide |
|:--:|---|---|
| **E0260** | **Force Control Function Disabled**<br>When the force control utilization setting within the system parameters is turned off. | Switch the function utilization setting to **On** in the [System ➔ Application Parameter ➔ Force Control] menu. |
| **E0355** | **Force Control Tool Number Error**<br>When there is no currently loaded tool number information or the designated tool setting within the force control condition (`cnd`) is mismatched. | Verify that a valid tool number is defined in the current teaching program, and reassign the tool parameters within the force control settings. |
| **E1336** | **User Coordinate System Number Error**<br>When the reference coordinate system of the force control condition (`cnd`) is designated as a non-existent user coordinate system. | Verify in the [Coordinate System Settings] menu whether the selected user coordinate system number is properly configured and recorded. |
| **E0259** | F/T Sensor Communication Issue | Inspect the sensor hardware and cable connections. |
| **E0272** | Unsupported Sensor | Contact the customer service center (Sensor Interface implementation required). |
| **E0273** | F/T Sensor Communication Issue | Inspect the sensor hardware and cable connections. |
| **E0274** | F/T Sensor Communication Issue | Inspect the sensor hardware and cable connections. |


* **System Protection Behavior:** Upon the occurrence of any of the exceptional situations listed above, the robot immediately halts pressurizing operations and switches to a **Safe-Stop** state.

---

##### **[Troubleshooting Diagnostic Procedure]**

When an unknown force control error or abnormal behavior occurs on-site, proceed with the diagnosis in the following order:

1. **Inspect F/T Sensor Physical Connections:** Check the LED status on the sensor body connector and the reception line inside the controller.
2. **Verify Software Parameters:** Re-verify the tool data and reference coordinate system assignment numbers inside the currently running program.
3. **Check Communication Quality and Logs:** Verify whether raw sensor data is normally outputting to the monitoring window, and then perform a backup of the controller system log (`Log`).# 8. Release Notes

This section covers the key changes and new feature history for each version of the force control function.

---

##### `V70.02-00`

<br>

* **Added AIDIN F/T Sensor Interface**
  > Official support for the real-time communication protocol of the AIDIN Robotics sensor lineup.
* **Introduced F/T Sensor Offset & Dynamic Load Identification**
  > Added an automatic identification algorithm for tool weight and center of gravity.
* **Applied Soft Start Function**
  > Prevents overshoot and mechanical impact at the moment of initial contact through initial pressurized ramping control.
* **Reflected Real-Time Maximum Speed Limit Profile**
  > Blocks rapid acceleration and control divergence of the robot during steps or surface detachment (non-contact).
* **Provided Dedicated Structure-Type System Variables (_fctrl)**
  > Provides intuitive monitoring variables such as `_fctrl.force_x` (maintains compatibility with legacy `cfo` functions).