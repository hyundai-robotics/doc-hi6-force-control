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