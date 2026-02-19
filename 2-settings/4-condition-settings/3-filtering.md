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
