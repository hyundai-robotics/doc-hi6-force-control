## 5.1 Z-Axis Force Control 

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
fctrl off                           # Terminate force control