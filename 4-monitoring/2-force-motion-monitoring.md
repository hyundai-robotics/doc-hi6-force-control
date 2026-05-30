## 4.2 Force Motion Monitoring

This function allows for real-time monitoring of the external forces applied to the robot, the error relative to the target force, and the commanded position during operation.

<br>

--- 

![](../_assets/_17_fctrl_ctrl_panel_force_motion.png)

| Item | Description |
|--------------|------|
| **Fext** | Force Error (Error between target force and external force) [N or Nm] |
| **Cmd** | Command Position for force control (mm or deg) |

- The coordinate system for **Fext** and **Cmd** follows the coordinate system selected in the settings (cnd).
- This data is only active while **fctrl on** is in effect.

<br>

--- 

{% hint style="info" %}

**TP Navigation Path**

[pane layout] - [F1: select] - [force motion]

{% endhint %}