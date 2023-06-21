# 自动调谐

## 自动调谐[¶](https://ardupilot.org/copter/docs/autotune.html#autotune)

AutoTune 尝试自动调整稳定 P、速率 P 和 D 以及最大旋转加速度，以提供最高响应，而不会产生明显的过冲。在尝试使用AutoTune之前，直升机需要在[AltHold模式下](https://ardupilot.org/copter/docs/altholdmode.html#altholdmode)“基本上”可以飞行，因为该功能需要能够在横滚和俯仰轴上“抽搐”直升机。

警告

AutoTune并不总是能够确定车辆的良好调谐，并且可能导致增益，从而导致无法飞行的车辆可能坠毁。在尝试使用自动调谐之前，请按照[调整过程说明](https://ardupilot.org/copter/docs/tuning-process-instructions.html#tuning-process-instructions)进行操作。按照这些说明操作并评估了[您的初始曲](https://ardupilot.org/copter/docs/evaluating-the-aircraft-tune.html#evaluating-the-aircraft-tune)调后，应该尝试自动调谐。

有许多问题可能会阻止自动调谐提供良好的调谐，包括：

* 强风
* 高水平的陀螺仪噪声
* [MOT\_THST\_EXPO](https://ardupilot.org/copter/docs/parameters.html#mot-thst-expo)值不正确引起的非线性电调响应
* 灵活的框架或有效载荷安装
* 过于灵活的隔振支架
* [非常低的MOT\_SPIN\_MIN](https://ardupilot.org/copter/docs/parameters.html#mot-spin-min)设置
* 过载的螺旋桨或电机

### 在自动调谐模式下飞行前的设置[¶](https://ardupilot.org/copter/docs/autotune.html#setup-before-flying-in-autotune-mode)

1. 将一个飞行模式开关位置设置为 AltHold。
2. 将 RC 通道辅助功能开关或[辅助功能开关](https://ardupilot.org/copter/docs/channel-7-and-8-options.html#channel-7-and-8-options)（4.0 版之前）设置为 AutoTune，以允许您使用 a 开关打开/关闭自动调谐。

注意

您还可以在飞行模式开关上将自动调整飞行模式设置为模式，以激活自动调谐

3. 取下相机云台或画面中可能在飞行中晃动的任何其他部分
4. 使用 [AUTOTUNE\_AXES](https://ardupilot.org/copter/docs/parameters.html#autotune-axes-ac-autotune-multi) 参数选择要调整的轴组合（横滚、俯仰、偏航）
5. 使用 [AUTOTUNE\_AGGR](https://ardupilot.org/copter/docs/parameters.html#autotune-aggr) 参数（0.1=激进，0.075=中等，0.050=弱）设置自动调谐的主动性，通常从默认的 0.1 开始。
6. 对于大型直升机（螺旋桨直径至少为 13 英寸或 33 厘米），将速率滚动和俯仰过滤器设置为 10hz，它们是：[ATC\_RAT\_RLL\_FLTT](https://ardupilot.org/copter/docs/parameters.html#atc-rat-rll-fltt-ac-attitudecontrol-multi)、[ATC\_RAT\_RLL\_FLTD](https://ardupilot.org/copter/docs/parameters.html#atc-rat-rll-fltd-ac-attitudecontrol-multi)、[ATC\_RAT\_PIT\_FLTT](https://ardupilot.org/copter/docs/parameters.html#atc-rat-pit-fltt-ac-attitudecontrol-multi)、[ATC\_RAT\_PIT\_FLTD](https://ardupilot.org/copter/docs/parameters.html#atc-rat-pit-fltd-ac-attitudecontrol-multi)（在 Copter-3.4 中它们是ATC\_RAT\_RLL\_FILT和ATC\_RAT\_PIT\_FILT）
7. 建议启用[PID增益的电池电压缩放](https://ardupilot.org/copter/docs/current-limiting-and-voltage-scaling.html#current-limiting-and-voltage-scaling)

### 如何调用自动调谐[¶](https://ardupilot.org/copter/docs/autotune.html#how-to-invoke-autotune)

1. 等待平静的一天，然后去一个大的空地。
2. 确保通道7或通道8开关（如果使用）处于低位。
3. 起飞并将直升机舒适地置于 AltHold 模式 高度。
4.  面向车辆，使其与风吹向方向成 90 度角抽搐（即，如果先调整滚动，请将车辆对准风中）

    [![../\_images/autotune\_copterwind.png](https://ardupilot.org/copter/\_images/autotune\_copterwind.png)](https://ardupilot.org/copter/\_images/autotune\_copterwind.png)
5. 将 ch7/ch8 开关设置为高电平位置，或切换到自动调谐模式，以启用自动调谐：
   * 你会看到它左右抽搐了大约 20 度 分钟，然后它将向前和向后重复。
   * 随时使用横滚杆和俯仰杆重新定位直升机 如果它漂移（它将在以下期间使用原始PID增益 重新定位和测试之间）。当你松开棍子时，它会 将在中断的地方继续自动调整。
   * 将 ch7/ch8 开关移动到低位置，如果使用自动调谐飞行模式，则随时更改飞行模式 放弃自动整定并返回到原始 PID。
   * 确保发射机上没有设置任何修剪或 自动调谐可能不会收到摇杆居中的信号。
6. 曲调完成后，直升机将变回原始声音 PID 增益。
7. 将通道7/通道8开关置于低电平位置，然后返回高电平 位置以测试调谐的PID增益，或者如果使用自动调谐飞行模式，则切换出去，然后重新进入该模式。
8. 将 ch7/ch8 开关置于低位，或切换出自动调谐飞行模式，使用 原始 PID 增益。
9.  如果您对自动调谐的PID增益感到满意，请离开通道7/通道8 切换到高位置，或切换回自动调谐飞行模式并着陆和撤防以保存PID 永久。

    如果您不喜欢新的 PIDS，请将 ch7/ch8 切换为低电平或退出自动调谐飞行模式，以返回 原始 PID。当你解除武装时，收益将无法保存。

如果您在执行自动调谐后发现飞行器在飞行时感觉过度抽搐，稳定，AltHold或PosHold（但还可以更多） 自主模式（如 Loiter、RTL、Auto）尝试将[ATC\_INPUT\_TC](https://ardupilot.org/copter/docs/parameters.html#atc-input-tc)参数增加到 0.25。这平滑了飞行员的输入。 或者尝试减小 [AUTOTUNE\_AGGR](https://ardupilot.org/copter/docs/parameters.html#autotune-aggr) 参数（它应始终在 0.05 到 0.10 的范围内），然后重试。

如果车辆在自动调谐后感觉马虎，请尝试将[AUTOTUNE\_AGGR](https://ardupilot.org/copter/docs/parameters.html#autotune-aggr)参数增加到 0.10，然后再次尝试自动调谐。

### 使用位置保持调用自动调谐[¶](https://ardupilot.org/copter/docs/autotune.html#invoke-autotune-with-position-hold)

警告

通常可以通过如上所述从 AltHold 调用 AutoTune 来实现更好的调谐，而不是如下所述从 Loiter 或 PosHold 调用。使用自动调谐飞行模式也有这个可能的缺点。

如果在执行自动调谐时从 Loiter 或 PosHold 飞行模式（与 AltHold 相反）调用，AutoTune 会执行弱位置保持。如果使用自动调谐飞行模式，则也会使用此弱位置保持。

> [![../\_images/autotune\_from\_loiter.png](https://ardupilot.org/copter/\_images/autotune\_from\_loiter.png)](https://ardupilot.org/copter/\_images/autotune\_from\_loiter.png)

* 车辆将轻轻倾斜（最多 10 度）向“目标点”倾斜（最多 <> 度），该目标点最初设置为调用 AutoTune 时车辆的位置。
* 飞行员可以使用横滚杆、俯仰杆、偏航杆或油门杆重新定位车辆。在飞行员释放横滚杆和俯仰杆的那一刻，目标位置将重置为车辆的位置。
* 高度保持控制器保持高度，因此 当摇杆时，车辆将尝试保持其当前高度 放置在中油门的 10% 处。它会在向上攀升或下降 至2.5m/s（此速度可通过[PILOT\_SPEED\_UP](https://ardupilot.org/copter/docs/parameters.html#pilot-speed-up)和[PILOT\_SPEED\_DN](https://ardupilot.org/copter/docs/parameters.html#pilot-speed-dn)参数进行调节）。用于建立这些速度的加速度由[PILOT\_ACCEL\_Z](https://ardupilot.org/copter/docs/parameters.html#pilot-accel-z)设置。
* 为了垂直于风向抽搐，当车辆从目标位置漂移90m（或更多）时，可能会突然向任一方向旋转5度。
* 如果风很小或没有风，飞行器的温和位置控制可能意味着它来回移动，每次偏离目标超过 5 米时，都会在目标点周围乒乓球，改变偏航。在这些情况下，恢复更简单的基于 AltHold 的 AutoTune 可能更舒服。

### 如果自动调谐失败[¶](https://ardupilot.org/copter/docs/autotune.html#if-autotune-fails)

如果自动调谐失败，则需要执行手动调整。

AutoTune成功的一些迹象是（除了DataFlash日志和地面控制站消息）：

* [ATC\_ANG\_PIT\_P](https://ardupilot.org/copter/docs/parameters.html#atc-ang-pit-p)和[ATC\_ANG\_RLL\_P](https://ardupilot.org/copter/docs/parameters.html#atc-ang-rll-p)值的增加。
* [ATC\_RAT\_PIT\_D](https://ardupilot.org/copter/docs/parameters.html#atc-rat-pit-d-ac-attitudecontrol-multi)和[ATC\_RAT\_RLL\_D](https://ardupilot.org/copter/docs/parameters.html#atc-rat-rll-d-ac-attitudecontrol-multi)大于[AUTOTUNE\_MIN\_D](https://ardupilot.org/copter/docs/parameters.html#autotune-min-d)。

AutoTune将尝试在飞机可以容忍的范围内尽可能紧密地调整每个轴。在某些飞机上，这可能会产生不必要的响应。大多数飞机的指南：

* [ATC\_ANG\_PIT\_P](https://ardupilot.org/copter/docs/parameters.html#atc-ang-pit-p)应从 10 减少到 6
* [ATC\_ANG\_RLL\_P](https://ardupilot.org/copter/docs/parameters.html#atc-ang-rll-p)应从 10 减少到 6
* [ATC\_ANG\_YAW\_P](https://ardupilot.org/copter/docs/parameters.html#atc-ang-yaw-p)应从 10 减少到 6
* [ATC\_RAT\_YAW\_P](https://ardupilot.org/copter/docs/parameters.html#atc-rat-yaw-p-ac-attitudecontrol-multi)应从 1 降低到 0.5
* [ATC\_RAT\_YAW\_I](https://ardupilot.org/copter/docs/parameters.html#atc-rat-yaw-i-ac-attitudecontrol-multi)： [ATC\_RAT\_YAW\_P](https://ardupilot.org/copter/docs/parameters.html#atc-rat-yaw-p-ac-attitudecontrol-multi) x 0.1

仅当自动调整产生更高的值时，才应更改这些值。小型特技飞机可能更愿意将这些值保持在尽可能高的水平。

### 附加说明[¶](https://ardupilot.org/copter/docs/autotune.html#additional-notes)

* 在Copter-3.3（及更高版本）中，AutoTune可以设置为飞行模式。切换到或退出自动调谐飞行模式的响应方式与将分配自动调谐功能的 ch7/ch8 辅助开关升高或降低相同。
* [AUTOTUNE\_AXES](https://ardupilot.org/copter/docs/parameters.html#autotune-axes-ac-autotune-multi)允许控制要调整的轴。如果车辆的电池寿命不足以完成所有 3 轴，这将非常有用）。“1” = 调音滚动，“2” = 调音，“4” = 调偏航。将这些数字相加以在单个会话中调谐多个轴（即“7”=调谐所有轴）
* [AUTOTUNE\_AGGR](https://ardupilot.org/copter/docs/parameters.html#autotune-aggr)：应在 0.05 到 0.10 的范围内。较高的值将产生更激进的调谐，但有时会导致增益过高。更具体地说，此参数控制 D 项反弹和 P 项过冲的阈值。这会影响调谐抗扰度（值越高，对帧中的弯曲或其他可能欺骗调谐算法的干扰的容忍度越高）。高值也会导致调谐更好地抑制外部干扰。较低的值会导致调谐对引导输入的响应速度更快。
*   可由自动调整更新的参数的完整列表

    > * 滚动角P增益[ATC\_ANG\_RLL\_P](https://ardupilot.org/copter/docs/parameters.html#atc-ang-rll-p)
    > * 滚动速率 P、I 和 D 增益[ATC\_RAT\_RLL\_P](https://ardupilot.org/copter/docs/parameters.html#atc-rat-rll-p-ac-attitudecontrol-multi)、[ATC\_RAT\_RLL\_I](https://ardupilot.org/copter/docs/parameters.html#atc-rat-rll-i-ac-attitudecontrol-multi)、[ATC\_RAT\_RLL\_D](https://ardupilot.org/copter/docs/parameters.html#atc-rat-rll-d-ac-attitudecontrol-multi)
    > * 横滚最大加速度[ATC\_ACCEL\_R\_MAX](https://ardupilot.org/copter/docs/parameters.html#atc-accel-r-max)
    > * 俯仰角P增益[ATC\_ANG\_PIT\_P](https://ardupilot.org/copter/docs/parameters.html#atc-ang-pit-p)
    > * 音高速率 P、I 和 D 增益[ATC\_RAT\_PIT\_P](https://ardupilot.org/copter/docs/parameters.html#atc-rat-pit-p-ac-attitudecontrol-multi)、[ATC\_RAT\_PIT\_I](https://ardupilot.org/copter/docs/parameters.html#atc-rat-pit-i-ac-attitudecontrol-multi)、[ATC\_RAT\_PIT\_D](https://ardupilot.org/copter/docs/parameters.html#atc-rat-pit-d-ac-attitudecontrol-multi)
    > * 俯仰最大加速度[ATC\_ACCEL\_P\_MAX](https://ardupilot.org/copter/docs/parameters.html#atc-accel-p-max)
    > * 偏航角P增益[ATC\_ANG\_YAW\_P](https://ardupilot.org/copter/docs/parameters.html#atc-ang-yaw-p)
    > * 偏航率 P，我获得[ATC\_RAT\_YAW\_P](https://ardupilot.org/copter/docs/parameters.html#atc-rat-yaw-p-ac-attitudecontrol-multi)、[ATC\_RAT\_YAW\_I](https://ardupilot.org/copter/docs/parameters.html#atc-rat-yaw-i-ac-attitudecontrol-multi)、[ATC\_RAT\_YAW\_D](https://ardupilot.org/copter/docs/parameters.html#atc-rat-yaw-d-ac-attitudecontrol-multi)
    > * 偏航角角速率滤波器[ATC\_RAT\_YAW\_FLTT](https://ardupilot.org/copter/docs/parameters.html#atc-rat-yaw-fltt-ac-attitudecontrol-multi)，[ATC\_RAT\_YAW\_FLTE](https://ardupilot.org/copter/docs/parameters.html#atc-rat-yaw-flte-ac-attitudecontrol-multi)（AC3.6：ATC\_RAT\_YAW\_FLT）
    > * 偏航最大加速度[ATC\_ACCEL\_Y\_MAX](https://ardupilot.org/copter/docs/parameters.html#atc-accel-y-max)
    > * 启用横滚和俯仰轴速率前馈 （[ATC\_RATE\_FF\_ENAB](https://ardupilot.org/copter/docs/parameters.html#atc-rate-ff-enab))
* 在你有一个好的调谐后，你可能希望将[ATC\_THR\_MIX\_MAX](https://ardupilot.org/copter/docs/parameters.html#atc-thr-mix-max)增加到 0.9（默认值为 0.5），以增加姿态控制的优先级。如果飞行器在执行快进飞行后突然减速，这可以减少 AltHold 中有时看到的俯仰超调（尤其是在带有大型螺旋桨的直升机上）。在这种情况下，风在提供升力的螺旋桨下方捕获，但也扰乱了车辆的姿态，导致油门和姿态控制之间的冲突。增加此参数值的危险在于，如果后来速率增益提高到车辆振荡严重，则车辆可能难以下降（因为它将优先尝试纠正姿态振荡并且永远不会充分降低油门）。
* AutoTune可以请求对电机**的输出进行非常大和快速的更改**，这可能会导致ESC同步问题，尤其是在使用SimonK固件和/或低KV电机（低于500KV）时。观看此[视频](https://www.youtube.com/watch?v=hBUBbeyLe0Q)，其中显示了重现同步问题的测试。
* 为了获得最佳效果，不应允许直升机建立过多的水平速度。这可以通过在测试之间应用快速校正（抽搐）来防止飞行器飞行过快。
* 请注意，AutoTune 将从 Stabilize 接合，因此在您处于 AltHold 并准备好开始该过程之前，不要意外翻转 AutoTune 开关。
* 作为一般规则，对于俯仰和滚动，P 和 I 应该相等，D 应该是 1/10 P。对于偏航，在大多数情况下，I 应该是 1/10 P 和 D = 0。

### 常见问题[¶](https://ardupilot.org/copter/docs/autotune.html#common-problems)

* 如果车辆即使处于自动调谐模式也不会开始调谐（即不会抽搐），那么问题可能是侧倾、俯仰、偏航或油门杆不在中间。通过将[RC1\_DZ](https://ardupilot.org/copter/docs/parameters.html#rc1-dz)、[RC2\_DZ](https://ardupilot.org/copter/docs/parameters.html#rc2-dz)、[RC3\_DZ](https://ardupilot.org/copter/docs/parameters.html#rc3-dz)和[RC4\_DZ](https://ardupilot.org/copter/docs/parameters.html#rc4-dz)增加到 50（或更高），可能有助于增加 RC 输入的死区。
* 如果自动调谐产生过度抽搐的车辆，请尝试减小[AUTOTUNE\_AGGR](https://ardupilot.org/copter/docs/parameters.html#autotune-aggr)参数（不应低于 0.05）并再次执行自动调谐。
* 如果自动调谐产生一个草率的车辆，请尝试增加[AUTOTUNE\_AGGR](https://ardupilot.org/copter/docs/parameters.html#autotune-aggr)参数（不应高于 0.1），然后再次执行自动调谐。

提示

报告自动调谐问题时，请附上帧的描述和飞行的数据闪存日志。

### 数据闪存日志记录[¶](https://ardupilot.org/copter/docs/autotune.html#dataflash-logging)

ATUN（自动调谐概述）和 ATDE（自动调谐详细信息）消息是 写入数据闪存日志。这些内容的一些细节 消息可以在[任务规划器维基页面的下载和分析数据日志](https://ardupilot.org/copter/docs/common-downloading-and-analyzing-data-logs-in-mission-planner.html#common-downloading-and-analyzing-data-logs-in-mission-planner-message-details-copter-specific)中找到。

### 地面控制站消息[¶](https://ardupilot.org/copter/docs/autotune.html#ground-control-station-messages)

对于每个轴，曲调有几个阶段。首先调整速率PID，然后调整角度参数。这些阶段的进度消息将发送到GCS（并记录在数据闪存日志中）。

调优期间的典型顺序可能是：

```
09:09:33       AutoTune: Twitch
09:09:34       AutoTune: (P) Rate P Up\
09:09:34       AutoTune: WFL (Rate(P)) (15.13040 > 10.00000)
09:09:34       AutoTune: p=0.052298 d=0.005232
09:09:34       AutoTune: success 1/4
```

这是在俯仰速率 P 调整期间，表示抽搐即将发生，因为 P 正在以增加的值 0.052298 尝试，但首先它等待它从最后一次抽搐回到水平（WFL = 等待水平），然后它报告此抽搐的结果在目标范围内并成功。但这必须连续发生 4 次，然后才能进入下一阶段。

注意

在调整的偏航速率阶段，消息将显示“d”的值，该值不是ATC\_RAT\_YAW\_D，通常是 0，而是正在更改的 ATC\_RAT\_YAW\_FLTE 的值。

每当过程被导向杆运动中断时，

```
09:09:38       AUTOTUNE: pilot overrides active
```

消息出现。

如果您在仍处于 AUTOTUNE 中时停止了调谐并解除了防，并且轴调谐已完成，您将收到一条消息，显示已为该轴保存了新的增益。如果没有与此效果的消息，但认为您至少完成了一个轴，那么您可能在未处于 AUTOTUNE 模式时解除武装，并且实际上并没有保存它们。

```
09:19:48       AutoTune: Saved gains for Pitch
```

提示

如果您碰巧在不处于自动调谐时通过撤防意外丢弃会话自动调谐值，则可以检查数据闪存日志中是否有它在调谐期间发送的 GCS 消息，并在工作台上手动设置它们。

***

<figure><img src="https://ardupilot.org/copter/_images/banner-freespace.png" alt=""><figcaption></figcaption></figure>
