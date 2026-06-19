## 2.2 F/T Sensor Communication Settings

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
| **Network Parameters** | • **IP Address:** Enter the unique IP address assigned to the F/T sensor controller.<br>• **Local Port:** The data reception port number on the robot controller side. (Mainly 50001, 50100 are used)<br>• **Remote Port:** The data transmission port number on the F/T sensor side. (Enter the fixed port specified in the manufacturer's specification manual) |