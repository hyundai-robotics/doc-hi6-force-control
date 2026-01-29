## 3.1 Example: Z-Axis Force Control

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
