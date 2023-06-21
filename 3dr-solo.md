# 3DR Solo

## 3DR 独奏 - ArduCopter 大师升级[¶](https://ardupilot.org/copter/docs/solo\_arducopter\_upgrade.html#dr-solo-arducopter-master-upgrade)

本文详细介绍了升级和操作ArduCopter 3.5.0及更高版本的3DR Solo。

### 概述[¶](https://ardupilot.org/copter/docs/solo\_arducopter\_upgrade.html#overview)

3DR Solo包含Pixhawk 2.0自动驾驶仪等许多功能。它带有早期ArduCopter 3.3的高度定制分支，该分支由3DR专门为Solo编译。当您对新的Solo进行初始飞行前更新时（或恢复出厂设置后），该更新的一部分是ArduCopter的Solo分支。它安装在Pixhawk上，并具有所有必要的默认参数和自定义功能。它对用户基本上是透明的，发生在窗帘后面。由于3DR不再从事消费者UAS业务，ArduCopter的这个定制分支将不会看到任何进一步的更新。它最后一次更新是在2016年初，现在远远落后。

#### 3DR 之后的生活[¶](https://ardupilot.org/copter/docs/solo\_arducopter\_upgrade.html#life-after-3dr)

由于Solo使用Pixhawk自动驾驶仪，因此除了3DR定制的Solo版本外，它还能够运行ArduCopter的变体。本文将重点介绍如何在 3DR Solo 上安装、配置和操作 ArduCopter 5.0.3 或更高版本。ArduCopter继续3DR中断的地方，使Solo保持现代，先进和高性能的sUAS。自动驾驶仪固件有无数的进步，使其成为更稳定、可靠和敏捷的飞机。有许多新功能，例如船模式，RTK GPS，增强遥测，ADS-B，激光雷达激光高度计，地形感知和跟随，红外精度着陆以及甚至和“室内GPS”。

[![../\_images/solo\_skids\_here.jpg](https://ardupilot.org/copter/\_images/solo\_skids\_here.jpg)](https://ardupilot.org/copter/\_images/solo\_skids\_here.jpg) [![../\_images/solo\_logos.jpg](https://ardupilot.org/copter/\_images/solo\_logos.jpg)](https://ardupilot.org/copter/\_images/solo\_logos.jpg) [![../\_images/solo\_rtk.jpg](https://ardupilot.org/copter/\_images/solo\_rtk.jpg)](https://ardupilot.org/copter/\_images/solo\_rtk.jpg) [![../\_images/solo\_nightraptor.jpg](https://ardupilot.org/copter/\_images/solo\_nightraptor.jpg)](https://ardupilot.org/copter/\_images/solo\_nightraptor.jpg)

_摄影：Andrew Emmett、Matt Lawrence、Stephan Schindewolf & Paul Dinardi_

\


#### 硬件要求[¶](https://ardupilot.org/copter/docs/solo\_arducopter\_upgrade.html#hardware-requirements)

Pixhawk 2.1 Green Cube（或内部跳线设置为5伏的传统立方体）目前需要安全可靠地在3DR Solo上使用ArduCopter 5.0.3及更高版本。您可以从[Jesters Drones](http://www.jestersdrones.org/store/index.php?rt=product/category\&path=68)购买Green Cube，也可以直接从[ProfiCNC](http://www.proficnc.com/3dr-solo-accessories/79-the-cube.html)购买。立方体具有更先进的组件。这包括 3 个温控 IMU 和 Solo 安全运行所需的 5 伏信号。如果您已经有一个立方体，您可以将内部焊接跳线设置为 5 伏信号并在 Solo 中使用它。绿色立方体带有此预设为 5 伏的跳线。

[![../\_images/solo\_greencube.jpg](https://ardupilot.org/copter/\_images/solo\_greencube.jpg)](https://ardupilot.org/copter/\_images/solo\_greencube.jpg) [![../\_images/solo\_cube\_installed.jpg](https://ardupilot.org/copter/\_images/solo\_cube\_installed.jpg)](https://ardupilot.org/copter/\_images/solo\_cube\_installed.jpg)

_您可以在_库存的Pixhawk 2.0上安装ArduCopter母版，但强烈建议不要这样做。它会安装，它会飞。但是，电机在飞行中关闭的风险相当高，从而导致严重碰撞。这是因为Solo的电机吊舱存在电气硬件缺陷。旧的库存固件有一个软件补丁，_可以在很大程度上_缓解此缺陷。这就是您可能听到的“压摆率保护”。您可以在[其 GitHub 站点上](https://github.com/3drobotics/ardupilot-solo/blob/master/libraries/AP\_Motors/AP\_MotorsMatrix.cpp#L388)查看库存 3DR 固件中的压摆率保护代码。ArduCopter的生产版本，包括ArduCopter 3.5没有这种压摆率保护。对于除了Solo之外使用ArduCopter的车辆世界来说，这是严重的障碍和难以管理。Pixhawk 5.2 Green Cube 中使用的 1 伏信号有效地解决了电机吊舱上的电气问题。

还有其他潜在的方法可以在不购买新立方体的情况下缓解电机吊舱的电气问题。您可以使用传统的 DIY 电调并绕过电机吊舱中内置的电调。或者，您可以构建一个电平转换器，将信号电压从3v升压至5v。这些解决方案都不是作为套件在市场上提供的，但如果您有创意，可以在 DIY 的基础上完成。你不会在The Cube中享受到增强型硬件的好处，但它的飞行同样安全可靠。

您不能在立方体上使用旧库存的 3DR Solo 固件。这是完全不兼容的。这也意味着您无法在独奏上恢复出厂设置，而立方体仍在独奏中。恢复出厂设置会尝试重新加载不兼容的旧Solo固件。如果您需要恢复出厂设置，则需要将旧的Pixhawk 2.0放回原处，运行完整的出厂重置和更新，然后将Green Cube放回原处。这很烦人，但现在或可预见的未来都没有办法解决。简而言之，不需要恢复出厂设置。这也意味着不要丢失您的WiFi密码！不要扔掉你的旧汤块！

\


#### 资源[¶](https://ardupilot.org/copter/docs/solo\_arducopter\_upgrade.html#resources)

网上有几个很棒的资源，用于修改想法、供应商、beta 测试固件、故障排除和支持

* [个人测试脸书组](https://www.facebook.com/groups/617648671719759/)
* [Solo Mod Club Facebook 群组](https://www.facebook.com/groups/3DRSOLOModClub/)
* [Solex Users Facebook 群组](https://www.facebook.com/groups/176789056089526/)
* [ArduPilot 讨论论坛](https://discuss.ardupilot.org/c/arducopter/copter-3-5)
* [ArduPilot copter Wiki](https://ardupilot.org/copter/docs/common-advanced-configuration.html)
* [3DR 飞行员论坛](https://3drpilots.com/)
* [单电池校准过程](https://ardupilot.org/copter/docs/solo\_battery\_calibration.html#solo-battery-calibration)

\
\
\


### 升级过程[¶](https://ardupilot.org/copter/docs/solo\_arducopter\_upgrade.html#upgrade-process)

#### 制备[¶](https://ardupilot.org/copter/docs/solo\_arducopter\_upgrade.html#preparation)

在开始使用Solo上的Pixhawk 3.5 Green Cube升级到ArduCopter 2.1之前，您需要完成一些重要的要求。

* 完整的独奏和控制器处于良好的工作状态，配对，可飞行且充满电。
* Solo和控制器都使用初始飞行前更新的当前3DR Solo固件进行更新。当前的 3DR 固件是 2.4.2。
* 经过飞行测试，各方面都能正常工作。未经测试或出现故障的 Solo 不应用于此过程。它不会修复它。
* 像素鹰 2.1 绿立方
* 飞利浦和平头螺丝刀
* 适用于Android的Solex应用程序或适用于Mission Planner和WinSCP的Windows PC

#### 指示[¶](https://ardupilot.org/copter/docs/solo\_arducopter\_upgrade.html#instructions)

有两种方法可以执行升级，此处发布了详细说明。

* [使用 Solex 应用程序进行初始安装](https://ardupilot.org/copter/docs/solo\_arducopter\_solex\_install.html#solo-arducopter-solex-install)。这是迄今为止最直接和强烈推荐的方法。Solex 具有加载和重置固件和参数的方法，并可以直接在线访问所有必要的文件。
* [使用 Mission Planner 和 WinSCP 进行初始安装](https://ardupilot.org/copter/docs/solo\_arducopter\_other\_install.html#solo-arducopter-other-install)。这种方法稍微复杂一些，但同样成功。您将需要下载 zip 文件，使用任务规划器更改设置，并使用 WinSCP 传输文件。如果您没有Solex应用程序，则需要遵循此方法。

### 首次飞行[¶](https://ardupilot.org/copter/docs/solo\_arducopter\_upgrade.html#first-flight)

升级过程完成后，您就可以在Solo上使用ArduCopter 3.5进行首次飞行了。建议您在允许您测试一些基本功能和安全系统的地点和时间进行首次飞行。选择开阔的没有障碍物，人群，湖泊等。

#### 独奏/索莱克斯应用程序设置[¶](https://ardupilot.org/copter/docs/solo\_arducopter\_upgrade.html#solo-solex-app-settings)

您需要浏览 3DR Solo 应用程序（以及 Solex 应用程序，如果您也使用它）中的所有设置，以验证和更新滑块、选项和设置。本次扫描中要设置的热门项目包括但不限于：

* 第焘列室海拔高度
* RTH/RTM\* & Rewind
* 最大海拔高度
* A/B 按钮
* 高级飞行模式
* 速度滑块
* 戈波设置

#### 空降[¶](https://ardupilot.org/copter/docs/solo\_arducopter\_upgrade.html#go-airborne)

完成上述所有操作后，是时候乘坐ArduCopter大师进行首次飞行了！

* 起飞并验证Solo飞行的稳定性和可预测性。
* 测试所有轴...俯仰、滚动、偏航、爬升、下降，甚至同时进行。
* 测试您在A和B按钮上的飞行模式
* 确保您获得良好的GPS锁
* 确保应用程序和控制器上显示的距离、高度、速度、模式和 GPS 数据正确且符合您的预期。
* 让电池运行到故障保护，同时安全地悬停在附近。观察其行为并验证它是否正确执行了 RTH/RTM 过程。

注意

如果您在此过程期间需要帮助解决问题或有疑问，[Solo Beta Test Facebook群组](https://www.facebook.com/groups/617648671719759/)是最佳选择。

\
\
\


### 直升机参数[¶](https://ardupilot.org/copter/docs/solo\_arducopter\_upgrade.html#arducopter-parameters)

ArduCopter中有700多个参数。对于Solo的日常使用，您仍然无需担心其中任何一个。它们都是在上述过程中和默认为您预设的。Solo的所有配置参数都需要与ArduCopter默认值不同的值，都可以在[ArduPilot GitHub存储库/tools/frame\_params/目录中](https://github.com/ArduPilot/ardupilot/blob/master/Tools/Frame\_params/Solo\_AC35.param)找到。这些是在升级过程中加载的参数。如果您不熟悉编辑参数，并且没有特殊用例来保证更改它们，则不建议更改它们。

但是，有一些高级和特殊用例可能需要更改某些参数。下面详细介绍了高级用户的一些关键参数。随着新用例和修改的发展，此列表可能会增长。

| [COMPASS\_ORIENT](https://ardupilot.org/copter/docs/parameters.html#compass-orient)是外部指南针的方向。 |           |
| --------------------------------------------------------------------------------------------- | --------- |
| 价值                                                                                            | 意义        |
| 38                                                                                            | 右后腿的库存指南针 |
| 0                                                                                             | 这里 外部指南针  |

| [FS\_THR\_ENABLE](https://ardupilot.org/copter/docs/parameters.html#fs-thr-enable)控制Solo如何响应来自控制器的信号丢失。 |                                                     |
| ------------------------------------------------------------------------------------------------------- | --------------------------------------------------- |
| 价值                                                                                                      | 意义                                                  |
| 0                                                                                                       | 无故障保护。不应使用此方法。                                      |
| 1                                                                                                       | 如果 GPS 可用，则 RTH/RTM 将启动。如果没有GPS，Solo将降落。            |
| 2                                                                                                       | 继续智能拍摄或自动任务。否则为 RTH/RTM（如果 GPS 可用）。如果没有GPS，Solo将降落。 |
| 3                                                                                                       | 仅限陆地，没有 RTH/RTM。这对于室内飞行很有用。                         |

| FS\_BATT\_ENABLE控制 Copter-3.5（及更早版本）的低电池电量故障保护操作。对于 Copter-3.6（及更高版本），请检查[BATT\_FS\_LOW\_ACT](https://ardupilot.org/copter/docs/parameters.html#batt-fs-low-act)参数。当参数中设置的值或被违反时，低电池电量故障保护启动。`FS_BATT_VOLTAGEFS_BATT_MAH` |                         |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------- |
| 价值                                                                                                                                                                                                                        | 意义                      |
| 0                                                                                                                                                                                                                         | 无故障保护操作                 |
| 1                                                                                                                                                                                                                         | 立即降落，没有RTH / RTM。适用于室内。 |
| 2                                                                                                                                                                                                                         | RTH/RTM                 |

| FS\_BATT\_VOLTAGE是Copter-3.5（及更早版本）的低电池电压阈值。对于 Copter-3.6（及更高版本），请检查[BATT\_LOW\_VOLT](https://ardupilot.org/copter/docs/parameters.html#batt-low-volt)参数。当电池电压降至此点以下时，低电量蜂鸣器会响起，它将执行您设置的操作。此值以伏特表示。默认值为 14.0。您可以根据用例和首选项将其调整得更高或更低。`FS_BATT_ENABLE` |             |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| 价值                                                                                                                                                                                                                                                  | 意义          |
| 0                                                                                                                                                                                                                                                   | 无低电压报警或故障保护 |
| 14                                                                                                                                                                                                                                                  | 14 伏        |

| FS\_BATT\_MAH是 Copter-3.5（及更早版本）的电池剩余容量阈值，以毫安 （MAH） 表示。对于 Copter-3.6（及更高版本），请检查 [BATT\_LOW\_MAH](https://ardupilot.org/copter/docs/parameters.html#batt-low-volt) 参数。当电池剩余容量降至此点以下时，低电量蜂鸣器会响起，它将执行您设置的操作。默认值为 520。在单人飞行中，平均剩余约1.5分钟的飞行时间。您可以向上或向下调整此设置以适合您的偏好和用例。将其设置为 0 将禁用基于剩余容量的警报和故障保护。`FS_BATT_ENABLE` |                |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------- |
| 价值                                                                                                                                                                                                                                                                                                          | 意义             |
| 0                                                                                                                                                                                                                                                                                                           | 无电池剩余容量报警或故障保护 |
| 520                                                                                                                                                                                                                                                                                                         | 520毫安时         |

| [WP\_YAW\_BEHAVIOR](https://ardupilot.org/copter/docs/parameters.html#wp-yaw-behavior)指定自动任务和 RTH/RTM 中的偏航行为。 |                               |
| ------------------------------------------------------------------------------------------------------------- | ----------------------------- |
| 价值                                                                                                            | 意义                            |
| 0                                                                                                             | 没有变化。Solo的偏航将一直指向同一方向，除非您更改它。 |
| 1                                                                                                             | 无论飞行方向如何，都要面对下一个航点。           |
| 2                                                                                                             | 面向下一个航点，但在 RTH/RTM 中除外。       |
| 3                                                                                                             | 沿着GPS路线面向前方。                  |

| **NTF\_OREO\_THEME**控制Solo的电机吊舱LED主题。这仅适用于ArduCopter 3.5.0及更高版本。 |                                 |
| ---------------------------------------------------------------- | ------------------------------- |
| 价值                                                               | 意义                              |
| 0                                                                | 禁用                              |
| 1                                                                | 飞机主题，前部为红色/绿色，后部为白色频闪。          |
| 2                                                                | Rover主题与白色正面和红色后部（就像曾经的股票Solo）。 |

| [AHRS\_GPS\_USE](https://ardupilot.org/copter/docs/parameters.html#ahrs-gps-use)用于启用或禁用您Solo上的GPS。默认值为 1 表示已启用。禁用 GPS 的主要用例是室内飞行。如果 GPS 被禁用，它不能也不会尝试将其用于飞行、故障保险或任何其他功能。这意味着 RTH 模式不可用。您必须熟悉故障保护在没有 GPS 的情况下的工作原理。在大多数情况下，Solo会着陆，因为它不能RTH。 |           |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------- |
| 价值                                                                                                                                                                                                                                         | 意义        |
| 0                                                                                                                                                                                                                                          | 全球定位系统已禁用 |
| 1                                                                                                                                                                                                                                          | 启用全球定位系统  |

| [LOG\_DISARMED](https://ardupilot.org/copter/docs/parameters.html#log-disarmed)在 Solo 撤防时启用和禁用数据闪存 （\*.bin） 日志记录。它目前默认处于启用状态，因为它对于测试和故障排除非常有用。但它确实会导致大量且通常不必要的日志。如果您对 Solo 感到满意和自信，则可以在解除武装时禁用日志记录。数据闪存日志更加干净和庞大。 |                        |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| 价值                                                                                                                                                                                                                | 意义                     |
| 0                                                                                                                                                                                                                 | 已禁用/撤防时无数据闪存日志记录       |
| 1                                                                                                                                                                                                                 | 启用/数据闪存日志记录，同时解除武装和武装。 |

### 更多信息[¶](https://ardupilot.org/copter/docs/solo\_arducopter\_upgrade.html#further-information)

* [3DR Solo - 使用Mission Planner和WinSCP进行初始ArduCopter安装](https://ardupilot.org/copter/docs/solo\_arducopter\_other\_install.html)
* [3DR Solo - 使用 Solex 初始 ArduCopter 安装](https://ardupilot.org/copter/docs/solo\_arducopter\_solex\_install.html)
* [3DR 独奏 - 智能电池校准](https://ardupilot.org/copter/docs/solo\_battery\_calibration.html)
