## 5.5 Continuous Switching of Control Conditions Using For Loop

This is an example of sequentially and automatically switching multiple force control conditions (`cnd`) using a `for` loop statement in the robot script language.

---

##### **[Precautions During Manual Mode Step Forward/Backward]**

* **Mandatory Prior Variable Declaration:** If a variable is specified as an argument in the program, such as `fctrl on, cnd=idx_cnd`, the controller will only recognize it normally if the corresponding variable is declared and initialized beforehand (`var idx_cnd=1`).
* **Cause of Error:** If you execute only the `fctrl on` command line independently via manual step (forward/backward) without running the variable initialization line, the controller cannot determine whether the value assigned to the `idx_cnd` variable is valid (i.e., whether it is a registered condition number in the UI). As a result, it interprets it as an unknown value (garbage value) in memory, which **causes a system error**.
* **Corrective Action:** When testing or verifying line operations manually, always execute the variable initialization statement (`var idx_cnd=1`) first to assign a valid condition number to the variable before running the `fctrl on` line.


---

##### **[JOB Program]** 

```python
S1   move P,spd=5%,accu=0,tool=0  
S2   move L,spd=5%,accu=0,tool=0   # Move to home position and approach position
     delay 2
     
     var idx_cnd=1                 # Declare force control condition number variable
     for idx_cnd=1 to 3            # Loop operation: Sequentially apply registered force control conditions 1 through 3 

       delay 3
       fctrl on,cnd=idx_cnd
       delay 20
       fctrl off
S3   move L,spd=5%,accu=0,tool=0  

     next
     
     end