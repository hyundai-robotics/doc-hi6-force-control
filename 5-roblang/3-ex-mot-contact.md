## 5.3 Contact Surface Detection Function 

The following is an example of a Job program that uses the **contact surface detection function** on a robot.

---

##### **[Operation Overview]**

Configure the **contact** conditions in the **settings** as follows:

- Example: If contact is maintained based on the criteria below for 5 seconds, the contact surface detection is determined as OK.

| Item | UI Value |
|---|---|
| Force Error | 3 N |
| Force Direction Variation | 20 deg |
| Contact Angle | 40 deg |
| Duration | 5 sec |


---

##### **[JOB Program]**

```python
delay 1.0                            # Stabilization wait before starting control
fctrl on,cnd=1                       # Start force control (Uses condition number 1)
delay 0.5                            # Wait for 0.5 seconds before executing the contact surface detection condition

wait _fctrl.contact, 20              # Execute contact surface detection condition, wait until contact surface detection is OK, check for a maximum of 20 seconds

fctrl off                            # Terminate force control