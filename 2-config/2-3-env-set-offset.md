## 2.3 F/T Sensor Offset Settings

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

{% endhint %}