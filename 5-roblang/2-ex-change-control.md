## 5.2 Changing Control Settings 

The following is a Job program example that **modifies only the 'Control' items among the force control conditions** on a robot.  
This approach is useful when you want to change only the external force response characteristics during real-time operation while keeping the filter, coordinate system, and motion settings as they are.

---

##### **[Operation Overview]**

- fctrl on,cnd=2: Applies the entire configuration set number 2 when starting force control.
- fctrl control,cnd=1: Changes **only the control parameters** to configuration set number 1.  
  (The coordinate system, filter, motion, etc., remain in the state configured by set number 2.)

---

##### **[JOB Program]** 

```python
delay 1.0                           # Stabilization wait before starting control
fctrl on,cnd=2                      # Start force control (Uses condition number 2)
delay 0.5

fctrl control,cnd=1                 # Change force control configuration (control parameters only) (Uses condition number 1)

delay 5                             # Wait for external force stabilization
fctrl off                           # Terminate force control