## 5.4 Spiral Motion 

The following is an example of a Job program that uses **Spiral Motion** on a robot.  
This example is designed to execute tasks while maintaining an **external force applied along the Z-axis at 20N**.

---

##### **[Operation Overview]**

- The **motion type** must be configured to Spiral in the **settings**. 

- Including a mandatory delay command before the fctrl motion_on command helps suppress vibrations, enabling more stable force control operation.

---

##### **[JOB Program]** 

```python
delay 1.0                            # Stabilization wait before starting control
fctrl on,cnd=1                       # Start force control (Uses condition number 1)
delay 0.5                            # Wait before starting spiral motion

fctrl motion_on                      # Start spiral motion
wait _fctrl.motion==0                # Wait until spiral motion terminates
fctrl motion_off                     # Terminate spiral motion

fctrl off                            # Terminate force control