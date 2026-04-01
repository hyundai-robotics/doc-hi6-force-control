## 2.3 Force Control Tool Information

By entering the physical characteristics of the tool mounted on the robot, the accuracy of the force control algorithm is improved.  
The force and torque perceived by the sensor are calibrated based on the tool's weight and center of gravity coordinates. 

The Force Control Tool Information setup can be accessed through the following path: 

`[F2: System] – 4: Application Parameters – 24: Force Control – 2: Force Control Tool Data`

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