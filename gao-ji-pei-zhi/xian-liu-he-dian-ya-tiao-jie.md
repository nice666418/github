# 限流和电压调节

## 限流和电压调节[¶](https://ardupilot.org/copter/docs/current-limiting-and-voltage-scaling.html#current-limiting-and-voltage-scaling)

直升机包括_电流限制_，以保护电池免受 损坏和_电压缩放_，以补偿压降，因为 电池电量耗尽。这两个功能都需要车辆具有 [电源模块或其他电压和电流监视器](https://ardupilot.org/copter/docs/common-powermodule-landingpage.html#common-powermodule-landingpage)。

注意

在 Copter 中引入了电流限制和电压缩放 3.3.

### 限流[¶](https://ardupilot.org/copter/docs/current-limiting-and-voltage-scaling.html#current-limiting)

这种保护会自动将油门降低到低至 60% 全油门以限制从电池请求的电流。 这对于保护电池免受损坏很有用。

要启用该功能，请将[MOT\_BAT\_CURR\_MAX](https://ardupilot.org/copter/docs/parameters.html#mot-bat-curr-max)参数设置为所需的 以安培为单位的限制（或“0”表示禁用此功能）。

[![../\_images/CurrentLimiting\_MPSetup.png](https://ardupilot.org/copter/\_images/CurrentLimiting\_MPSetup.png)](https://ardupilot.org/copter/\_images/CurrentLimiting\_MPSetup.png)

如果测量的电流超过此限制，则最大油门将为 在 1 到 5 秒内降低到安全水平（取决于超过多远 极限）。因为可以在短时间内超过限制 时间，限制应设置在电池爆裂之间的某个地方 限制及其绝对上限。

### 电压调节[¶](https://ardupilot.org/copter/docs/current-limiting-and-voltage-scaling.html#voltage-scaling)

如果启用，此功能将增加横滚、俯仰和偏航控制 增益，用于补偿电池耗尽时的压降。这 有助于确保车辆的姿态控制 不会随着电池的减弱而退化。

要启用，请将[MOT\_BAT\_VOLT\_MAX](https://ardupilot.org/copter/docs/parameters.html#mot-bat-volt-max)设置为电池的完全充电 电压（即 12S 电池为 6.3）。收益将按比例调整以尝试 以保持充满电时的姿态控制响应。

[将MOT\_BAT\_VOLT\_MIN](https://ardupilot.org/copter/docs/parameters.html#mot-bat-volt-min)设置为车辆将达到的最小电池电压 通常经验。收益将不再扩大，因为 电压低于此水平。将其设置为[电池故障保护电压](https://ardupilot.org/copter/docs/failsafe-battery.html#failsafe-battery)是一个良好的开端。

[![../\_images/VoltageScaling\_MPSetup.png](https://ardupilot.org/copter/\_images/VoltageScaling\_MPSetup.png)](https://ardupilot.org/copter/\_images/VoltageScaling\_MPSetup.png)
