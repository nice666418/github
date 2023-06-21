# 推力损失和偏航不平衡警告

如果您看到推力损失或偏航不平衡警告，此页面概述了为解决问题而应进行的一些检查和修改。在大多数情况下，这些警告是硬件选择或设置不正确的结果。

这些警告旨在检测推进系统中的硬件故障，如果它们开始发生在没有警告的情况下飞行的车辆上，则应检查推进系统。 警告更有可能发生在较大的有效载荷和强/阵风中。

### 潜在推力损失[¶](https://ardupilot.org/copter/docs/thrust\_loss\_yaw\_imbalance.html#potential-thrust-loss)

如果在GCS或数据闪存日志中看到潜在的推力损失消息，则应进行调查以找到原因和补救措施。警告将给出电机编号，例如：

`` `Potential Thrust Loss (3)` ``

这些警告是一个或多个电机在 100% 油门下饱和的结果。由于这种饱和，ArduCopter 无法再实现所需的横滚、俯仰、偏航和油门输出。 如果这种情况持续很长时间，车辆的高度和姿态控制将降低，并可能坠毁。

如果在悬停或放松飞行中看到这些消息，则必须在硬件中修复问题。应通过改变推进力或减少质量来增加车辆的推重比。

如果只在爬坡和激进的动作中看到，可能足以降低要求的加速度和速度。同样，可以增加车辆的推重比，以允许更高的加速度和速度。

### 偏航不平衡[¶](https://ardupilot.org/copter/docs/thrust\_loss\_yaw\_imbalance.html#yaw-imbalance)

偏航不平衡警告是衡量车辆偏航工作力度的指标，警告将在偏航输出饱和之前触发。如果偏航输出饱和，则车辆的 保持偏航的能力将受到影响。而且，在最坏的情况下，这将导致车辆快速旋转。警告消息给出最大偏航输出的百分比。在100%时，它是饱和的。例如：

`` `Yaw Imbalance 87%` ``

如果在悬停时看到，则应在硬件中解决问题。如果在没有飞行员偏航输入的情况下该值正在增加，则应立即降落车辆。通过比较相对电机的PAR输出，可以在数据闪存日志中识别偏航不平衡。 它将表现为顺时针和逆时针电机之间的大节气门水平差异，如下所示：

<figure><img src="https://ardupilot.org/copter/_images/yaw_imbalance_log.png" alt=""><figcaption></figcaption></figure>

这应该在硬件中修复。最常见的原因是电机在圆形臂上不垂直。如果不平衡仍然存在 电机可以稍微倾斜，使推力角有助于偏航的旋转方向。一些车辆可能对电机推力矢量非常敏感。

如果警告仅在激进偏航操作中出现，则可以通过提高[ATC\_RAT\_YAW\_IMAX](https://ardupilot.org/copter/docs/parameters.html#atc-rat-yaw-imax-ac-attitudecontrol-multi)来提高警告阈值。然而，可能也值得重新审视偏航曲调。

注意

推力损失和偏航不平衡警告都可以使用 [FLIGHT\_OPTIONS](https://ardupilot.org/copter/docs/parameters.html#flight-options) 参数禁用。 只有在进行广泛的日志审查和测试以验证警告是否发现真正的问题后，才应执行此操作。
