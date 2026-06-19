## 3.2 Dynamic Load Identification

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

---