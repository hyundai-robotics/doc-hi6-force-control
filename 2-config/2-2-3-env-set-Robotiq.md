## 2.2.3 Robotiq Configuration

Since Robotiq sensors (such as the FT 300S) utilize serial communication (SCI), you must complete both the force control environment configuration and the serial port settings.

---

##### **[Step 1: Force Control Sensor Configuration]**
First, specify the communication protocol as serial communication (SCI) on the force control user environment configuration screen.

![](../_assets/_03_01_fctrl_env_setting_Robotiq_FT300S_SCI.png)

---

##### **[Step 2: Serial Port Environment Configuration]**
To activate serial communication, navigate to the following path and configure the communication port parameters of the controller.

> **[F2: System]** → **2: Control Parameter** → **3: Serial Port** → **1: Environment Settings**

![](../_assets/_03_02_fctrl_env_setting_Robotiq_FT300S_SCI_CFG.png)

{% hint style="info" %}

Instead of entering a separate IP address, it is essential for the Robotiq sensor to match the physical serial port (SCI) channel and Baud rate located on the back or inside of the controller.

After specifying the sensor in Step 1, you must complete the serial port configuration in Step 2 without omission to prevent communication errors from occurring.

{% endhint %}