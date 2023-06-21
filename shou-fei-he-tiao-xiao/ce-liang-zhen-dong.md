# 测量震动

自动驾驶仪具有对振动敏感的加速度计。 这些加速度计值与气压计和 用于估计车辆位置的 GPS 数据。与过度 振动，估计可能会被抛弃并导致非常糟糕 在依赖于精确定位的模式下的性能（例如在直升机上： AltHold、Loiter、RTL、Guided 、Position 和 Auto Flight 模式）。

这些说明解释了如何测量振动水平。如果你 发现它们超出公差，然后按照[减振](https://ardupilot.org/copter/docs/common-vibration-damping.html#common-vibration-damping)页面上的建议进行操作。

### 地面站的实时视图[¶](https://ardupilot.org/copter/docs/common-measuring-vibration.html#real-time-view-in-ground-station)

地面站可以显示振动和削波的实时视图。如果使用任务规划器，请单击HUD上的“Vibe”以显示当前的振动级别。

> [![../\_images/vibration-realtime-mp.png](https://ardupilot.org/copter/\_images/vibration-realtime-mp.png)](https://ardupilot.org/copter/\_images/vibration-realtime-mp.png)

低于30m/s/s的振动水平通常是可以接受的。高于30m/s/s的水平_可能有_问题，高于60m/s/s的水平几乎总是有位置或高度保持的问题。

### Vibe 数据闪存日志消息[¶](https://ardupilot.org/copter/docs/common-measuring-vibration.html#vibe-dataflash-log-message)

检查记录的 Vibe 电平大多低于 30m/s/s

* 执行至少 几分钟并[下载数据闪存日志](https://ardupilot.org/copter/docs/common-downloading-and-analyzing-data-logs-in-mission-planner.html#common-downloading-and-analyzing-data-logs-in-mission-planner-downloading-logs-via-mavlink)。
* 使用任务规划器或其他地面站绘制 VIBE 消息的图形 VibeX、VibeY 和 VibeZ 值。这些显示标准偏差 主加速度计的输出（以 m/s/s 为单位）。下图，拍摄 从 3DR IRIS 显示低于 15m/s/s 的正常水平，但 偶尔峰值可达30m/s/s。可接受的最大值似乎为 低于30米/秒/秒（见下图）。
*   绘制剪辑 0、剪辑 1 和剪辑 2 值的图形，这些值每次增加一次 的加速度计达到其最大极限 （16G）。理想 对于整个飞行，这些数字应为零，但低数字 （<100） 是 可能还可以，特别是如果它们发生在硬着陆期间。A 定期 通过日志的数量增加表示严重振动 [应该解决](https://ardupilot.org/copter/docs/common-vibration-damping.html#common-vibration-damping)的问题。

    [![../\_images/mp\_vibe\_dataflash\_msg.png](https://ardupilot.org/copter/\_images/mp\_vibe\_dataflash\_msg.png)](https://ardupilot.org/copter/\_images/mp\_vibe\_dataflash\_msg.png)

这是由于位置估计问题而出现位置估计问题的车辆的示例 到高振动。

[![../\_images/mp\_measuring\_vibration\_bad\_vibes.png](https://ardupilot.org/copter/\_images/mp\_measuring\_vibration\_bad\_vibes.png)](https://ardupilot.org/copter/\_images/mp\_measuring\_vibration\_bad\_vibes.png)

计算振动水平的算法可以在[AP\_InertialSensor.cpp的calc\_vibration\_and\_clipping（）](https://github.com/ArduPilot/ardupilot/blob/master/libraries/AP\_InertialSensor/AP\_InertialSensor.cpp#L1609)方法中看到，但简而言之，它涉及计算标准偏差 加速度计读数如下：

* 从主 IMU 捕获原始 x、y 和 z 加速度计值
* 高通滤波器在 5hz 处的原始值，以去除车辆的 移动并为 x、y 和 z 轴创建“accel\_vibe\_floor”。
* 计算最新加速度值与 accel\_vibe\_floor。
* 对上述差异进行平方，在2hz处过滤，然后计算 平方根（对于 x、y 和 z）。这最后三个值是什么 出现在 VIBE 消息的 VibeX、Y 和 Z 字段中。

在查看原木中的振动时，首先要看的是削波。如果剪辑为 0，那就好了。这意味着检测到的振动不会压倒IMU。

对振动进行故障排除时，请将振动轴视为凝视点以查找问题：

> 如果 X 和 Y 都很高，则电机轴承或螺旋桨平衡可能有问题。或者，您可能需要为您的 FC 提供更多/更好的整体减振。 如果 X 或 Y 为高，则您的 FC 安装可能有问题。也许电线在 FC 上弹跳或限制它。或者，您的减振在一个轴上比在另一个轴上效果更好。 如果您有 Z 振动，那么您的螺旋桨（弯曲叶片）或电机中的垂直游隙可能存在轨道问题。

还要考虑到某些飞行条件/机身会有不同的自然振动。如果振动在悬停时看起来不错，但它们随着速度的增加而增加，则可能是机身或风中存在空气动力学问题，

### 寻找“精益”[¶](https://ardupilot.org/copter/docs/common-measuring-vibration.html#looking-for-the-leans)

当飞行器的姿态估计变得不正确导致其显着倾斜时，即使飞行员正在指挥水平飞行，也会发生**倾斜**。问题的原因通常是加速度计混叠，这可以通过比较每个估计系统（即每个AHRS或EKF）的滚动和俯仰姿态估计来确认。姿态估计应该在几度以内

* 下载数据闪存日志并在地面站的日志查看器中打开
* 比较AHRS2。卷，NKF1\[0]。Roll和NKF1\[1]。如果使用 EKF2 或 AHRS2，则滚动。卷，XKF1\[0]。滚动和XKF1\[1]。滚动，如果使用 EKF3

下图显示了态度匹配良好的典型日志

[![../\_images/vibration-measuring-leans.png](https://ardupilot.org/copter/\_images/vibration-measuring-leans.png)](https://ardupilot.org/copter/\_images/vibration-measuring-leans.png)

### 使用 FFT 进行高级分析[¶](https://ardupilot.org/copter/docs/common-measuring-vibration.html#advanced-analysis-with-fft)

有关如何收集大量 IMU 数据并执行 FFT 分析以确定振动最大的频率的说明，请参阅使用 [IMU 批量采样器测量振动](https://ardupilot.org/copter/docs/common-imu-batchsampling.html#common-imu-batchsampling)页面。

### IMU 数据闪存日志消息[¶](https://ardupilot.org/copter/docs/common-measuring-vibration.html#imu-dataflash-log-message)

对于不包含Vibe消息的非常旧的ArduPilot版本，可以直接检查IMU值

* 确保[将LOG\_BITMASK](https://ardupilot.org/copter/docs/parameters.html#log-bitmask)参数设置为包含 IMU 数据，以便将加速度计值记录到数据闪存日志中
* 在稳定模式下飞行您的直升机并尝试保持水平悬停（它不需要完全稳定或水平）
* [下载数据闪存日志](https://ardupilot.org/copter/docs/common-downloading-and-analyzing-data-logs-in-mission-planner.html#common-downloading-and-analyzing-data-logs-in-mission-planner-downloading-logs-via-mavlink)，下载完成后，使用任务规划器的“查看 日志“按钮打开日志目录中的最新文件（它是最后一个 数字将是您下载的日志编号，因此在上面的示例中 我们下载了日志#1，因此文件名将以1.log结尾）
*   当日志浏览器出现时，向下滚动，直到找到任何 IMU 消息。单击该行的 AccX 并将**“将此数据绘制”向**左按 按钮。对 AccY 和 AccZ 列重复此操作以生成类似 下面。

    [![DiagnosingWithLogs\_Vibes](https://ardupilot.org/copter/\_images/DiagnosingWithLogs\_Vibes.png)](https://ardupilot.org/copter/\_images/DiagnosingWithLogs\_Vibes.png)
* 检查左侧的刻度，确保您的振动水平 AccX 和 AccY 介于 -3 和 +3 之间。对于 AccZ 可接受的 范围为 -15 到 -5。如果它非常接近或超过这些限制，则 应参考减[振](https://ardupilot.org/copter/docs/common-vibration-damping.html#common-vibration-damping)页面以获取可能的解决方案。
* 完成上述所有操作后，转到任务规划器的标准 参数页面（您可能需要再次按**“连接**”按钮） 并将日志位掩码设置回“默认”。这很重要，因为 特别是在 APM 日志记录上，需要大量的 CPU 资源和 如果不是真正需要的，记录这些是一种浪费。
