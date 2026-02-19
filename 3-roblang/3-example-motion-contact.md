## 3.3 Example: Contact Surface Detection

The following is a Job program example for using the **Contact Surface Detection** function in the robot. 

<br>

---

### **Operation Overview**

Configure the **Contact Check** conditions in the **Settings** as follows:

- **Criteria**: If contact is maintained according to the standards below for 5 seconds, the contact surface detection is confirmed (OK).

| Item | Value |
|------------------|---------|
| Force Error (Thresh) | 3 N |
| Force Direction Change (Dev Angle) | 20 deg |
| Contact Angle (Tilt Angle) | 40 deg |
| Confirmation Time | 5 sec |

<br> 

---

### **JOB Program Example** 

```python
delay 1.0                           # Wait for stabilization before starting control
fctrl on, cnd=1                     # Start force control (Using condition set No. 1)
delay 0.5                           # Wait 0.5s before executing contact detection

wait contact_state()                # Execute contact detection; wait until "OK"

fctrl off                           # End force control

