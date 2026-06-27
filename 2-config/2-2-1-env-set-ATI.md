## 2.2.1 ATI 配置

ATI 传感器的特定模型配置方法和通信参数如下。

---

##### **[默认通信参数]**
所有 ATI 传感器模型使用以下相同的通信设置。

* **协议:** UDP
* **IP 地址:** 192.168.1.2
* **远程端口:** 49152

---

##### **[特定模型配置方法]** <br>

##### **1. ATI (通用模型)**
此方法不会单独注册个别模型，而是 **用户手动输入并应用 ATI 提供的特定模型缩放值**。

![](../_assets/_01_04_fctrl_env_setting_ATI_Generic_UDP.png)

---

##### **2. ATI (Delta-SI-660-60)**
通过使用控制器中预注册的专用 Delta 模型配置文件，相应模型的优化缩放值将自动应用。

![](../_assets/_01_01_fctrl_env_setting_ATI_Delta_UDP.png)

---

##### **3. ATI (Theta-SI2500-400)**
通过使用控制器中预注册的专用 Theta 模型配置文件，相应模型的优化缩放值将自动应用。

![](../_assets/_01_02_fctrl_env_setting_ATI_Theta_UDP.png)

---

##### **4. ATI (Omega-SI7200-1400)**
通过使用控制器中预注册的专用 Omega 模型配置文件，相应模型的优化缩放值将自动应用。

![](../_assets/_01_03_fctrl_env_setting_ATI_Omega_UDP.png)

{% hint style="info" %}

由于 Delta、Theta 和 Omega 模型（不包括通用模型）提供预定义参数，因此可以防止因输入错误的缩放值而导致的故障。

{% endhint %}