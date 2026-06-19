### 4.4.1 Profile: Soft Start

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

{% endhint %}