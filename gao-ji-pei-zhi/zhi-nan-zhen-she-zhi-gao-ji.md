# 指南针设置（高级）

## 高级指南针设置[¶](https://ardupilot.org/copter/docs/common-compass-setup-advanced.html#advanced-compass-setup)

本文提供有关如何设置系统指南针和高级指南针相关功能的高级指南。

提示

只有内部指南针或使用UBlox GPS +指南针组合的外部指南针（如[UBlox GPS +](https://ardupilot.org/copter/docs/common-installing-3dr-ublox-gps-compass-module.html#common-installing-3dr-ublox-gps-compass-module)指南针模块）并将其安装在默认方向的用户通常可以执行简单的“板载校准”，如[指南针校准](https://ardupilot.org/copter/docs/common-compass-calibration-in-mission-planner.html#common-compass-calibration-in-mission-planner)中所述）。

### 概述[¶](https://ardupilot.org/copter/docs/common-compass-setup-advanced.html#overview)

准确设置指南针至关重要，因为它是主要的 标题信息的来源。没有准确的航向车辆 在自动驾驶模式下不会以正确的方向移动（即自动， LOITER、PosHold、RTL 等）。这可能导致盘旋（又名 “马桶保龄球”）或飞走。

ArduPilot允许连接多个指南针，但一次只能使用三个指南针。通常，只使用主指南针，除非其读数与其他指南针和/或其他传感器存在一致性问题。在这种情况下，自动驾驶仪将自动确定使用前三个指南针中的哪一个。

虽然许多自动驾驶仪都有一个或多个内部指南针，但许多应用程序将使用外部指南针。这提供了更可靠的数据 比内部指南针，因为与其他指南针分离 电子学。有关特定自动舵的详细信息，请参阅自动[导航仪硬件选项，以确定自动舵](https://ardupilot.org/copter/docs/common-autopilots.html#common-autopilots)可能具有多少个内置指南针（如果有）。

大多数用户只需要执行正常的[指南针校准](https://ardupilot.org/copter/docs/common-compass-calibration-in-mission-planner.html#common-compass-calibration-in-mission-planner)，但较少使用的[CompassMot](https://ardupilot.org/copter/docs/common-compass-setup-advanced.html#common-compass-setup-advanced-compassmot-compensation-for-interference-from-the-power-wires-escs-and-motors)也提供了详细信息

### 指南针设置[¶](https://ardupilot.org/copter/docs/common-compass-setup-advanced.html#compass-settings)

_任务规划器指南针设置屏幕_可在菜单**设置|必需硬件 |**侧边栏中的指南针。这 屏幕用于设置指南针顺序、优先级、校准和使用。正常使用不需要其他设置。

[![../\_images/CompassCalibration\_Onboard.png](https://ardupilot.org/copter/\_images/CompassCalibration\_Onboard.png)](https://ardupilot.org/copter/\_images/CompassCalibration\_Onboard.png)

任务规划器：高级指南针设置和校准[¶](https://ardupilot.org/copter/docs/common-compass-setup-advanced.html#id1)

#### 指南针排序和优先级[¶](https://ardupilot.org/copter/docs/common-compass-setup-advanced.html#compass-ordering-and-priority)

在启动过程中，ArduPilot 会自动检测系统中存在的指南针，将它们添加到列表中，并根据发现它们的顺序为前三个指南针分配与其 DEV ID （） 相关联的优先级 （1-3）。此优先级决定了 EKF 车道使用的指南针。主指南针（最高优先级，1）将由所有通道使用，如果主指南针变得不正常，则会回退到前三个优先级中的下一个可行指南针。`COMPASS_PRIOx_ID`

发现的指南针列表及其优先级在靴子中维护。

如果用户希望更改为三个优先级之一的不同指南针，则可以更改为该指南针的 ID 值。如果 a 设置为零，指南针将连续向上移动，以便在下次重新启动时填充该优先级槽。这在任务规划器中很容易完成，箭头在右侧。`COMPASS_PRIOx_IDCOMPASS_DEV_IDxCOMPASS_PRIOx_ID`

警告

切勿手动更改指南针的 ID 值，然后重新启动！`COMPASS_DEV_IDx`

如果先前发现的指南针在启动时丢失或未检测到，并且位于三个优先级位置之一，则会发生预布防故障，警告用户。用户需要将指南针从优先位置移除，或纠正问题以防止前臂故障。任务规划器提供了一个按钮，用于删除上述屏幕上未检测到的指南针。

注意

校准期间不存在或检测到的指南针将自动删除。

#### 指南针启用[¶](https://ardupilot.org/copter/docs/common-compass-setup-advanced.html#compass-enables)

可以禁用前三个指南针中的任何一个。这将只留下剩余的供自动驾驶仪使用。如果您经常看到“不一致的指南针”前臂消息，并且您确定外部指南针已校准，则您可能希望禁用任何内部指南针。

> 注意
>
> 指南针应始终为直升机/漫游车启用，但可以禁用（不推荐，如果有的话）飞机。

#### 取向[¶](https://ardupilot.org/copter/docs/common-compass-setup-advanced.html#orientation)

必须正确设置[AHRS\_ORIENTATION](https://ardupilot.org/copter/docs/parameters.html#ahrs-orientation)才能成功进行指南针校准。此外，[加速度计](https://ardupilot.org/copter/docs/common-accelerometer-calibration.html#common-accelerometer-calibration)校准应在指南针校准之前完成。

不再需要设置外部指南针的方向。现在，它是在[指南针校准](https://ardupilot.org/copter/docs/common-compass-calibration-in-mission-planner.html#common-compass-calibration-in-mission-planner)期间自动确定的。可以禁用此功能，也可以使用 [COMPASS\_AUTO\_ROT](https://ardupilot.org/copter/docs/parameters.html#compass-auto-rot) 参数仅报告在指南针校准期间确定的方向。如果磁场受到附近金属或其他干扰的影响，特别是在 45 度偏移方向上，方向确定可能会失败。如果已知指南针安装在加速度计的 45 度偏差上，并且在指南针校准期间无法确定方向，则[COMPASS\_AUTO\_ROT](https://ardupilot.org/copter/docs/parameters.html#compass-auto-rot)设置为“3”并重复校准可能会成功完成。

注意

指南针方向的自动确定仅使用正常的指南针校准进行。[飞行中校准](https://ardupilot.org/copter/docs/common-compass-setup-advanced.html#automatic-compass-offset-calibration)和[大型车辆磁](https://ardupilot.org/copter/docs/common-compass-calibration-in-mission-planner.html#large-vehicle-mag-cal)校准要求在尝试这些类型的校准之前正确设置方向。

但是，如果需要仔细检查指南针的方向：

* 当通过所有轴旋转飞机时，每个指南针应沿同一方向移动，并且应具有大致相同的值：
* 北半球：
  * Z 分量应_为正数_
  * 当车辆向下倾斜时，X 分量的值_应该增加_
  * 当车辆向右滚动时，Y 分量的值_应该增加_
* 南半球：
  * Z 分量应_为负数_
  * 当车辆向下倾斜时，X 分量的值_应该会降低_
  * 当车辆右滚动时，Y 分量的值_应减小_

#### 其他参数[¶](https://ardupilot.org/copter/docs/common-compass-setup-advanced.html#other-parameters)

早期版本的ArduPilot没有包含世界磁力模型数据库，磁偏角的位置可能需要手动输入，或通过飞行学习。现在没有必要了。此外，这允许在长途飞行中不断更新偏角。

此外，对于难以移动的飞行器来说，学习飞行中的罗盘偏移而不是地面校准是一种选择。但不建议这样做，因为大型车辆磁力卡选项现在可用。有关详细信息，请参阅[指南针校准](https://ardupilot.org/copter/docs/common-compass-calibration-in-mission-planner.html#common-compass-calibration-in-mission-planner)页面。

### CompassMot — 补偿来自电源线、电调和电机的干扰[¶](https://ardupilot.org/copter/docs/common-compass-setup-advanced.html#compassmot-compensation-for-interference-from-the-power-wires-escs-and-motors)

建议只有内部指南针和 在指南针受到严重干扰的车辆上 电机、电源线等CompassMot仅在您拥有[电池电流监视器](https://ardupilot.org/copter/docs/common-powermodule-landingpage.html#common-powermodule-landingpage)时才有效，因为磁干扰与消耗的电流成线性关系。是的 技术上可以使用油门设置CompassMot，但这不是 推荐。

请按照以下说明操作：

* 启用当前监视器（又名[电源模块](https://ardupilot.org/copter/docs/common-powermodule-landingpage.html#common-powermodule-landingpage)）)
* 断开道具的连接，将它们翻转并旋转一个位置 框架周围。在这种配置中，他们应该推动直升机 油门升起时向下进入地面
* 固定直升机（可能用胶带），使其不会移动
* 打开发射器并将油门保持在零
* 连接车辆的锂聚合物电池
* 使用 USB 电缆将自动驾驶仪连接到计算机
* 打开**初始设置 |可选硬件 |指南针/电机校准**屏幕
*   按**“开始”**按钮

    > [![../\_images/CompassCalibration\_CompassMot.png](https://ardupilot.org/copter/\_images/CompassCalibration\_CompassMot.png)](https://ardupilot.org/copter/\_images/CompassCalibration\_CompassMot.png)
* 您应该听到电调布防蜂鸣声
* 缓慢将油门提高到50%\~75%之间（道具会旋转！ 持续5\~10秒
* 快速将油门降至零
* 按完成按钮**完成**校准
* 检查显示的干扰百分比。如果小于 30%，则 您的指南针干扰是可以接受的，您应该看到良好的情况 徘徊、RTL 和自动性能。如果是 31% \~ 60%，则 干扰位于“灰色区域”，可能没问题（某些用户是 很好，有些不是）。如果高于60%，您应该尝试移动 您的自动驾驶仪更远，远离干扰源，或 考虑购买外部指南针（或[GPS+指南针模块](https://ardupilot.org/copter/docs/common-positioning-landing-page.html#common-positioning-landing-page)（其中一些））。

### 自动偏移校准[¶](https://ardupilot.org/copter/docs/common-compass-setup-advanced.html#automatic-offset-calibration)

在 ArduPilot 的 4.0 版本中，提供了自动偏移学习功能。[COMPASS\_LEARN](https://ardupilot.org/copter/docs/parameters.html#compass-learn)参数确定此功能的工作原理。这适用于高级用户，不建议这样做。

* 如果设置为 3，偏移量将在飞行过程中自动学习、保存，并将此参数重置为 0。在学习偏移时，不应使用位置控制模式（悬停、自动等）。

注意

不建议将[COMPASS\_LEARN](https://ardupilot.org/copter/docs/parameters.html#compass-learn)设置为 1 或 2。这些模式已弃用，要么不起作用，要么仍在开发中。

[COMPASS\_LEARN](https://ardupilot.org/copter/docs/parameters.html#compass-learn) = 3 的过程为：

1. 设置 [COMPASS\_LEARN](https://ardupilot.org/copter/docs/parameters.html#compass-learn) = 3。消息“CompassLearn：已初始化”将出现在MP的消息选项卡上（它不会以红色字母显示在HUD上）。
2. “坏指南针”会出现，但这没什么可担心的。我们希望在最终版本之前将其消除。
3. 以您喜欢的任何模式武装和驾驶/飞行车辆，做一些转弯“指南针学习：有地球场”应该出现在MP的消息选项卡上，然后最终“指南针学习：完成”。

注意

您必须有GPS锁和信号才能成功。确保GPS具有清晰的天空“视野”，并且没有障碍物阻挡GPS信号。

4. 如果需要，可以检查[COMPASS\_LEARN](https://ardupilot.org/copter/docs/parameters.html#compass-learn)参数是否已设置回零（您可能需要刷新参数才能看到这一点），并且 COMPASS\_OFS\_X/Y/Z 值将已更改。
5. 此方法也可以使用“指南针学习”的RCxOPTION来调用。当通道超过1800uS时，它将激活并自动完成并保存。

### 指南针错误消息[¶](https://ardupilot.org/copter/docs/common-compass-setup-advanced.html#compass-error-messages)

* 指南针**健康：指南针**至少没有发送信号 半秒钟。
* **指南针方差**：在 EKF 解决方案中，指南针方向不一致 带有其他惯性传感器的航向估计。点击 任务规划器HUD上的EKF按钮将显示 错误。
* 指南针**未校准：指南针**需要校准。
* 指南针偏移量高：您的一个**指南针偏移量**超过 600， 表明可能存在磁干扰。检查来源 干扰，然后再次尝试校准。

### 使用飞行日志优化校准参数[¶](https://ardupilot.org/copter/docs/common-compass-setup-advanced.html#refining-calibration-parameters-using-a-flight-log)

罗盘偏移、刻度、对角线甚至电机补偿都可以使用分析实用程序从飞行器的飞行数据闪存日志中确定。

* [Magfit Python Utility](https://ardupilot.org/copter/docs/common-magfit.html)
