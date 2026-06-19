# 6. Monitoring

This monitoring menu allows you to intuitively verify and diagnose the robot's real-time operational status and F/T sensor data while the force control function is running. 

Through real-time data analysis, you can optimize control parameters and safely diagnose abnormal behaviors that may occur during the on-site teaching process.


---


##### **Monitoring Menu Configuration**

Two dedicated monitoring screens are provided depending on the purpose of use. Please select and utilize them according to your task conditions and debugging needs.

###### **[Force Data Monitoring]**
* **Purpose:** Used when you want to check the raw force and torque data measured by the F/T sensor itself.

* **Primary Verification Items:** Verifies the current force data in Cartesian coordinates (X, Y, Z, RX, RY, RZ) based on the designated reference coordinate system.


###### **[Force Motion Monitoring]**
* **Purpose:** Comprehensively diagnoses the real-time pressurizing state, the robot's tracking behavior, speed limit constraints, and contact determination status.

* **Primary Verification Items:** Real-time target force (F), position command (Cmd), maximum limit speed (Vmax), and contact condition threshold matching status (TLT, AVG, HLD).

---

{% hint style="info" %}

**Safety Monitoring Guidelines:** When tuning a new process, it is highly recommended to constantly monitor the **Vmax (Maximum Limit Speed)** and **HLD (Duration)** counts on the `6.2 Force Motion Monitoring` window to check in real time whether the robot is experiencing unintended divergent vibrations or is paused due to a missing contact determination.

{% endhint %}