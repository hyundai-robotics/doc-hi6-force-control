# 7. Errors and Troubleshooting

This section provides the causes and on-site corrective action guides for major exceptional situations (error codes) occurring within the controller and F/T sensor unit during the force control process.

---

##### **[Force Control Exception Situations and Response Guide]**

| Error Code | Error Name & Primary Cause | On-Site Corrective Action Guide |
|:--:|---|---|
| **E0260** | **Force Control Function Disabled**<br>When the force control utilization setting within the system parameters is turned off. | Switch the function utilization setting to **On** in the [System ➔ Application Parameter ➔ Force Control] menu. |
| **E0355** | **Force Control Tool Number Error**<br>When there is no currently loaded tool number information or the designated tool setting within the force control condition (`cnd`) is mismatched. | Verify that a valid tool number is defined in the current teaching program, and reassign the tool parameters within the force control settings. |
| **E1336** | **User Coordinate System Number Error**<br>When the reference coordinate system of the force control condition (`cnd`) is designated as a non-existent user coordinate system. | Verify in the [Coordinate System Settings] menu whether the selected user coordinate system number is properly configured and recorded. |
| **E0259** | F/T Sensor Communication Issue | Inspect the sensor hardware and cable connections. |
| **E0272** | Unsupported Sensor | Contact the customer service center (Sensor Interface implementation required). |
| **E0273** | F/T Sensor Communication Issue | Inspect the sensor hardware and cable connections. |
| **E0274** | F/T Sensor Communication Issue | Inspect the sensor hardware and cable connections. |


* **System Protection Behavior:** Upon the occurrence of any of the exceptional situations listed above, the robot immediately halts pressurizing operations and switches to a **Safe-Stop** state.

---

##### **[Troubleshooting Diagnostic Procedure]**

When an unknown force control error or abnormal behavior occurs on-site, proceed with the diagnosis in the following order:

1. **Inspect F/T Sensor Physical Connections:** Check the LED status on the sensor body connector and the reception line inside the controller.
2. **Verify Software Parameters:** Re-verify the tool data and reference coordinate system assignment numbers inside the currently running program.
3. **Check Communication Quality and Logs:** Verify whether raw sensor data is normally outputting to the monitoring window, and then perform a backup of the controller system log (`Log`).