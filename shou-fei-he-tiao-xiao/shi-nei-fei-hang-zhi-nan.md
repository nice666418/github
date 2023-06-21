# 室内飞行指南

本文提供了飞行多旋翼飞行器的重要指南 里面。

警告

* 在室内飞行时，请确保您有足够的空间并跟随 安全程序。
* GPS在室内不起作用，需要禁用。（无例外）

### 概述[¶](https://ardupilot.org/copter/docs/indoor-flying.html#overview)

在室内飞行时的主要注意事项是 全球定位 系统将无法正常工作。即使您看到您拥有正确的号码 的卫星和低 HDOP，这是由于 来自卫星的信号。这意味着单曲正在被反映到 天线通过墙壁、窗户和其他表面从外部。如果你 查看地图上的位置，您会发现该位置不会 匹配您当前的位置，或将漂移，时间数米或 甚至距离您的位置1000米。

### 稳定[¶](https://ardupilot.org/copter/docs/indoor-flying.html#stabilize)

[稳定](https://ardupilot.org/copter/docs/stabilize-mode.html#stabilize-mode)模式不使用GPS，并且作为 问题最少，但飞行员需要对直升机进行良好的控制。

### 海拔保持[¶](https://ardupilot.org/copter/docs/indoor-flying.html#altitude-hold)

[高度](https://ardupilot.org/copter/docs/altholdmode.html#altholdmode)保持模式使用气压计保持 特定海拔高度。气压计依赖于恒定的气压。 房间内的气压会因门的打开或关闭而发生变化。也 风扇和空调等气候控制设备也会导致 压力变化。可能的结果是地板突然坠毁或 天花板。

### 声纳[¶](https://ardupilot.org/copter/docs/indoor-flying.html#sonar)

朝下的[声纳或激光雷达](https://ardupilot.org/copter/docs/common-rangefinder-landingpage.html#common-rangefinder-landingpage)可以帮助避免 在 AltHold 模式下高度突然变化导致撞到 地板或天花板。

### 安全的室内飞行注意事项[¶](https://ardupilot.org/copter/docs/indoor-flying.html#safe-indoor-flying-dos)

* 在非自动\*\*模式下禁用 GPS - 将[AHRS\_GPS\_USE](https://ardupilot.org/copter/docs/parameters.html#ahrs-gps-use)设置为 0
* 仅启用Battery\_failsafe到LAND 或禁用（非 RTL） - 从 Copter-3.6 或更高版本设置[BATT\_FS\_LOW\_ACT](https://ardupilot.org/copter/docs/parameters.html#batt-fs-low-act)参数（对于 Copter-3.5 及更低版本，请使用 FS\_BATT\_ENABLE 参数）
* 将限制故障保护启用为仅 LAND 或禁用（不是 RTL 或继续）- 设置 [FS\_THR\_ENABLE](https://ardupilot.org/copter/docs/parameters.html#fs-thr-enable) = 0 或 3
* 禁用 FENCE - 设置 [FENCE\_ENABLE](https://ardupilot.org/copter/docs/parameters.html#fence-enable) = 0
* 使用声纳（如果可用）

### 安全室内飞行注意事项[¶](https://ardupilot.org/copter/docs/indoor-flying.html#safe-indoor-flying-don-ts)

* 不要在狭小的密闭空间内飞行。使用常识，在里面飞行 高屋顶的仓库=OK，卧室=不OK。
* 不要使用自动\*模式

\*自动模式是需要GPS的模式，即悬停，位置保持， 引导式，自动

\*\* 非自动模式为稳定和高度保持
