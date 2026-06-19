# 8. Release Notes

This section covers the key changes and new feature history for each version of the force control function.

---

##### `V70.02-00`

<br>

* **Added AIDIN F/T Sensor Interface**
  > Official support for the real-time communication protocol of the AIDIN Robotics sensor lineup.
* **Introduced F/T Sensor Offset & Dynamic Load Identification**
  > Added an automatic identification algorithm for tool weight and center of gravity.
* **Applied Soft Start Function**
  > Prevents overshoot and mechanical impact at the moment of initial contact through initial pressurized ramping control.
* **Reflected Real-Time Maximum Speed Limit Profile**
  > Blocks rapid acceleration and control divergence of the robot during steps or surface detachment (non-contact).
* **Provided Dedicated Structure-Type System Variables (_fctrl)**
  > Provides intuitive monitoring variables such as `_fctrl.force_x` (maintains compatibility with legacy `cfo` functions).