## 2.2 力控制环境设置

要使用基于传感器的力控制功能，必须配置以下关键项目。  
这些设置作为所有控制器操作的**起始点**。

您可以通过以下路径访问力控制环境设置：

`[F2: System] – 4: Application Parameters – 17: Force Control – 1: User Environment Setup`

<br>

---


### **启用功能**

设置是否使用基于传感器的力控制功能。

- 启用：功能**已激活**
- 禁用：功能**已停用**

力控制功能的操作必须设置为启用。

<br>

---

### **传感器制造商和型号**

选择要使用的**力传感器的制造商和型号**。

- 示例：
  - ATI：标准ATI型号
  - ATI：Delta-SI-660-60
  - ATI：Theta-SI2500-400
  - ATI：Omega-SI7200-1400 
  - OnRobot：HEX-E 
  - Robotiq：FT-300S 

**数据格式和通信方式**因传感器而异，因此需要准确选择。

{% hint style="info" %}

以下ATI型号在**版本V60.32-05或更高版本**中受支持。  
- 标准ATI型号  
- Theta-SI2500-400  
- Omega-SI7200-1400

{% endhint %}
--- 

### **通信协议**

设置所选传感器提供的**通信方法**。

- UDP
- SCI
- TCP

根据协议配置端口设置和内部解析方法如下：

<br>

--- 

### **按ATI模型的配置方法**

- **通信协议**：UDP
- **IP地址**：192.168.1.2
- **远程端口**：49152

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

#### **ATI(通用ATI模型)**
![](../_assets/_01_04_fctrl_env_setting_ATI_Generic_UDP.png)

- 此方法不需要单独注册模型，而是**用户手动输入并应用ATI为每个特定模型提供的缩放值。**

<br>

---
### **OnRobot HEX-E 配置方法**

- **通信协议**: UDP
- **IP 地址**: 192.168.1.1
- **远程端口**: 49152

![](../_assets/_02_fctrl_env_setting_OnRobot_HEX_E_UDP.png)


<br>


---

### **SCI 通信方法: Robotiq(FT-300S)**
![](../_assets/_03_01_fctrl_env_setting_Robotiq_FT300S_SCI.png)

`[F2: 系统] – 2: 控制参数 – 3: 串口 – 1: 配置`

![](../_assets/_03_02_fctrl_env_setting_Robotiq_FT300S_SCI_CFG.png)

<br>


---


{% hint style="info" %}
 
- 这些设置是基于标准模型的示例。  
- **某些 ATI 模型可能使用与上述设置不同的网络值。**

{% endhint %}