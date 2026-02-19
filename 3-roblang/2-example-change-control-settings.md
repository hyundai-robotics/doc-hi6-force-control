## 3.2 Example: Modifying Control Settings

The following is a Job program example for **modifying only the 'Control' parameters** within the force control conditions.  
This method is useful when you want to change only the external force response characteristics during real-time operation while maintaining other settings such as filters, coordinate systems, and motion profiles.

<br>

---

### **Operation Overview**

- **fctrl on, cnd=2**: Applies the complete configuration from set No. 2 when starting force control.
- **fctrl control, cnd=1**: Changes **only the 'Control' parameters** to those of set No. 1.
  (Other settings such as coordinate system, filters, and motion profiles remain as they were in set No. 2.)

<br>

---

### **JOB Program Example**

```python
delay 1.0                           # Wait for stabilization before starting control
fctrl on, cnd=2                     # Start force control (Initial: Using set No. 2)
delay 0.5

fctrl control, cnd=1                # Update ONLY 'Control' parameters (Switch to set No. 1)
                                    # (Coordinates, Filters, and Motion remain from No. 2)

delay 5                             # Wait for stabilization of external force
fctrl off                           # End force control
