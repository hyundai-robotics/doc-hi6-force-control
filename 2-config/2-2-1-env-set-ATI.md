## 2.2.1 ATI 환경 설정

ATI 센서의 모델별 설정 방법 및 통신 파라미터는 다음과 같습니다.

### **[기본 통신 파라미터]**
모든 ATI 센서 모델은 아래의 동일한 통신 설정을 사용합니다.

* **통신 프로토콜:** UDP
* **IP 주소:** 192.168.1.2
* **원격 포트:** 49152

---

### **[모델별 설정 방법]**

#### **1. ATI (일반 모델)**
모델을 별도로 개별 등록하지 않고, **ATI에서 제공하는 모델별 스케일링 값을 사용자가 직접 수동으로 입력**하여 적용하는 방식입니다.

![ATI 일반 모델 설정](../_assets/_01_04_fctrl_env_setting_ATI_Generic_UDP.png)

<br>

#### **2. ATI (Delta-SI-660-60)**
제어기에 사전 등록된 Delta 모델 전용 프로파일을 사용하여, 해당 모델에 최적화된 스케일링 값이 자동으로 적용됩니다.

![ATI Delta 설정](../_assets/_01_01_fctrl_env_setting_ATI_Delta_UDP.png)

<br>

#### **3. ATI (Theta-SI2500-400)**
제어기에 사전 등록된 Theta 모델 전용 프로파일을 사용하여, 해당 모델에 최적화된 스케일링 값이 자동으로 적용됩니다.

![ATI Theta 설정](../_assets/_01_02_fctrl_env_setting_ATI_Theta_UDP.png)

<br>

#### **4. ATI (Omega-SI7200-1400)**
제어기에 사전 등록된 Omega 모델 전용 프로파일을 사용하여, 해당 모델에 최적화된 스케일링 값이 자동으로 적용됩니다.

![ATI Omega 설정](../_assets/_01_03_fctrl_env_setting_ATI_Omega_UDP.png)

{% hint style="info" %}

> **참고**
> 일반(Generic) 모델을 제외한 Delta, Theta, Omega 모델은 사전 정의된 파라미터를 제공하므로, 스케일링 값 오입력으로 인한 오작동을 방지할 수 있습니다.

{% endhint %}