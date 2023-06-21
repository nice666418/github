# 气压计温度补偿

## 气压计温度补偿[¶](https://ardupilot.org/copter/docs/common-baro-temp-comp.html#barometer-temperature-compensation)

![../\_images/baro-temp-comp.png](https://ardupilot.org/copter/\_images/baro-temp-comp.png)

如果气压计随着温度变化而报告的压力发生显着变化，则一些具有非常紧密组件的小型自动驾驶仪可能会受到高度控制不良的影响。气压计温度补偿功能可用于部分纠正此问题。

警告

此功能对于大多数自动驾驶仪（包括Pixracer和Pixhawk系列板）没有用。

注意

此功能在 Copter-3.6（及更高版本）中可用

### 如何使用[¶](https://ardupilot.org/copter/docs/common-baro-temp-comp.html#how-to-use)

* 将[TCAL\_ENABLED](https://ardupilot.org/copter/docs/parameters.html#tcal-enabled)设置为 2（学习和使用校准）
* 关闭电路板电源，让它冷却几分钟
* 打开电路板电源并放置约 10 分钟
* 学习将在电路板升温且不移动时发生
* 应使用非零值更新[TCAL\_BARO\_EXP](https://ardupilot.org/copter/docs/parameters.html#tcal-baro-exp)
* （可选）通过将[TCAL\_ENABLED](https://ardupilot.org/copter/docs/parameters.html#tcal-enabled)设置为 1 来关闭学习（使用但不学习新的校准值）
