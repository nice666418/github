# 布臂前安全检查

ArduPilot包括一套布臂前安全检查，可以防止 车辆从布防其推进系统，如果存在相当多的问题中的任何一个 在运动前发现，包括错过校准、配置 或错误的传感器数据。这些检查有助于防止崩溃或飞走，但 如有必要，也可以禁用它们。

### 使用 GCS 识别哪个布臂前检查失败[¶](https://ardupilot.org/copter/docs/common-prearm-safety-checks.html#recognising-which-pre-arm-check-has-failed-using-the-gcs)

飞行员会注意到手臂前检查失败，因为他/她会 无法武装车辆，通知 LED（如果有）将闪烁黄色。自 准确确定哪个检查失败：

1. 使用 USB 电缆将自动驾驶仪连接到地面站 或[遥测](https://ardupilot.org/copter/docs/common-telemetry-landingpage.html#common-telemetry-landingpage)。
2. 确保GCS连接到车辆（即执行任务时） 计划并按右上角的“连接”按钮）。
3. 打开无线电发射器并尝试武装车辆 （常规程序是使用油门下降，向右偏航或通过RCx\_OPTION开关）
4. 布臂前检查失败的第一个原因将以红色显示 在 HUD 窗口上

在撤防时，失败的预布防检查也将作为消息发送到 GCS，大约每 30 秒一次。如果您希望禁用此功能并仅在尝试臂失败时才发送它们，请将[ARMING\_OPTIONS](https://ardupilot.org/copter/docs/parameters.html#arming-options)位设置为 1（值 1）。

### 失败消息[¶](https://ardupilot.org/copter/docs/common-prearm-safety-checks.html#failure-messages)

#### 故障保护：[¶](https://ardupilot.org/copter/docs/common-prearm-safety-checks.html#failsafes)

任何故障保护（RC，电池，GCS等）都会显示一条消息并阻止布防。

#### RC 故障：[¶](https://ardupilot.org/copter/docs/common-prearm-safety-checks.html#rc-failures)

**RC未校准**：无线电校准尚未[校准](https://ardupilot.org/copter/docs/common-radio-control-calibration.html#common-radio-control-calibration) 执行。[RC3\_MIN](https://ardupilot.org/copter/docs/parameters.html#rc3-min)和[RC3\_MAX](https://ardupilot.org/copter/docs/parameters.html#rc3-max)必须已从其更改 默认值（1100 和 1900），对于通道 1 到 4，最小值必须为 1300 或更小，最大值必须为 1700 或更大。

#### 气压计故障：[¶](https://ardupilot.org/copter/docs/common-prearm-safety-checks.html#barometer-failures)

气**压不健康 ：气**压计传感器报告它是 不正常，这通常是硬件故障的迹象。

**替代视差**：气压计高度与惯性不一致 导航（即气压+加速度计）高度估计超过1 米。此消息通常是短暂的，并且可能在以下情况下发生 自动驾驶仪首先插入或是否收到剧烈颠簸 （即突然下降）。如果不清楚加速度[计可能需要校准](https://ardupilot.org/copter/docs/common-accelerometer-calibration.html#common-accelerometer-calibration)，或者可能存在 是晴雨表硬件问题。

#### 指南针故障：[¶](https://ardupilot.org/copter/docs/common-prearm-safety-checks.html#compass-failures)

指南针**不健康：指南针**传感器报告它是 不正常，这是硬件故障的迹象。

指南针未校准：[指南针尚未校准](https://ardupilot.org/copter/docs/common-compass-calibration-in-mission-planner.html#common-compass-calibration-in-mission-planner)。参数为零或数字或类型 自上次指南针校准以来，连接的指南针已更改 进行了。`COMPASS_OFS_X, _Y, _Z`

指南针偏移**量过高：主指南针的偏移**长度 （即 sqrt（x^2+y^2+z^2）） 大于 500。这可能是由以下原因引起的 金属物体放置在离指南针太近的地方。如果只有一个 正在使用内部指南针（不推荐），它可能只是 电路板中的金属导致较大的偏移，这可能不会 实际上是一个问题，在这种情况下，您可能希望禁用指南针 检查。

**检查磁场**：该区域感应磁场为35% 高于或低于预期值。预期长度为 530 所以 > 874 或 < 185。磁场强度在世界各地各不相同 但这些广泛的限制意味着[指南针校准](https://ardupilot.org/copter/docs/common-compass-calibration-in-mission-planner.html#common-compass-calibration-in-mission-planner)更有可能没有 计算出良好的偏移量，应重复。

**指南针不一致**：内部和外部指南针是 指向不同的方向（偏离 >45 度）。这通常是 由于外部罗盘方向（即[COMPASS\_ORIENT](https://ardupilot.org/copter/docs/parameters.html#compass-orient)参数）设置不正确。

#### 全球定位系统相关故障：[¶](https://ardupilot.org/copter/docs/common-prearm-safety-checks.html#gps-related-failures)

GPS**故障**：[GPS毛刺](https://ardupilot.org/copter/docs/gps-failsafe-glitch-protection.html#gps-failsafe-glitch-protection)和车辆 处于需要 GPS（即徘徊、PosHold 等）和/或 [圆柱形围栏](https://ardupilot.org/copter/docs/common-ac2\_simple\_geofence.html#common-ac2-simple-geofence)已启用。

需要3D修复：GPS没有**3D**定位，车辆处于 启用需要 GPS 和/或[圆柱形围栏](https://ardupilot.org/copter/docs/common-ac2\_simple\_geofence.html#common-ac2-simple-geofence)的飞行模式。

**不良速度**：车辆的速度（根据惯性 导航系统）高于50厘米/秒。可能导致此问题的问题 包括实际移动或掉落的车辆，不良加速度计 校准，GPS 更新低于预期的 5hz。

高 GPS HDOP ：**GPS 的 HDOP** 值（位置的度量） 精度）高于 2.0，飞行器处于飞行模式，需要 GPS 和/或[圆柱形围栏](https://ardupilot.org/copter/docs/common-ac2\_simple\_geofence.html#common-ac2-simple-geofence)已启用。 这可以通过简单地等待几分钟来解决，移动到 位置，可以更好地欣赏天空或检查GPS来源 干扰（即 FPV 设备）远离 GPS。 或者，可以通过将[GPS\_HDOP\_GOOD](https://ardupilot.org/copter/docs/parameters.html#gps-hdop-good)参数增加到 2.2 或 2.5 来放宽检查。在最坏的情况下，飞行员可能会禁用围栏和 以不需要 GPS 的模式起飞（即稳定， AltHold）并在布防后切换到Loiter，但这不是 推荐。

注意：GPS HDOP可以通过任务规划器的轻松查看 快速选项卡如下所示。

<figure><img src="https://ardupilot.org/copter/_images/MP_QuicHDOP.jpg" alt=""><figcaption></figcaption></figure>

#### INS检查（即加速度计和陀螺仪检查）：[¶](https://ardupilot.org/copter/docs/common-prearm-safety-checks.html#ins-checks-i-e-acclerometer-and-gyro-checks)

**INS 未校准**：加速度计的部分或全部偏移量为 零。[加速度计需要校准](https://ardupilot.org/copter/docs/common-accelerometer-calibration.html#common-accelerometer-calibration)。

加速度不正常：其中一个加速度计报告它不**正常** 健康，这可能是硬件问题。这也可能发生 在重新启动主板之前进行固件更新后立即进行。

加速度不一致：加速度计报告**加速度** 相差至少 1m/s/s。[加速度计需要重新校准](https://ardupilot.org/copter/docs/common-accelerometer-calibration.html#common-accelerometer-calibration)，否则 硬件问题。

陀螺仪**不健康：其中一个陀螺仪**报告它是 不正常，这可能是硬件问题。这也可能发生 在重新启动主板之前进行固件更新后立即进行。

陀螺仪校准**失败：陀螺仪校准**无法捕获偏移。 这通常是由陀螺仪期间移动的车辆引起的 校准（当红灯和蓝灯闪烁时），在这种情况下 拔下电池并再次插入，同时注意不要 推挤车辆可能会解决问题。传感器硬件 故障（即峰值）也可能导致此故障。

陀螺仪不一致：两台**陀螺仪**报告车辆旋转 速率相差超过 20 度/秒。这可能是硬件 故障或由陀螺仪校准不良导致。

#### 板电压检查：[¶](https://ardupilot.org/copter/docs/common-prearm-safety-checks.html#board-voltage-checks)

**检查**电路板电压：电路板的内部电压低于 4.3 伏 或高于 5.8 伏。

如果通过USB电缆供电（即在工作台上），这可能是 由于台式计算机无法提供足够的 当前到自动驾驶仪 - 尝试更换 USB 电缆。

如果由电池供电，这是一个严重的问题，电源系统 （即电源模块、电池等）在检查前应仔细检查 飞行。

#### 参数检查：[¶](https://ardupilot.org/copter/docs/common-prearm-safety-checks.html#parameter-checks)

**Ch7和Ch8 Opt不能相同**：[辅助功能开关](https://ardupilot.org/copter/docs/channel-7-and-8-options.html#channel-7-and-8-options)设置为不允许的相同选项，因为它可能导致混淆。

**检查FS\_THR\_VALUE**：[无线电故障保护PWM值](https://ardupilot.org/copter/docs/radio-failsafe.html#radio-failsafe)设置得太接近节流通道（即通道3）最小值。

**检查ANGLE\_MAX** [ANGLE\_MAX](https://ardupilot.org/copter/docs/parameters.html#angle-max)：控制 车辆的最大倾斜角度已设置为10度以下（即1000度） 或80度以上（即8000度）。

**ACRO\_BAL\_ROLL/节距**：[ACRO\_BAL\_ROLL](https://ardupilot.org/copter/docs/parameters.html#acro-bal-roll)参数高于 稳定辊 P 和/或[ACRO\_BAL\_PITCH](https://ardupilot.org/copter/docs/parameters.html#acro-bal-pitch)参数高于 稳定音高 P 值。这可能导致飞行员无法 在ACRO模式下控制倾斜角度，因为[Acro教练机稳定](https://ardupilot.org/copter/docs/acro-mode.html#acro-mode-acro-trainer)会压倒飞行员的 输入。

#### 电池/电源监视器：[¶](https://ardupilot.org/copter/docs/common-prearm-safety-checks.html#battery-power-monitor)

如果电源监视器电压低于其故障安全低电压或临界电压或故障安全剩余容量低或临界设定点，则此检查将失败并指示其低于哪个设定点。如果这些设定点反转，即临界点高于低点，它也将失败。有关这些内容的更多信息，请参阅直升机的电池故障保护、飞机的飞机故障保护功能或漫游车的[故障保护](https://ardupilot.org/plane/docs/apms-failsafe-function.html#apms-failsafe-function)。

此外，可以为每个电池/电源监视器设置最小布防电压和剩余容量参数，例如第一个电池的[BATT\_ARM\_VOLT](https://ardupilot.org/copter/docs/parameters.html#batt-arm-volt)和[BATT\_ARM\_MAH](https://ardupilot.org/copter/docs/parameters.html#batt-arm-mah)，以检查电池不仅高于故障安全水平，而且还有足够的运行容量。

#### 空速：[¶](https://ardupilot.org/copter/docs/common-prearm-safety-checks.html#airspeed)

如果配置了空速传感器，并且它未提供读数或校准失败，则此检查将失败。

#### 伐木：[¶](https://ardupilot.org/copter/docs/common-prearm-safety-checks.html#logging)

日志记录失败：已启用预布防**日志记录**，但无法写入日志。

无 SD 卡：已启用日志记录，但未检测到 **SD 卡**。

#### 安全开关：[¶](https://ardupilot.org/copter/docs/common-prearm-safety-checks.html#safety-switch)

硬件安全开关：未按下**硬件安全开关**。

#### 系统：[¶](https://ardupilot.org/copter/docs/common-prearm-safety-checks.html#system)

参数存储失败：检查读取**参数存储区域失败**。

内部错误 **（0xx）：发生内部错误**。[在此处](https://github.com/ArduPilot/ardupilot/issues/15916)向 ArduPilot 开发团队报告

**KDECAN 失败：KDECAN** 系统故障。

**DroneCAN 失败：DroneCAN** 系统故障。

#### 任务：[¶](https://ardupilot.org/copter/docs/common-prearm-safety-checks.html#mission)

请参阅[ARMING\_MIS\_ITEMS](https://ardupilot.org/copter/docs/parameters.html#arming-mis-items)

**不存在任务库**：已启用任务检查，但未加载任何任务。

**不存在拉力赛库**：已启用集结点检查，但未加载集结点。

**缺少任务项目： xxxx：**缺少必需的任务项目。

#### 测距：[¶](https://ardupilot.org/copter/docs/common-prearm-safety-checks.html#rangefinder)

如果配置了测距仪，则发生报告错误。

### 禁用布防前安全检查[¶](https://ardupilot.org/copter/docs/common-prearm-safety-checks.html#disabling-the-pre-arm-safety-check)

警告

不建议禁用布臂前安全检查。如果可能，应在车辆运行前纠正前臂故障的原因。如果您确信布臂前检查失败不是真正的问题，则可以禁用失败的检查。

可以通过将 [ARMING\_CHECK](https://ardupilot.org/copter/docs/parameters.html#arming-check) 参数设置为 1 以外的参数来单独禁用布防检查。设置为 0 将完全删除所有布防前检查。例如，设置为 4 仅检查 GPS 是否已锁定。

这也可以使用任务规划器进行配置：

<figure><img src="https://ardupilot.org/copter/_images/MP_PreArmCheckDisable.png" alt=""><figcaption></figcaption></figure>

* 将自动驾驶仪连接到任务规划器
* 转到任务规划器的配置/调整>>标准参数屏幕
* 将“布防检查”下拉列表设置为“已禁用”或“跳过”之一 更有效地跳过导致失败的项目的选项。
* 按下“写入参数”按钮
