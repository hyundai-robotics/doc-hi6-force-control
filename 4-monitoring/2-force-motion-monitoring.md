## 4.2 力量运动监控

此功能允许实时监控施加在机器人上的外部力量、相对于目标力的误差以及操作过程中命令的位置。

<br>

--- 

![](../_assets/_17_fctrl_ctrl_panel_force_motion.png)

| 项目 | 描述 |
|--------------|------|
| **Fext** | 力量误差（目标力量与外部力量之间的误差）[N 或 Nm] |
| **Cmd** | 力量控制的命令位置（mm 或度） |

- **Fext** 和 **Cmd** 的坐标系统遵循设置中选择的坐标系统（cnd）。
- 此数据仅在 **fctrl on** 处于有效状态时激活。

<br>

--- 

{% hint style="info" %}

**TP导航路径**

[pane layout] – [F1: select] – [force motion]

{% endhint %}