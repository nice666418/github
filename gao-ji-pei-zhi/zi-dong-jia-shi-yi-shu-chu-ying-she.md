# 自动驾驶仪输出映射

## 自动驾驶仪输出功能[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#autopilot-output-functions)

所有自动驾驶仪伺服/电机输出都可以映射到 ArduPilot。本页介绍如何配置这些输出通道以及每个输出通道的内容 可以分配给输出的可用函数是。

ArduPilot 支持多达 32 个输出。这些可以通过DroneCAN电调或直接从自动驾驶仪输出，或两者的混合。

注意

请参阅主要输出类别的左侧边栏菜单，以快速导航到此页面上的所需功能。

### SERVOn\_FUNCTION参数[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#the-servon-function-parameters)

在GCS的高级参数视图中，您会发现每个 伺服输出通道有一个参数。例如，[SERVO5\_FUNCTION](https://ardupilot.org/copter/docs/parameters.html#servo5-function)控制通道5的输出功能，[SERVO6\_FUNCTION](https://ardupilot.org/copter/docs/parameters.html#servo6-function)控制通道6的输出功能等。`SERVOn_FUNCTION`

并非所有功能在每辆车上都可用。首次加载车辆类型的固件时，默认值设置为 0。选择框架 在初始设置期间，任务规划器中的配置会将输出设置为该帧类型的基本典型功能。例如 固定翼飞机将分别将前四个输出SERVO1-SERVO4设置为副翼，升降舵，油门和方向舵功能。

所有这些功能都可以在多个通道上使用。所以如果你 想要 3 个电梯通道 出于某种原因，您可以在 19 个输出通道上设置为 3。`SERVOn_FUNCTION`

### 配置[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#configuration)

可以使用任务规划器的伺服选项卡或通过直接设置输出参数来完成配置。`SERVOx_FUNCTION`

[![../\_images/rcoutput-mapping.png](https://ardupilot.org/copter/\_images/rcoutput-mapping.png)](https://ardupilot.org/copter/\_images/rcoutput-mapping.png)

例如，如果您希望将 Copter quad-x 机架的电机从[小猫角默认](https://ardupilot.org/copter/docs/connect-escs-and-motors.html#connect-escs-and-motors)重新订购为更合乎逻辑的顺时针方法，请进行以下更改：

* [SERVO1\_FUNCTION](https://ardupilot.org/copter/docs/parameters.html#servo1-function)保留为 33（又名“motor1”，右前方）
* [SERVO2\_FUNCTION](https://ardupilot.org/copter/docs/parameters.html#servo2-function)从 34（又名“motor2”，左后）更改为 36（电机 #4，右后）
* [SERVO3\_FUNCTION](https://ardupilot.org/copter/docs/parameters.html#servo3-function)从 35（又名“motor3”，左前方）更改为 34（电机 #2，左后方）
* [SERVO4\_FUNCTION](https://ardupilot.org/copter/docs/parameters.html#servo4-function)从 36（又名“motor4”，右后）更改为 35（电机 #3，左前）

### 泛型函数[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#generic-functions)

| 功能           | 身份证 | 提供：          |
| ------------ | --- | ------------ |
| 禁用           | 0   | 飞机， 直升机， 漫游车 |
| RCPassThru   | 1   | 飞机， 直升机， 漫游车 |
| RCPassThru1  | 51  | 飞机， 直升机， 漫游车 |
| RCPassThru2  | 52  | 飞机， 直升机， 漫游车 |
| RCPassThru3  | 53  | 飞机， 直升机， 漫游车 |
| RCPassThru4  | 54  | 飞机， 直升机， 漫游车 |
| RCPassThru5  | 55  | 飞机， 直升机， 漫游车 |
| RCPassThru6  | 56  | 飞机， 直升机， 漫游车 |
| RCPassThru7  | 57  | 飞机， 直升机， 漫游车 |
| RCPassThru8  | 58  | 飞机， 直升机， 漫游车 |
| RCPassThru9  | 59  | 飞机， 直升机， 漫游车 |
| RCPassThru10 | 60  | 飞机， 直升机， 漫游车 |
| RCPassThru11 | 61  | 飞机， 直升机， 漫游车 |
| RCPassThru12 | 62  | 飞机， 直升机， 漫游车 |
| RCPassThru13 | 63  | 飞机， 直升机， 漫游车 |
| RCPassThru14 | 64  | 飞机， 直升机， 漫游车 |
| RCPassThru15 | 65  | 飞机， 直升机， 漫游车 |
| RCPassThru16 | 66  | 飞机， 直升机， 漫游车 |
| RCIN1缩放      | 140 | 飞机， 直升机， 漫游车 |
| RCIN2缩放      | 141 | 飞机， 直升机， 漫游车 |
| RCIN3缩放      | 142 | 飞机， 直升机， 漫游车 |
| RCIN4缩放      | 143 | 飞机， 直升机， 漫游车 |
| RCIN5缩放      | 144 | 飞机， 直升机， 漫游车 |
| RCIN6缩放      | 145 | 飞机， 直升机， 漫游车 |
| RCIN7缩放      | 146 | 飞机， 直升机， 漫游车 |
| RCIN8缩放      | 147 | 飞机， 直升机， 漫游车 |
| RCIN9缩放      | 148 | 飞机， 直升机， 漫游车 |
| RCIN10缩放     | 149 | 飞机， 直升机， 漫游车 |
| RCIN11缩放     | 150 | 飞机， 直升机， 漫游车 |
| RCIN12缩放     | 151 | 飞机， 直升机， 漫游车 |
| RCIN13缩放     | 152 | 飞机， 直升机， 漫游车 |
| RCIN14缩放     | 153 | 飞机， 直升机， 漫游车 |
| RCIN15缩放     | 154 | 飞机， 直升机， 漫游车 |
| RCIN16缩放     | 155 | 飞机， 直升机， 漫游车 |

#### 禁用[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#disabled)

对于正常操作，禁用输出功能设置输出值 的通道为 0，即没有发送 PWM 脉冲。例外情况是当 使用通道或任务伺服组的 MAVLink 覆盖。所以在 有些方式“残疾”可以称为“任务控制”。

当您执行自动任务时，您可以要求将舵机设置为 价值是该使命的一部分。在这种情况下，您应该设置 将该通道SERVOn\_FUNCTION为“已禁用”，以便该值不会 任务结束后立即被另一个输出函数更改 设置值。

#### RCPassThru[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#rcpassthru)

将通道设置为 RCPassThru 意味着它将输出以下值： 从相应的输入通道进入电路板。例如 如果[SERVO5\_FUNCTION](https://ardupilot.org/copter/docs/parameters.html#servo5-function)为 1（表示 RCPassThru），则通道 5 输出将 始终等于通道 5 输入。

注意

伺服输出将与 RC 输入源的 PWM 值完全匹配。RCx\_TRIM/\_MIN/\_MAX 和 SERVOx\_TRIM/\_MIN/\_MAX 在此模式下没有影响。

#### RCPassThru1 to RCPassThru16[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#rcpassthru1-to-rcpassthru16)

这与上面解释的RCPassThru相同。但是，可以分配任何RC输入来控制此输出，而不是由输入控制输出。例如，RCPassThru 1 （51） 将分配 RC 通道 1 输入来控制输出。因此，对于输出 1，将 51 分配给[SERVO1\_FUNCTION](https://ardupilot.org/copter/docs/parameters.html#servo1-function)与将 RC 通道 1 传递给输出的值 1 相同。`SERVOxRCx`

#### RCIN1Scaled to RCIN16Scaleed[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#rcin1scaled-to-rcin16scaled)

此操作类似于上面的 RCPassThru1 到 RCPassThru16。但是，不是将接收到的PWM精确地传递到输出，而是对其进行缩放。RC输入的死区（DZ）也受到遵守。

从输入微调值到最大输入的上限PWM范围将转换为其相应输出的调整到最大参数值范围，对于低于输入微调值的范围，类似地，如下所示：

[![../\_images/rcscaled-io.jpg](https://ardupilot.org/copter/\_images/rcscaled-io.jpg)](https://ardupilot.org/\_images/rcscaled-io.jpg)

注意

SERVx\_MIN/MAX 值可能大于任务规划器在某些演示文稿中允许的值。使用“配置/完整参数树”视图将参数设置为其正常的“安全”范围。

### 平面功能（也适用于四平面）[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#plane-functions-also-applies-to-quadplanes)

| 功能      | 身份证 | 提供：          |
| ------- | --- | ------------ |
| 副翼      | 4   | 飞机           |
| 电梯      | 19  | 飞机           |
| 节流阀     | 70  | 飞机， 直升机， 漫游车 |
| 油门左     | 73  | 飞机， 直升机， 漫游车 |
| 油门右     | 74  | 飞机， 直升机， 漫游车 |
| 舵       | 21  | 飞机           |
| 皮 瓣     | 2   | 飞机           |
| 自动襟翼    | 3   | 飞机           |
| 左襟副翼    | 24  | 飞机           |
| 襟副翼右    | 25  | 飞机           |
| 埃隆左     | 77  | 飞机           |
| 埃隆右     | 78  | 飞机           |
| V型尾部左   | 79  | 飞机           |
| V型尾右    | 80  | 飞机           |
| 差速扰流板左1 | 16  | 飞机           |
| 差速扰流板右1 | 17  | 飞机           |
| 差速扰流板左2 | 86  | 飞机           |
| 差速扰流板右2 | 87  | 飞机           |
| 地面转向    | 26  | 飞机， 漫游车      |
| 增压发动机油门 | 81  | 直升机，四翼飞机     |
| 电机使能开关  | 30  | 直升机，四翼飞机     |
| 起落架     | 29  | 直升机， 飞机      |
| 空气制动器   | 110 | 飞机           |

#### 副翼[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#aileron)

副翼输出功能提供副翼输出，具有 它自己的每通道微调和范围。当您想要时，这很有用 单独修剪每个副翼，或者如果您的主横滚控制设置为[ELEVONS](https://ardupilot.org/plane/docs/guide-elevon-plane.html#guide-elevon-plane)，并且您还需要一些 普通副翼。

#### 电梯[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#elevator)

电梯输出功能提供电梯输出。可以有多个输出，每个输出具有 单独的每通道调整和范围。当您想要时，这很有用 单独修剪每个电梯，或者如果您的主俯仰控制设置为[ELEVONS](https://ardupilot.org/plane/docs/guide-elevon-plane.html#guide-elevon-plane)，并且您还需要一些 普通电梯。

#### 节流阀[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#throttle)

用于车辆电机功率控制的典型伺服输出。多引擎车辆可以使用多个输出。普通固定翼飞机、单旋翼直升机和漫游车的主功率控制输出。

#### 油门左/右[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#throttle-left-right)

在平面中，这些输出用于双引擎飞机的差分推力，影响基本节气门值的偏航量由[RUDD\_DT\_GAIN](https://ardupilot.org/plane/docs/parameters.html#rudd-dt-gain)确定。此外，在Plane的矢量尾座中，这些是电机输出。在 Rover 中，这些输出用于控制[滑移转向漫游车](https://ardupilot.org/rover/docs/rover-motor-and-servo-configuration.html#rover-motor-and-servo-configuration-skid)中的转向电机。在直升机中，这些输出用于Bicopter电机。

#### 舵[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#rudder)

方向舵输出功能提供具有自身方向舵输出 每个通道的调整和范围。单独的方向舵通道特别 适用于前轮转向可能需要前轮的位置 与普通方向舵通道或多轮相比反转 飞机。

#### 皮 瓣[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#flap)

当通道设置为襟翼时，其值来自通过为其分配 = 208 选择的襟翼 rc 输入通道和/或[自动摆动](https://ardupilot.org/plane/docs/automatic-flaps.html#automatic-flaps)功能。您可能想使用它而不是 RCPassThru 的原因是您可以设置 具有不同装饰和范围的多个襟翼通道，您可能需要 利用[FLAP\_SLEWRATE](https://ardupilot.org/plane/docs/parameters.html#flap-slewrate)来限制襟翼的速度 运动。`RCx_FUNCTION`

#### 自动襟翼[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#automatic-flaps)

自动襟翼输出功能的行为与襟翼输出类似，不同之处在于它 还可以接受来自[TKOFF\_FLAP\_PCNT](https://ardupilot.org/plane/docs/parameters.html#tkoff-flap-pcnt)和[LAND\_FLAP\_PERCNT](https://ardupilot.org/plane/docs/parameters.html#land-flap-percnt)参数以及[FLAP\_1\_SPEED](https://ardupilot.org/plane/docs/parameters.html#flap-1-speed)、[FLAP\_1\_PERCNT](https://ardupilot.org/plane/docs/parameters.html#flap-1-percnt)、[FLAP\_2\_SPEED](https://ardupilot.org/plane/docs/parameters.html#flap-2-speed)和[FLAP\_2\_PERCNT](https://ardupilot.org/plane/docs/parameters.html#flap-2-percnt)参数的自动襟翼输出控制。除了手动控制。

如果同时设置了 RC 襟翼输入通道 （ = 208） 和自动襟翼 函数集，则施加的襟翼量是两者中的较高者。`RCx_OPTION`

#### 襟副翼[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#flaperons)

使用 SERVOn\_FUNCTION 24 和 25（襟副翼左/襟副翼右）您可以设置 襟副翼，这是兼作襟翼的副翼。它们非常有用 适用于有副翼但没有襟翼的飞机。

有关更多详细信息，请参阅[襟副翼指南](https://ardupilot.org/plane/docs/flaperons-on-plane.html#flaperons-on-plane)部分。

请注意，襟副翼的作用类似于自动或普通襟翼，如上所述的襟翼 输出的组件。

#### 升降左/右[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#elevon-left-right)

为 [Elevons](https://ardupilot.org/plane/docs/guide-elevon-plane.html#guide-elevon-plane) 提供输出。

#### V型尾左/右[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#v-tail-left-right)

为 [V 尾平面](https://ardupilot.org/plane/docs/guide-vtail-plane.html#guide-vtail-plane)提供输出。

#### 差速扰流板左/右[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#differential-spoilers-left-right)

请参阅[差分扰流板](https://ardupilot.org/plane/docs/differential-spoilers.html#differential-spoilers)部分。

#### 地面转向[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#ground-steering)

地面转向输出功能的作用与方向舵输出非常相似 功能，只是它仅在飞机低于[GROUND\_STEER\_ALT](https://ardupilot.org/plane/docs/parameters.html#ground-steer-alt)高度时才起作用。在[海拔高于GROUND\_STEER\_ALT](https://ardupilot.org/plane/docs/parameters.html#ground-steer-alt) 输出将是通道的修剪值。

请参阅有关[设置地面转向](https://ardupilot.org/plane/docs/tuning-ground-steering-for-a-plane.html#tuning-ground-steering-for-a-plane)的单独页面

#### 增压发动机油门[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#boost-engine-throttle)

此输出用于辅助[增压电机](https://ardupilot.org/copter/docs/booster-motor.html#booster-motor)的油门控制，以在多旋翼和四翼飞机应用中添加额外的垂直推力源。

#### 电机使能开关[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#motor-enable-switch)

这提供了一个输出，反映车辆的ARM/DISARM状态，以控制电机使能/终止开关。武装时，它处于SERVOx\_MAX pwm，解除武装时处于SERVOx\_MIN pwm。

#### 起落架[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#landing-gear)

此输出控制直升机和飞机中的起落架伺服。有关更多信息，请参阅[起落架](https://ardupilot.org/copter/docs/landing-gear.html#landing-gear)。

#### 空气制动器[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#airbrakes)

此输出用于空气制动控制。手动输入控制通过 = 210。有关更多信息，请参阅[空气制动器](https://ardupilot.org/plane/docs/airbrakes-on-plane.html#airbrakes-on-plane)。`RCx_OPTION`

### 直升机/四翼飞机功能[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#copter-quadplane-functions)

| 功能      | 身份证 | 提供：                    |
| ------- | --- | ---------------------- |
| 电机 1    | 33  | 直升机，四翼飞机，直升机四翼，传统和双直升机 |
| 电机 2    | 34  | 直升机，四翼飞机，直升机四翼，传统和双直升机 |
| 电机 3    | 35  | 直升机，四翼飞机，直升机四翼，传统和双直升机 |
| 电机 4    | 36  | 直升机，四翼飞机，直升机四翼，传统和双直升机 |
| 电机 5    | 37  | 直升机，四翼飞机，双直升机          |
| 电机 6    | 38  | 直升机，四翼飞机，双直升机          |
| 电机 7    | 39  | 直升机，四翼飞机               |
| 电机 8    | 40  | 直升机，四翼飞机               |
| 电机 9    | 82  | 直升机                    |
| 电机 10   | 83  | 直升机                    |
| 电机 11   | 84  | 直升机                    |
| 电机 12   | 85  | 直升机                    |
| 电机倾斜    | 41  | 四翼飞机                   |
| 油门左     | 73  | 飞机， 直升机， 漫游车           |
| 油门右     | 74  | 飞机， 直升机， 漫游车           |
| 倾斜电机左   | 75  | 直升机，四翼飞机               |
| 向右倾斜电机  | 76  | 直升机，四翼飞机               |
| 后倾电机    | 45  | 四翼飞机                   |
| 倾斜电机左后部 | 46  | 四翼飞机                   |
| 右后倾斜电机  | 47  | 四翼飞机                   |
| 增压发动机油门 | 81  | 直升机，四翼飞机               |
| 电机使能开关  | 30  | 直升机，四翼飞机               |
| 降落伞释放   | 27  | 直升机                    |
| 起落架     | 29  | 直升机， 飞机                |
| 绞车      | 88  | 直升机                    |
| 转子头转速   | 31  | 传统和双直升机，HeliQuad       |
| 尾桨速度    | 32  | 传统直升机                  |

#### 电机 1 - 12[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#motors-1-12)

这些是直升机和四平面垂直起降电机输出。对于多轴飞行器，请参见[电机顺序图](https://ardupilot.org/copter/docs/connect-escs-and-motors.html#connect-escs-and-motors)。或者参见[传统](https://ardupilot.org/copter/docs/traditional-helicopter-connecting-apm.html#traditional-helicopter-connecting-apm)直升机，或单轴直升机[和同轴直升机](https://ardupilot.org/copter/docs/singlecopter-and-coaxcopter.html#singlecopter-and-coaxcopter)，或[HeliQuads（可变螺距多旋翼飞行器）。](https://ardupilot.org/copter/docs/heliquads.html#heliquads)

注意

只能修改使用的输出通道，不能使用这些参数重新定义电机的旋转方向。 Copter-3.5（及更早版本）不支持将相同的功能分配给多个输出通道，但此功能将出现在 Copter-3.6（及更高版本）中。

对于四平面，请参阅电机输出配置的[四平面框架设置](https://ardupilot.org/plane/docs/quadplane-frame-setup.html#quadplane-frame-setup)。

#### 油门左/右[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#id1)

在平面中，这些输出用于双引擎飞机的差分推力，影响基本节气门值的偏航量由[RUDD\_DT\_GAIN](https://ardupilot.org/plane/docs/parameters.html#rudd-dt-gain)确定。此外，在Plane的矢量尾座中，这些是电机输出。在 Rover 中，这些输出用于控制[滑移转向漫游车](https://ardupilot.org/rover/docs/rover-motor-and-servo-configuration.html#rover-motor-and-servo-configuration-skid)中的转向电机。在直升机中，这些输出用于Bicopter电机。

#### 倾斜电机/左倾电机/右倾电机/后倾电机/后倾电机/右倾电机/右倾电机[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#tilt-motor-tilt-motor-left-tilt-motor-right-tilt-motor-rear-tilt-motor-rear-left-tilt-motor-rear-right)

这些输出控制飞机中[倾转旋翼平面](https://ardupilot.org/plane/docs/guide-tilt-rotor.html#guide-tilt-rotor)和直升机中双轴飞行器的倾斜伺服器。

#### 增压发动机油门[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#id2)

此输出用于辅助[增压电机](https://ardupilot.org/copter/docs/booster-motor.html#booster-motor)的油门控制，以在多旋翼和四翼飞机应用中添加额外的垂直推力源。

#### 电机使能开关[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#id3)

这提供了一个输出，反映车辆的ARM/DISARM状态，以控制电机使能/终止开关。武装时，它处于SERVOx\_MAX pwm，解除武装时处于SERVOx\_MIN pwm。

#### 降落伞释放[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#parachute-release)

请参阅[降落伞](https://ardupilot.org/copter/docs/common-parachute.html#common-parachute)部分。

#### 起落架[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#id4)

此输出控制直升机和飞机中的起落架伺服。有关更多信息，请参阅[起落架](https://ardupilot.org/copter/docs/landing-gear.html#landing-gear)。

#### 绞车[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#winch)

此输出控制绞盘，用于在 Copter 中传送物体。

#### 转子头转速[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#rotor-head-speed)

[传统直升机](https://ardupilot.org/copter/docs/traditional-helicopters.html#traditional-helicopters)的电机控制输出。

#### 尾桨速度[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#tail-rotor-speed)

输出到[传统直升机](https://ardupilot.org/copter/docs/traditional-helicopters.html#traditional-helicopters)尾桨电调/调速器（未来增强）。

### 漫游车功能[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#rover-functions)

| 功能   | 身份证 | 提供：                |
| ---- | --- | ------------------ |
| 地面转向 | 26  | 飞机， 漫游车            |
| 节流阀  | 70  | 飞机， 四翼飞机， 直升机， 漫游者 |
| 油门左  | 73  | 飞机， 直升机， 漫游车       |
| 油门右  | 74  | 飞机， 直升机， 漫游车       |
| 主帆板  | 89  | 车                  |

#### 节流阀[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#id5)

用于车辆电机功率控制的典型伺服输出。多引擎车辆可以使用多个输出。普通固定翼飞机、单旋翼直升机和漫游车的主功率控制输出。

#### 油门左/右[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#id6)

在平面中，这些输出用于双引擎飞机的差分推力，影响基本节气门值的偏航量由[RUDD\_DT\_GAIN](https://ardupilot.org/plane/docs/parameters.html#rudd-dt-gain)确定。此外，在Plane的矢量尾座中，这些是电机输出。在 Rover 中，这些输出用于控制[滑移转向漫游车](https://ardupilot.org/rover/docs/rover-motor-and-servo-configuration.html#rover-motor-and-servo-configuration-skid)中的转向电机。在直升机中，这些输出用于Bicopter电机。

#### 主帆板[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#main-sail-sheet)

此输出用于控制基于漫游者的帆船中的主帆。有关详细信息，请参阅[帆船车辆设置](https://ardupilot.org/rover/docs/sailboat-hardware.html#sailboat-hardware)设置。

### 天线跟踪器功能[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#antenna-tracker-functions)

| 功能    | 身份证 | 提供：   |
| ----- | --- | ----- |
| 跟踪器偏航 | 71  | 天线跟踪器 |
| 跟踪器间距 | 72  | 天线跟踪器 |

#### 跟踪器偏航/俯仰[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#tracker-yaw-pitch)

这些输出控制[天线跟踪](https://ardupilot.org/antennatracker/index.html)器的俯仰和偏航伺服。

### 相机/云台功能[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#camera-gimbal-functions)

| 功能        | 身份证 | 提供：          |
| --------- | --- | ------------ |
| 偏航山       | 6   | 飞机， 直升机， 漫游车 |
| 安装间距      | 7   | 飞机， 直升机， 漫游车 |
| 安装辊       | 8   | 飞机， 直升机， 漫游车 |
| 装载部署/收回   | 9   | 飞机， 直升机， 漫游车 |
| 相机触发器     | 10  | 飞机， 直升机， 漫游车 |
| 坐骑2偏航     | 12  | 飞机， 直升机， 漫游车 |
| 安装座2间距    | 13  | 飞机， 直升机， 漫游车 |
| 安装2 卷筒    | 14  | 飞机， 直升机， 漫游车 |
| 装载2 展开/收回 | 15  | 飞机， 直升机， 漫游车 |
| 相机ISO     | 90  | 飞机， 直升机， 漫游车 |
| 相机光圈      | 91  | 飞机， 直升机， 漫游车 |
| 相机对焦      | 92  | 飞机， 直升机， 漫游车 |
| 相机快门速度    | 93  | 飞机， 直升机， 漫游车 |

#### 偏航/俯仰/滚动/展开[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#mount-yaw-pitch-roll-deploy)

它们控制用于控制伺服云台的输出通道。请 有关详细信息，请参阅[相机云台配置文档](https://ardupilot.org/copter/docs/common-camera-gimbal.html#common-camera-gimbal)。

Mount2 选项相同，但控制第二个相机云台。

#### Camera\_trigger[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#camera-trigger)

Camera\_trigger输出功能用于触发具有 伺服。有关详细信息，请参阅[相机云台文档](https://ardupilot.org/copter/docs/common-camera-gimbal.html#common-camera-gimbal)。

#### 相机ISO/光圈/对焦/快门速度[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#camera-iso-aperture-focus-shutter-speed)

这些输出用于远程控制BMMC（Blackmagic Micro Cinema Camera）兼容设备的上述值。

### 内燃机功能[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#internal-combustion-engine-functions)

| 功能  | 身份证 | 提供：          |
| --- | --- | ------------ |
| 点火  | 67  | 飞机， 直升机， 漫游车 |
| 呛   | 68  | _保留供将来使用_    |
| 起动机 | 69  | 飞机， 直升机， 漫游车 |

#### 点火/起动机/扼流圈[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#ignition-starter-choke)

用于控制内燃机的火花塞/点火器、起动电机和扼流圈。参见[内燃机 （ICE）。](https://ardupilot.org/plane/docs/common-ice.html#common-ice)

### 新像素 LED 串[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#neopixel-led-strings)

[新像素LED/](https://ardupilot.org/copter/docs/common-serial-led-neopixel.html#common-serial-led-neopixel)串可以使用 进行控制，从而支持多达四个独立控制的灯串。这些可用于ArduPilot通知和警告（请参阅[通知设备配置](https://ardupilot.org/copter/docs/common-ntf-devices.html#common-ntf-devices)）或通过LUA脚本进行控制（请参阅[Lua脚本](https://ardupilot.org/copter/docs/common-lua-scripts.html#common-lua-scripts)）。 这适用于所有车辆。`Function IDs 120-123`

### 专业发光二极管[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#profileds)

[ProfiLED可以使用](https://ardupilot.org/copter/docs/common-serial-led-ProfiLED.html#common-serial-led-profiled)进行控制，从而支持多达三个串，由一个公共时钟独立控制。这些可用于ArduPilot通知和警告（请参阅[通知设备配置](https://ardupilot.org/copter/docs/common-ntf-devices.html#common-ntf-devices)）或通过LUA脚本进行控制（请参阅[Lua脚本](https://ardupilot.org/copter/docs/common-lua-scripts.html#common-lua-scripts)）。这适用于所有车辆。请参阅 ：ref：`Function IDs 129-132`

### 杂项函数[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#miscellaneous-functions)

| 功能                   | 身份证 | 提供：          |
| -------------------- | --- | ------------ |
| 片 梭                  | 28  | 飞机， 直升机， 漫游车 |
| 蛋滴                   | 11  | 荒废的          |
| 喷雾泵                  | 22  | 直升机          |
| 喷雾搅拌机                | 23  | 直升机          |
| 输出SERVOn\_MIN PWM 值  | 134 | 飞机， 直升机， 漫游车 |
| 输出SERVOn\_TRIM PWM 值 | 135 | 飞机， 直升机， 漫游车 |
| 输出SERVOn\_MAX PWM 值  | 136 | 飞机， 直升机， 漫游车 |

#### 片 梭[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#gripper)

这是用于控制伺服或电磁抓手的输出，用于固定物品以进行交付应用。有关详细信息，请参阅[夹具（用于交付）。](https://ardupilot.org/copter/docs/common-gripper-landingpage.html#common-gripper-landingpage)

#### 喷雾泵/搅拌机[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#sprayer-pump-mixer)

这些输出控制[作物喷雾器](https://ardupilot.org/copter/docs/sprayer.html#sprayer)。

#### 输出伺服 n 最大值/最小值/微调[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#output-servon-max-min-trim)

连续输出为该输出设置的参数值。用于按钮检测。请参阅[按钮](https://ardupilot.org/copter/docs/common-buttons.html#common-buttons)

### 通用 LUA 脚本输出[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#general-purpose-lua-scripting-outputs)

[Lua 脚本](https://ardupilot.org/copter/docs/common-lua-scripts.html#common-lua-scripts)还可以直接控制自动驾驶仪输出。如果自动驾驶仪支持，则能够配置多达 16 个此类输出。这适用于所有车辆。`Function IDs 94-109`

### 内部控制器访问[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#internal-controller-access)

| 功能   | 身份证 | 提供： |
| ---- | --- | --- |
| 率滚动  | 124 | 直升机 |
| 费率间距 | 125 | 直升机 |
| 速率推力 | 126 | 直升机 |
| 拉特亚乌 | 127 | 直升机 |

这些输出提供来自姿态控制回路的前馈项，按横滚/俯仰/偏航的ATC\_RAT\_x\_FF PID参数值进行缩放，以便与外部车辆控制器一起使用。

### 默认值[¶](https://ardupilot.org/copter/docs/common-rcoutput-mapping.html#default-values)

加载固件或选择帧类型时，将为输出功能设置某些默认值。如果需要，用户可以将它们移动到备用伺服/电机输出。默认值如下所示：

| 车辆类型伺服        | 1  | 2  | 3  | 4  | 5  | 6  | 7  | 8  | 9  | 10 | 11 | 12 |
| ------------- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- |
| 多旋翼           | 33 | 34 | 35 | 36 | 37 | 38 | 39 | 40 | 82 | 83 | 84 | 85 |
| 三轴飞行器         | 33 | 34 | 0  | 36 | 0  | 0  | 39 | 0  | 0  | 0  | 0  | 0  |
| 单轴飞行器 / 同轴飞行器 | 33 | 34 | 35 | 36 | 37 | 38 | 0  | 0  | 0  | 0  | 0  | 0  |
| 传统直升机         | 33 | 34 | 35 | 36 | 0  | 0  | 0  | 31 | 0  | 0  | 0  | 0  |
| 双直升机          | 33 | 34 | 35 | 36 | 37 | 38 | 0  | 31 | 0  | 0  | 0  | 0  |
| 直升机四方         | 33 | 34 | 35 | 36 | 0  | 0  | 0  | 31 | 0  | 0  | 0  | 0  |
| 固定翼飞机/尾翼      | 4  | 19 | 21 | 70 | 0  | 0  | 0  | 0  | 0  | 0  | 0  | 0  |
| 四翼飞机          | 4  | 19 | 21 | 70 | 33 | 34 | 35 | 36 | 0  | 0  | 0  | 0  |
| 四翼三轴飞行器       | 4  | 19 | 21 | 70 | 33 | 34 | 0  | 36 | 0  | 0  | 39 | 0  |
| 车             | 26 | 0  | 70 | 0  | 0  | 0  | 0  | 0  | 0  | 0  | 0  | 0  |

> 注意
>
> Rover 滑移车辆需要手动将 SERVO1 和 SERVO3 更改为左油门和右油门以启用滑移转向。
