## 2.2 Force Control Environment Setup

To use sensor-based force control functions, the following key items must be configured.  
These settings serve as the **starting point** for all controller operations. 

You can access the Force Control Environment Setup through the following path: 

`[F2: System] – 4: Application Parameters – 8: Force Control – 1: User Environment Setup`

<br>

---


### **Enable Function**

Set whether to use the sensor-based force control function.

- Enable: Function **Activated**
- Disable: Function **Deactivated**

The setting must be set to Enable for the force control function to operate.

<br>

---

### **Sensor Manufacturer and Model**

Select the **manufacturer and model of the force sensor** to be used.

- Examples:
  - ATI: Standard ATI models
  - ATI: Delta-SI-660-60
  - ATI: Theta-SI2500-400
  - ATI: Omega-SI7200-1400 
  - OnRobot: HEX-E 
  - Robotiq: FT-300S 

The **data format and communication method** vary depending on the sensor, so an accurate selection is required.

{% hint style="info" %}

The following ATI models are supported in **version V60.32-05 or later**.  
- Standard ATI models  
- Theta-SI2500-400  
- Omega-SI7200-1400

{% endhint %}

<br>

--- 

### **Communication Protocol**

Set the **communication method** provided by the selected sensor.

- UDP
- SCI
- TCP

Configure the port settings and internal parsing methods according to the protocol as follows:

<br>

--- 

### **Configuration Method by ATI Model**

- **Communication Protocol**: UDP
- **IP Address**: 192.168.1.2
- **Remote Port**: 49152

<br>

#### **ATI(Delta-SI-660-60)**  

![](../_assets/_01_01_fctrl_env_setting_ATI_Delta_UDP.png)

<br>

#### **ATI(Theta-SI2500-400)**
![](../_assets/_01_02_fctrl_env_setting_ATI_Theta_UDP.png)

<br>

#### **ATI(Omega-SI7200-1400)**
![](../_assets/_01_03_fctrl_env_setting_ATI_Omega_UDP.png)

<br>

#### **ATI(Generic ATI Model)**
![](../_assets/_01_04_fctrl_env_setting_ATI_Generic_UDP.png)

- Instead of registering models individually, this method involves the **user manually entering and applying the scaling values provided by ATI for each specific model.**

<br>

---

### **OnRobot HEX-E Configuration Method**

- **Communication Protocol**: UDP
- **IP Address**: 192.168.1.1
- **Remote Port**: 49152

![](../_assets/_02_fctrl_env_setting_OnRobot_HEX_E_UDP.png)


<br>


---

### **SCI Communication Method: Robotiq(FT-300S)**
![](../_assets/_03_01_fctrl_env_setting_Robotiq_FT300S_SCI.png)

`[F2: System] – 2: Control Parameters – 3: Serial Port – 1: Configuration`

![](../_assets/_03_02_fctrl_env_setting_Robotiq_FT300S_SCI_CFG.png)

<br>


---


{% hint style="info" %}
 
- These settings are examples based on standard models.  
- **Some ATI models may use network values that differ from the settings above.**

{% endhint %}

