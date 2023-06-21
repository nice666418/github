# 自动修剪

风当然会对你的直升机产生强烈的影响，并会把它推来推去。但是，您可能还会发现，在稳定模式下飞行时，即使在无风环境中，您的直升机也总是朝着同一方向漂移。这在很大程度上可以使用“保存修剪”或“自动修剪”功能进行纠正。

注意

对于大多数用户来说，此过程不是必需的，因为[加速度计校准](https://ardupilot.org/copter/docs/common-accelerometer-calibration.html#common-accelerometer-calibration)可以很好地设置微调值。

### 保存修剪[¶](https://ardupilot.org/copter/docs/autotrim.html#save-trim)

保存修剪是更简单的方法，基本上涉及将无线电发射器的修剪传输到自动驾驶仪（[此处的视频演示](https://www.youtube.com/watch?v=ayA0uYOqKX4)）。

1. 检查 MissionPlanner 的硬件>强制硬件>无线电校准屏幕上的 CH7 交换机是否高于 1800

<figure><img src="https://ardupilot.org/copter/_images/MP_SaveTrim_Ch7PWMCheck.png" alt=""><figcaption></figcaption></figure>

2. 在软件> Copter Pids 屏幕上设置 CH7 选项以保存修剪，然后按“写入参数”按钮

<figure><img src="https://ardupilot.org/copter/_images/MP_SaveTrim_Ch7.png" alt=""><figcaption></figcaption></figure>

3. 当您的 CH7 开关处于关闭位置时，将直升机置于稳定模式，并使用发射器的横滚和俯仰修剪使其保持飞行水平
4. 着陆并将油门归零
5. 松开滚动杆和俯仰杆，并将 CH7 开关切换为高电平至少 1 秒钟。“修剪已保存”字样应出现在 MP 的“飞行数据”屏幕的“消息”选项卡中
6. 重置您的发射器滚动和俯仰修剪回到中心并再次飞行，它现在应该水平飞行。如果不重复步骤3，4和5

### 自动修剪[¶](https://ardupilot.org/copter/docs/autotrim.html#auto-trim)

使用自动修剪功能，当您在稳定的悬停中飞行时，可以捕获横滚和俯仰修剪。

1. 找到一个无风的环境，有足够的空间让你的直升机飞行而不会撞到东西
2. 将战车置于稳定模式
3. 按住油门并向右舵 15 秒，或直到您看到红色、蓝色和黄色的小 LED 以循环模式闪烁
4. 在稳定的悬停中飞行直升机约 25 秒
5. 着陆并将油门归零并等待几秒钟（正在保存修剪参数）
6. 在稳定模式下再次起飞，并检查您的直升机现在是否在飞行水平。如果没有，请重复步骤 2、3 和 4

注意

您还可以测试上述这些程序在断开电池连接的情况下在地面上运行。将您的自动驾驶仪连接到任务规划器，并在模拟完成上述步骤时观察飞行数据屏幕。

<figure><img src="https://ardupilot.org/copter/_images/MP_SaveTrim_FlightDataScreen.jpg" alt=""><figcaption></figcaption></figure>

注意

您可以通过修改[AHRS\_TRIM\_X](https://ardupilot.org/copter/docs/parameters.html#ahrs-trim-x)和[AHRS\_TRIM\_Y](https://ardupilot.org/copter/docs/parameters.html#ahrs-trim-y)来手动设置修剪。滚动修剪[AHRS\_TRIM\_X](https://ardupilot.org/copter/docs/parameters.html#ahrs-trim-x)，节距修剪[AHRS\_TRIM\_Y](https://ardupilot.org/copter/docs/parameters.html#ahrs-trim-y)。这两个值都以弧度为单位，左滚和前倾为负数。

注意

几乎不可能摆脱所有漂移，因此您的直升机在没有任何输入的情况下保持完全静止。

### 保存修剪和自动修剪的视频演示[¶](https://ardupilot.org/copter/docs/autotrim.html#video-demonstrations-of-save-trim-and-auto-trim)

### 桌面方法[¶](https://ardupilot.org/copter/docs/autotrim.html#desktop-method)

装饰也可以通过设置车辆水平来更新，连接到 任务规划器（或其他地面站）并选择 初始设置、强制硬件、加速校准和推送 降低“校准级别”按钮。

<figure><img src="https://ardupilot.org/copter/_images/AccelCalibration_MP.png" alt=""><figcaption></figcaption></figure>

请注意，虽然在车辆在 地面并不一定意味着它不会水平漂移，而 由于其他小框架问题（包括飞行）而飞行 控制器在框架上不完全水平且略微倾斜 电机。
