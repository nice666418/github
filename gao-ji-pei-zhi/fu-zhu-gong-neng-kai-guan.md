# 辅助功能开关

## 辅助功能[¶](https://ardupilot.org/copter/docs/common-auxiliary-functions.html#auxiliary-functions)

此功能是固件版本 4.0 及更高版本。在 4.0 之前的 Copter 版本中，类似的功能是使用 CHx\_OPT 参数实现的。请参阅[辅助功能开关（3.6 及更早版本）](https://ardupilot.org/copter/docs/channel-7-and-8-options.html#channel-7-and-8-options)页面。

本页介绍如何设置可从变送器的辅助功能开关或外部[按钮](https://ardupilot.org/copter/docs/common-buttons.html#common-buttons)调用的附加功能。

### 配置使用的发射机通道[¶](https://ardupilot.org/copter/docs/common-auxiliary-functions.html#configuring-which-transmitter-channel-is-used)

任何RC输入通道都可以分配任何辅助功能。但是，RC通道不应由任何其他功能使用，例如飞行模式选择或飞行控制。默认情况下，通道 1-4 用于飞行控制（即横滚、俯仰、油门和偏航）。飞机和漫游者的默认飞行模式通道为 8，直升机的默认飞行模式通道为 5。

### 分配特征[¶](https://ardupilot.org/copter/docs/common-auxiliary-functions.html#assigning-the-feature)

RCx\_OPTION参数控制这些功能。例如，[RC7\_OPTION](https://ardupilot.org/copter/docs/parameters.html#rc7-option)参数控制将哪个要素分配给 RC 输入 7。每个RC通道都有其 拥有可在完整参数列表中访问的RCx\_OPTION参数。

### 支持的功能[¶](https://ardupilot.org/copter/docs/common-auxiliary-functions.html#supported-features)

| **RCx\_OPTION值** | **功能说明**              | **直升机** | **飞机** | **车** |
| ---------------- | --------------------- | ------- | ------ | ----- |
| 0                | 不执行任何操作（默认）           | X       | X      | X     |
| 2                | 空翻                    | X       |        |       |
| 3                | 简单模式（直升机）             | X       |        |       |
| 4                | 劳特模式                  | X       | X      | X     |
| 5                | 保存修剪                  | X       |        | X     |
| 7                | 保存航点                  | X       |        | X     |
| 9                | 相机触发器                 | X       | X      | X     |
| 10               | 测距                    | X       |        |       |
| 11               | 栅栏                    | X       | X      | X     |
| 12               | 重置到装甲偏航               |         |        |       |
| 13               | 超简单模式                 | X       |        |       |
| 14               | 安科训练器                 | X       |        |       |
| 15               | 喷雾器                   | X       |        |       |
| 16               | 自动模式                  | X       | X      | X     |
| 17               | 自动调谐模式                | X       |        |       |
| 18               | 土地模式                  | X       |        |       |
| 19               | 片 梭                   | X       | X      | X     |
| 21               | 降落伞启用                 | X       |        |       |
| 22               | 降落伞释放                 | X       |        |       |
| 23               | 降落伞 3 位开关             | X       |        |       |
| 24               | 重置自动任务以开始             | X       | X      | X     |
| 25               | 姿态控制器FF               | X       |        |       |
| 26               | 姿态控制器 AccLim          | X       |        |       |
| 27               | 缩回支架                  | X       |        |       |
| 28               | 继电器 1 开/关             | X       | X      | X     |
| 29               | 起落架                   | X       | X      |       |
| 30               | 丢失的车辆声音               | X       | X      | X     |
| 31               | 电机紧急停止                | X       | X      | X     |
| 32               | 电机联锁                  | X       |        |       |
| 33               | 制动                    | X       |        |       |
| 34               | 继电器 2 开/关             | X       | X      | X     |
| 35               | 继电器 3 开/关             | X       | X      | X     |
| 36               | 继电器 4 开/关             | X       | X      | X     |
| 37               | 投掷模式                  | X       |        |       |
| 38               | 启用 ADSB 避免            | X       |        |       |
| 39               | 精密游荡器                 | X       |        |       |
| 40               | 物体回避                  | X       |        | X     |
| 41               | 手臂撤防（4.1 及之前版本）       | X       | X      | X     |
| 42               | 智能引导模式                | X       |        | X     |
| 43               | 倒置飞行                  | X       | X      |       |
| 44               | 绞盘启用                  | X       |        |       |
| 45               | 绞盘控制                  | X       |        |       |
| 46               | RC 覆盖启用               | X       | X      | X     |
| 47               | 用于自定义功能的回复            | X       |        |       |
| 48               | 用于自定义功能的回复            | X       |        |       |
| 49               | 用于自定义功能的回复            | X       |        |       |
| 50               | 学习游轮                  |         |        | X     |
| 51               | 手动模式                  |         | X      | X     |
| 52               | 阿克罗模式                 | X       |        | X     |
| 53               | 转向模式                  |         |        | X     |
| 54               | 保持模式                  |         |        | X     |
| 55               | 引导模式                  | X       | X      | X     |
| 56               | 徘徊模式                  | X       |        | X     |
| 57               | 关注模式                  | X       |        | X     |
| 58               | 清除航点                  | X       | X      | X     |
| 59               | 简单模式（漫游车）             |         |        | X     |
| 60               | 锯齿形模式                 | X       |        |       |
| 61               | ZIGZAG 模式 - 保存 Waypts | X       |        |       |
| 62               | 指南针学习                 | X       | X      | X     |
| 63               | 帆船钉                   |         |        | X     |
| 64               | 反向油门                  |         | X      |       |
| 65               | 全球定位系统禁用              | X       | X      | X     |
| 66               | 继电器 5 开/关             | X       | X      | X     |
| 67               | 继电器 6 开/关             | X       | X      | X     |
| 68               | 稳定模式                  | X       |        |       |
| 69               | 保有模式                  | X       |        |       |
| 70               | ALTHOLD 模式            | X       | X      |       |
| 71               | 保持模式                  | X       |        |       |
| 72               | 圆形模式                  | X       | X      |       |
| 73               | 漂移模式                  | X       |        |       |
| 74               | 帆船马达 3Pos Sw          |         |        | X     |
| 75               | 表面向上/向下追踪             | X       |        |       |
| 76               | 待机模式                  | X       |        |       |
| 77               | 起飞模式                  |         | X      |       |
| 78               | 运行摄像头控制               | X       | X      | X     |
| 79               | 运行摄像头 OSD 控制          | X       | X      | X     |
| 80               | 维索对齐                  | X       |        |       |
| 81               | 缴械                    | X       | X      | X     |
| 82               | Q\_Assist 3Pos Sw     |         | X      |       |
| 83               | 锯齿形汽车                 | X       |        |       |
| 84               | 飞行模式（非飞行模式）           | X       | X      |       |
| 85               | 发电机                   | X       | X      | X     |
| 86               | 非自动地形跟随 禁用            |         | x      |       |
| 87               | 乌鸦模式切换                |         | X      |       |
| 88               | 翱翔启用                  |         | X      |       |
| 89               | 强制耀斑                  |         | X      |       |
| 90               | EKF 位置来源              | X       | X      | X     |
| 91               | 空速比校准                 |         | X      |       |
| 92               | FBWA 模式               |         | X      |       |
| 94               | VTX 电源                | X       | X      | X     |
| 95               | FBWA\_TAILDRAGGER     |         | X      |       |
| 96               | MODE\_SWITCH\_RESET   | X       | X      | X     |
| 97               | 风向标家庭目录偏移             |         |        | X     |
| 102              | 相机模式切换                | X       | X      | X     |
| 105              | 全球定位系统禁用偏航 （仅测试！      | X       | X      | X     |
| 106              | 禁用空速使用                | X       | X      | X     |
| 107              | 启用自动调整                |         | X      |       |
| 108              | QRTL 模式               |         | X      |       |
| 150              | 巡航模式                  |         | X      |       |
| 151              | 海龟模式                  | X       |        |       |
| 152              | 简单模式航向复位              | X       |        |       |
| 153              | 布防/撤防（4.2 及更高版本）      | X       | X      | X     |
| 154              | 开启空气模式时的布防/撤防         | X       | X      |       |
| 155              | 修剪遥控/伺服保存             |         | X      | X     |
| 156              | 托克多错误清除               |         |        | X     |
| 157              | 强制FBWA长期FS行动          |         | X      |       |
| 158              | 光流校准                  | X       | X      |       |
| 159              | 原力飞行状态                | X       |        |       |
| 160              | 风向标启用                 |         | X      |       |
| 161              | 涡轮启动（直升机）             | X       |        |       |
| 162              | 飞行中FFT自动设置            | X       | X      |       |
| 163              | 安装锁                   | X       | X      | X     |
| 164              | 暂停流式日志记录              | X       | X      | X     |
| 165              | 机械/电机紧急停止             | X       | X      | X     |
| 166              | 摄像机录制视频               | X       | X      | X     |
| 167              | 相机变焦                  | X       | X      | X     |
| 168              | 相机手动对焦                | X       | X      | X     |
| 169              | 相机自动对焦                | X       | X      | X     |
| 170              | Q稳定模式                 |         | X      |       |
| 171              | 指南针校准                 | X       | X      | X     |
| 173              | 飞机自动着陆中止              |         | X      |       |

用作连续 PWM 范围控制输入：

| **RCx\_OPTION值** | **功能说明**   | **直升机** | **飞机** | **车** |
| ---------------- | ---------- | ------- | ------ | ----- |
| 201              | 滚动输入       | X       | X      | X     |
| 202              | PTCH输入     | X       | X      | X     |
| 203              | 油门输入       | X       | X      | X     |
| 204              | 偏航输入       | X       | X      | X     |
| 207              | 主帆         |         |        | X     |
| 208              | 襟翼控制       |         | X      |       |
| 209              | 前进油门       |         | X      |       |
| 210              | 空气制动器      |         | X      |       |
| 211              | 步行机器人高度    |         |        | X     |
| 300-307          | 编写 RC 通道脚本 | X       | X      | X     |

注意

201-204 未实现，保留供将来使用。

### 功能说明[¶](https://ardupilot.org/copter/docs/common-auxiliary-functions.html#description-of-features)

注意

在下面的描述中，通道的低和高分别指PWM <1200us和>1800us。

#### 模式开关[¶](https://ardupilot.org/copter/docs/common-auxiliary-functions.html#mode-switches)

任何以“模式”结尾的功能都可以通过将RC通道设置为高电平来将车辆切换到该模式。您可以有多个“模式”选项开关，并且一次可以有多个高电平。最后一个“模式”更改开关将确定当前模式，以及正常模式开关的任何更改。

例如，如果您激活了“LOITER 模式”开关，然后“自动模式”开关切换为高电平，则该模式将更改为 AUTO。 更改正常飞行模式开关将再次将模式更改为新的飞行模式设置，即使两个RCx\_OPTION模式开关都很高。将活动RCx\_OPTION模式开关降低回低电平会将飞行模式返回到飞行模式通道上设置的任何模式，但前提是当前模式与该开关设置的模式匹配。否则，它将没有效果。

注意

不保证直升机和漫游车模式的更改。如果不满足该模式所需的条件，则可能会被拒绝。例如，如果 GPS 锁定未激活，则在 Copter 中更改为 LOITER 模式将失败，而在 Plane 中，所需模式将更改并尽可能最佳地运行。

注意

如果映射到三位置开关，则超简单模式功能将允许分别使用高位和中间开关位置启用超简单和简单模式（两位开关将仅启用/禁用**超简单**模式）。[有关更多详细信息，请参阅此处](https://ardupilot.org/copter/docs/simpleandsuper-simple-modes.html#simpleandsuper-simple-modes)。

其他功能包括：

| 选择                      | 描述                                                                                                                                                                                                                                                                                                                    |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **空翻**                  | 车辆将根据飞行员的横滚和俯仰杆位置在其横滚或俯仰轴上翻转。请参阅[翻转模式](https://ardupilot.org/copter/docs/flip-mode.html#flip-mode)。                                                                                                                                                                                                                   |
| **保存修剪**                | 在 Rover 中，高电平保存当前转向通道修剪，请参阅[保存转向微调](https://ardupilot.org/rover/docs/savetrim.html#savetrim)。在 Copter 中，它使用当前的横滚和俯仰杆输入调整车辆水平位置。[点击此处](https://ardupilot.org/plane/docs/auto-trim.html#auto-trim)查看详细信息。                                                                                                               |
| **保存航点**                | 将当前位置（包括高度）保存为航点 任务。如果在自动模式下没有航点将被保存，而是车辆将RTL                                                                                                                                                                                                                                                                         |
| **相机触发器**               | 相机快门将被激活。[在此处](https://ardupilot.org/copter/docs/common-camera-shutter-with-servo.html#common-camera-shutter-with-servo)查看更多详细信息。                                                                                                                                                                                     |
| **测距**                  | 当开关处于低位置时，[测距仪](https://ardupilot.org/copter/docs/common-rangefinder-landingpage.html#common-rangefinder-landingpage)被禁用，在处于高位置时启用。                                                                                                                                                                                   |
| **栅栏**                  | 当交换机处于低位置时禁用围栏，在处于高位置时启用围栏。                                                                                                                                                                                                                                                                                           |
| **安科训练器**               | 在 ACRO 飞行模式下打开自动调平。                                                                                                                                                                                                                                                                                                   |
| **喷雾器**                 | 当开关拉高时，打开[作物喷雾器](https://ardupilot.org/copter/docs/sprayer.html#sprayer)。                                                                                                                                                                                                                                             |
| **片 梭**                 | 操作[夹持器](https://ardupilot.org/copter/docs/common-gripper-landingpage.html#common-gripper-landingpage)。开关拉低释放夹持器，高关闭或抓取。                                                                                                                                                                                               |
| **降落伞启用**               | 启用[降落伞](https://ardupilot.org/copter/docs/common-parachute.html#common-parachute)的自动释放（这不会立即触发释放）。                                                                                                                                                                                                                    |
| **降落伞释放**               | 只要飞行器没有着陆或太低，就会立即触发[降落伞](https://ardupilot.org/copter/docs/common-parachute.html#common-parachute)的释放。                                                                                                                                                                                                                |
| **降落伞 3Pos**            | 开关拉低将禁用[降落伞](https://ardupilot.org/copter/docs/common-parachute.html#common-parachute)。中间的开关使降落伞能够自动释放。开关拉高触发降落伞的释放，只要飞行器没有着陆或太低。                                                                                                                                                                                     |
| **任务重置**                | 重置 AUTO 以运行命令列表中的第一个任务命令。                                                                                                                                                                                                                                                                                             |
| **阿特康前馈**               | 打开/关闭姿态控制器向前馈送。仅供开发人员使用。                                                                                                                                                                                                                                                                                              |
| **AttCon 加速限制**         | 打开/关闭姿态控制器加速度限制。仅供开发人员使用。                                                                                                                                                                                                                                                                                             |
| **缩回支架**                | 将[相机支架](https://ardupilot.org/copter/docs/common-cameras-and-gimbals.html#common-cameras-and-gimbals)移动到其缩回位置。                                                                                                                                                                                                        |
| **继电器 1 开/关**           | 开关拉低关闭第一个继电器，拉高匝关闭第一个[继电器](https://ardupilot.org/copter/docs/common-relay.html#common-relay)。                                                                                                                                                                                                                         |
| **起落架**                 | 展开或收回[起落架](https://ardupilot.org/copter/docs/common-landing-gear.html#common-landing-gear)                                                                                                                                                                                                                            |
| **车辆丢失警报**              | 通过蜂鸣器播放[丢失的直升机警报](https://download.ardupilot.org/downloads/wiki/pixhawk\_sound\_files/LostCopter.wav)                                                                                                                                                                                                                 |
| **急停电机**                | 立即停止电机 （[视频](https://www.youtube.com/watch?v=-Db4u8LJE5w))                                                                                                                                                                                                                                                            |
| **电机联锁**                | 电机联锁控制传统直升机和直升机四轮摩托车中产生heliRSC（电机油门控制）输出的方式。如果> 1200us，则启用电机联锁功能，下方禁用。当<1200us时，它类似于传统直升机和直升机四轮直升机的RC直升机术语中有时称为油门保持。对于多旋翼飞机，当<1200us时，它用作电机停止功能。（[视频](https://youtu.be/-Db4u8LJE5w?t=51)）。                                                                                                                            |
| **制动**                  | 当开关变高时调用[制动飞行模式](https://ardupilot.org/copter/docs/brake-mode.html#brake-mode)。 将开关恢复为低电平将使车辆返回到该模式 由 CH5 飞行模式开关指示。                                                                                                                                                                                                   |
| **继电器2 开/关**            | 开关拉低关闭第二个继电器，拉高匝关闭第二个[继电器](https://ardupilot.org/copter/docs/common-relay.html#common-relay)。                                                                                                                                                                                                                         |
| **继电器3 开/关**            | 开关拉低关闭第三个继电器，拉高匝关闭第三个[继电器](https://ardupilot.org/copter/docs/common-relay.html#common-relay)。                                                                                                                                                                                                                         |
| **继电器4 开/关**            | 开关拉低关闭第四[个继电器](https://ardupilot.org/copter/docs/common-relay.html#common-relay)，拉高匝关闭第四个继电器。                                                                                                                                                                                                                         |
| **扔**                   | 当开关变高时调用[投掷飞行模式](https://ardupilot.org/copter/docs/throw-mode.html#throw-mode)。 将开关恢复为低电平将使车辆返回到该模式 由 CH5 飞行模式开关指示。                                                                                                                                                                                                   |
| **ADSB-避免**             | 当开关为高电平时，[ADSB避让（避](https://ardupilot.org/copter/docs/common-ads-b-receiver.html#common-ads-b-receiver)让有人驾驶飞机）启用，否则禁用                                                                                                                                                                                                |
| **精密游荡器**               | 打开/关闭[精确悬停器](https://ardupilot.org/copter/docs/precision-landing-with-irlock.html#precision-landing-with-irlock)。即使用红外锁定传感器在悬停模式下保持目标上方的位置。                                                                                                                                                                           |
| **物体回避**                | 当开关为高电平时，请避开使用 [Lightware SF40c](https://ardupilot.org/copter/docs/common-lightware-sf40c-objectavoidance.html#common-lightware-sf40c-objectavoidance) 或 [TeraRanger Tower](https://ardupilot.org/copter/docs/common-teraranger-tower-objectavoidance.html#common-teraranger-tower-objectavoidance) 的物体。当较低时，将禁用对象回避。 |
| **布防/撤防（4.1 及更早版本）**    | 如果开关变高，则对车辆进行布防（需进行布防检查）。 如果调低，则解除车辆的武装。                                                                                                                                                                                                                                                                              |
| **倒置飞行**                | 启用倒置飞行只会改变ArduPilot稳定飞行器的方式。每当在稳定模式下启用倒置飞行时，它都会以与正常情况 180 度的滚动来稳定它。除非飞行器能够倒置飞行，否则**请勿**使用此选项。                                                                                                                                                                                                                         |
| **绞盘启用**                | 启用绞盘操作。此通道上的低音可放松绞盘。                                                                                                                                                                                                                                                                                                  |
| **绞盘控制**                | 控制绞盘的速度和方向。低：卷取，中：停止，高：开卷                                                                                                                                                                                                                                                                                             |
| **RC 覆盖启用**             | 这是一个 3 位开关，可启用（高）或禁用（低）地面控制站的 RC 超控。                                                                                                                                                                                                                                                                                  |
| **学习游轮**                | 当切换到高时，这将启动 Rover 上的巡航速度和油门学习序列。请参阅[调整速度和油门](https://ardupilot.org/rover/docs/rover-tuning-throttle-and-speed.html#rover-tuning-throttle-and-speed)。                                                                                                                                                                  |
| **清除航点**                | 清除当前加载的任务航点。                                                                                                                                                                                                                                                                                                          |
| **指南针学习**               | 飞行指南针偏移学习。请参阅“[高级指南针设置”的“](https://ardupilot.org/copter/docs/common-compass-setup-advanced.html#common-compass-setup-advanced)自动偏移校准”部分。                                                                                                                                                                              |
| **帆船钉**                 | 该通道上的任何高到低或从低到高的变化都将在与最后一个方向相反的方向上开始粘合。请参阅帆船[配置和设置](https://ardupilot.org/rover/docs/sailboat-configure.html#sailboat-configure)。                                                                                                                                                                                     |
| **反向油门**                | 当切换为高电平时，力在平面中反转油门以陡峭下降。通常，这是通过[USE\_REV\_THRUST](https://ardupilot.org/plane/docs/parameters.html#use-rev-thrust)参数由飞行模式控制的。有关反向推力设置的更多信息，请参阅[自动着陆](https://ardupilot.org/plane/docs/automatic-landing.html#automatic-landing)。                                                                                      |
| **全球定位系统禁用**            | 通过禁用 GPS 来模拟 GPS 故障。                                                                                                                                                                                                                                                                                                  |
| **继电器 5 开/关**           | 开关拉低关闭第三个继电器，拉高匝关闭第五个[继电器](https://ardupilot.org/copter/docs/common-relay.html#common-relay)。                                                                                                                                                                                                                         |
| **继电器 6 开/关**           | 开关拉低关闭第三个继电器，拉高匝关闭第六个[继电器](https://ardupilot.org/copter/docs/common-relay.html#common-relay)。                                                                                                                                                                                                                         |
| **帆船电机3位开关**            | 这个 3 位开关控制帆船电机。电机总是在高时使用，在低时使用，否则根据需要使用。                                                                                                                                                                                                                                                                              |
| **表面向上/向下追踪**           | 此 3 位开关通过测距仪确定表面跟踪是朝向地面（低）还是天花板（高），否则是禁用。                                                                                                                                                                                                                                                                             |
| **待机**                  | 这使自动导航仪控制回路进入软待机模式，以便并行、冗余的自动导航仪或配套计算机可以控制车辆。PID回路、位置和高度控制器经过修改，以便在随后禁用待机时，自动驾驶仪可以平稳地恢复对车辆的控制。输出或其他外围设备的切换必须通过外部电路完成。                                                                                                                                                                                                 |
| **运行摄像头控制**             | 允许开始和停止兼容的RunCam摄像机的视频录制。查看 [RunCam 相机支持](https://ardupilot.org/copter/docs/common-camera-runcam.html#common-camera-runcam)                                                                                                                                                                                           |
| **运行摄像头 OSD 控制**        | 启用对 RunCam 摄像机 OSD 的控制。查看 [RunCam 相机支持](https://ardupilot.org/copter/docs/common-camera-runcam.html#common-camera-runcam)                                                                                                                                                                                             |
| **VISO 对齐**             | 使外部视觉里程计与当前的自动驾驶仪 AHRS 对齐                                                                                                                                                                                                                                                                                             |
| **缴械**                  | 立即无条件解除车辆的武装。与在直升机中等待[DISARM\_DELAY](https://ardupilot.org/copter/docs/parameters.html#disarm-delay)的紧急停止电机不同。                                                                                                                                                                                                        |
| **Q\_Assist 3Pos SW**   | 低：完全禁用Q\_Assist，中：正常Q\_Assist操作，高：始终Q\_Assist活动。请参阅[驾驶四翼飞机](https://ardupilot.org/plane/docs/quadplane-flying.html#quadplane-flying)的辅助固定翼飞行部分                                                                                                                                                                        |
| **锯齿形线模式自动启用**          | 在锯齿形模式下启用自动锯齿形和喷雾器。查看[锯齿形调整浪模式](https://ardupilot.org/copter/docs/zigzag-mode.html#zigzag-mode)                                                                                                                                                                                                                       |
| **空气模式（非常规飞行模式）**       | 启用和禁用空气模式功能。请参阅[空气模式](https://ardupilot.org/copter/docs/airmode.html#airmode)                                                                                                                                                                                                                                         |
| **发电机**                 | 瑞辰混合动力发电机的模式控制                                                                                                                                                                                                                                                                                                        |
| **非自动地形跟随禁用**           | 在巡航和FBWB模式下禁用地形跟随                                                                                                                                                                                                                                                                                                     |
| **乌鸦模式切换**              | 在不同的 CROW 副翼操作模式之间进行选择                                                                                                                                                                                                                                                                                                |
| **翱翔启用**                | 启用飙升功能操作模式                                                                                                                                                                                                                                                                                                            |
| **强制耀斑**                | 将倾斜电机移动到直立位置，并在着陆倾斜旋翼四平面时可选地设置喇叭口的螺距。中间：飞行员在耀斑期间保持俯仰控制。高：音高设置为 [LAND\_PITCH\_CD](https://ardupilot.org/plane/docs/parameters.html#land-pitch-cd)。                                                                                                                                                                     |
| **EKF 位置来源**            | 允许在最多三个 EKF3 的源集之间手动切换（仅限）。查看 GPS [/ 非 GPS 过渡](https://ardupilot.org/copter/docs/common-non-gps-to-gps.html#common-non-gps-to-gps)                                                                                                                                                                                    |
| **空速比校准**               | 激活飞行中空速比的校准。最佳结果发生在执行随时间推移超过 360 度的航向变化时，如在 LOITER 模式下。请参阅[校准空速传感器](https://ardupilot.org/plane/docs/calibrating-an-airspeed-sensor.html#calibrating-an-airspeed-sensor)。                                                                                                                                             |
| **VTX 电源**              | 允许读取多达 6 位开关，用于控制视频发射器功率。请参阅[视频传输器支持](https://ardupilot.org/copter/docs/common-vtx.html#common-vtx)。                                                                                                                                                                                                                  |
| **FBWA\_TAILDRAGGER**   | 启用FBWA后三点式起飞模式，将升降舵和尾翼保持在地面上，直到达到空速                                                                                                                                                                                                                                                                                   |
| **MODE\_SWITCH\_RESET** | 强制重新读取模式开关。                                                                                                                                                                                                                                                                                                           |
| **风向标返航标返航向偏移**         | 这是一个连续的输入通道，当使用 [WNDVN\_TYPE](https://ardupilot.org/rover/docs/parameters.html#wndvn-type) = 45 时，提供初始风向的 -45 至 +2 度偏移。                                                                                                                                                                                               |
| **相机模式切换**              | 切换相机模式（照片/视频/等）。理想情况下，这应该在瞬时开关上，因为只有从低到高的过渡才能切换相机模式。目前仅与独奏万向节一起使用。                                                                                                                                                                                                                                                    |
| **全球定位系统禁用偏航**          | 禁用偏航进行测试（仅限高级用户！                                                                                                                                                                                                                                                                                                      |
| **禁用空速使用**              | 强制空速 禁用用于空中测试。                                                                                                                                                                                                                                                                                                        |
| **启用自动调整**              | 允许在不进入自动调谐模式的情况下进行调谐。（即，如果您在启用摇杆混合的情况下将车辆置于 LOITER/AUTO 状态，它可以在车辆使用摇杆徘徊时自动调谐，但启用自动整定可以在手动以外的任何模式下发生。                                                                                                                                                                                                                  |
| **简单模式航向复位**            | 将原始标题引用重置为 SIMPLE 模式的当前标题。                                                                                                                                                                                                                                                                                            |
| **布防/撤防（4.2 及更高版本）**    | 如果开关变高，则对车辆进行布防（需进行布防检查）。 如果调低，则无条件解除车辆的武装。                                                                                                                                                                                                                                                                           |
| **开启空气模式时的布防/撤防**       | 在 AIRMODE 激活的情况下，如果开关变高（需经过布防检查），则对车辆进行布防。空气模式 rc 选项开关随后可以启用或禁用（如果已配置）。如果调低，则无条件解除车辆的武装。                                                                                                                                                                                                                              |
| **修剪遥控/伺服保存**           | 保存当前 RC 输入调整和 SERVO 输出调整以用于俯仰。滚动，并在飞机上偏航，在漫游车中转向。                                                                                                                                                                                                                                                                     |
| **托克多错误清除**             | 清除托克伊多电机控制器中的错误情况。                                                                                                                                                                                                                                                                                                    |
| **强制FBWA作为长FS行动**       | 在长FS中强制模式更改为FBWA，覆盖超出RC控制范围的紧急着陆的[FS\_LONG\_ACTN](https://ardupilot.org/plane/docs/parameters.html#fs-long-actn)参数值，以防止发生正常的故障操作。                                                                                                                                                                                     |
| **光流校准**                | 能够校准光流参数。                                                                                                                                                                                                                                                                                                             |
| **原力飞行**                | 禁用着陆检测启发式，以防止在任务或手动飞行期间由于阵风等原因突然发生Z变化时进行错误着陆检测。                                                                                                                                                                                                                                                                       |
| **风向标启用**               | 在四平面 VTOL 模式下启用或禁用风向标。                                                                                                                                                                                                                                                                                                |
| **涡轮启动（直升机）**           | 当武装且 RSC 怠速时，高位置向直升机旋翼调速器发出信号，将油门提升到完全并返回怠速状态，从而向涡轮发动机 ECU 发出启动序列的信号。开关必须调低，并且必须撤防飞机才能重新启用此功能。                                                                                                                                                                                                                        |
| **飞行中FFT自动设置**          | 允许自动设置飞行中FFT陷波参数。设置[FFT\_ENABLE](https://ardupilot.org/copter/docs/parameters.html#fft-enable)=1，开关低起飞，开关高悬停30秒，开关低，着陆和缺口参数已配置。                                                                                                                                                                                       |
| **安装锁**                 | 如果高，则将所有支架的航向锁定到地球框架，否则，偏航方向锁定到车辆航向。如果飞行员控制定位处于活动状态，则飞行员的输入会在所选的任何帧中适当地改变航向目标。没有这个开关，它的车辆就会驶向。                                                                                                                                                                                                                        |
| **暂停流式日志记录**            | 如果很高，则不会记录流类型日志消息（传感器，态度，ekf等），以仅允许在具有有限日志记录能力（即没有SD卡）的自动驾驶仪需要时才允许日志记录。事件、模式更改等仍处于记录状态。如果开关为低电平，日志记录不受影响。                                                                                                                                                                                                             |
| **机械/电机紧急停止**           | 三档位开关。如果高，将要求布防。如果切换到低位，将紧急停止任何旋转电机输出，如电机急停开关。如果切换到中间位置，将停用电机紧急停止，但不请求手臂条件。这是ARM/DISARM更安全的替代方案，因为意外切换到低位置不会解除武装，并且如果快速切换回中位或高位，则可以在空中恢复。                                                                                                                                                                             |
| **摄像机录制视频**             | 控制某些摄像机/支架上的视频录制。                                                                                                                                                                                                                                                                                                     |
| **相机变焦**                | 控制某些摄像机/支架上的摄像机变焦。                                                                                                                                                                                                                                                                                                    |
| **相机手动对焦**              | 更改某些相机/卡口上的手动对焦。                                                                                                                                                                                                                                                                                                      |
| **相机自动对焦**              | 控制某些相机/支架上的自动对焦。                                                                                                                                                                                                                                                                                                      |
| **指南针校准**               | 切换到高电平的行为与按下[板载校准](https://ardupilot.org/copter/docs/common-compass-calibration-in-mission-planner.html#onboard-calibration)的“开始”按钮的行为相同。如果仍在进行，将开关恢复为低电平将取消校准。                                                                                                                                                       |
| **飞机自动模式着陆中止**          | 如果切换到高位置，将在自动模式下中止当前正在进行的任何着陆，这包括任何自动任务的垂直起降或固定翼着陆阶段，以及[PAYLOAD\_PLACE](https://ardupilot.org/copter/docs/common-mavlink-mission-command-messages-mav\_cmd.html#mav-cmd-nav-payload-place)任务命令。它不会影响垂直起降着陆、QLAND 或 QRTL 模式的固定翼进近阶段。                                                                                   |
| **滚动输入**                | 滚动输入通道。（取代RCMAP）                                                                                                                                                                                                                                                                                                      |
| **音高输入**                | 俯仰输入通道。（取代RCMAP）                                                                                                                                                                                                                                                                                                      |
| **油门输入**                | 油门输入通道。（取代RCMAP）                                                                                                                                                                                                                                                                                                      |
| **偏航输入**                | 偏航输入通道。（取代RCMAP）                                                                                                                                                                                                                                                                                                      |
| **曼斯泰尔**                | 此RC通道将驱动MainSail输出的输出（= 89），而不是 从油门输入通道设置（如果它有一个使用该输入的辅助电机，则很有用）。有关主帆设置的详细信息，请参阅帆船[配置和设置](https://ardupilot.org/rover/docs/sailboat-configure.html#sailboat-configure)。`SERVOx_FUNCTION`                                                                                                                              |
| **皮 瓣**                 | 该RC通道可手动控制襟翼偏转量，也可与[自动襟](https://ardupilot.org/plane/docs/automatic-flaps.html#automatic-flaps)翼和/或[襟副翼](https://ardupilot.org/plane/docs/flaperons-on-plane.html#flaperons-on-plane)配合使用。（替换旧的FLAP\_IN\_CHANNEL参数）                                                                                                   |
| **前进油门**                | QSTABILIZE、QACRO 和 QHOVER 模式下的手动前进电机油门                                                                                                                                                                                                                                                                                |
| **空气制动器**               | 控制[空气制动器的](https://ardupilot.org/plane/docs/airbrakes-on-plane.html#airbrakes-on-plane)展开                                                                                                                                                                                                                             |
| **步行机器人高度**             | 步行机器人高度的输入通道。参见[步行机器人](https://ardupilot.org/rover/docs/walking-robots.html#walking-robots)。                                                                                                                                                                                                                          |
| **编写 RC 通道脚本**          | 允许读取脚本输入的专用 RC 通道                                                                                                                                                                                                                                                                                                     |

### 检查通道范围[¶](https://ardupilot.org/copter/docs/common-auxiliary-functions.html#check-the-channel-range)

[![../\_images/aux-switch-check.png](https://ardupilot.org/copter/\_images/aux-switch-check.png)](https://ardupilot.org/copter/\_images/aux-switch-check.png)

当辅助开关的 pwm 值高于 1800 时，将触发配置的功能。当值低于 1200 时，它将停用。

您可以使用任务规划器的初始设置>>强制硬件>>无线电校准屏幕检查交换机在开关高电平和低电平时从发射器发送的 pwm 值。如果不爬升到1800以上或低于1200，最好调整变送器中的伺服端点。
