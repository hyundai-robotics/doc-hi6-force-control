### 4.3 Filtering

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

* **Mitigation Method:** Refer