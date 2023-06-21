# BLHeli ESC

## BLHeli32 和 BLHeli\_S 电调[¶](https://ardupilot.org/copter/docs/common-blheli32-passthru.html#blheli32-and-blheli-s-escs)

BLHeli固件和配置应用程序的开发是为了允许配置电调并提供附加功能。具有此固件的电调允许配置定时、电机方向、LED、电机驱动频率等。在尝试使用 BLHeli 之前，请按照 [DShot 设置说明](https://ardupilot.org/copter/docs/common-dshot-escs.html#common-dshot-escs)进行操作。

本页包含以下功能的设置说明

* 直通支持允许BLHeli应用程序用于配置ESC，同时保持与自动驾驶仪的连接
* [可逆DShot](https://ardupilot.org/copter/docs/common-blheli32-passthru.html#blheli32-reversible-dshot)（又名3D模式）允许电机向任一方向旋转
* [双向 DShot](https://ardupilot.org/copter/docs/common-blheli32-passthru.html#bidir-dshot) 允许电调将 RPM 发送回自动驾驶仪，而无需额外的遥测连接
* ESC[遥测允许ESC](https://ardupilot.org/copter/docs/common-blheli32-passthru.html#blheli32-esc-telemetry)将RPM，电压和电流信息发送回自动驾驶仪，以便可以记录，实时查看，甚至允许移除[电池监视器](https://ardupilot.org/copter/docs/common-blheli32-passthru.html#esc-telemetry-based-battery-monitor)

“BLHeli”涵盖多个（有时是竞争的）项目，提供ESC固件和随附的配置软件

* BLHeli是最初的开源软件，不再维护，在现代ESC上不可用
* [BLHeli32](https://github.com/bitdump/BLHeli)是闭源的，基于32位ARM MCU。所有现代 BLHeli 电调都使用 BLHeli32
* [BLHeli\_S](https://github.com/bitdump/BLHeli)是开源的，是16位的。这不再主动维护，但最后发布的版本 16.7 在出厂时默认安装在“BLHeli\_S”ESC 上
* [BLHeli\_S JESC](https://jflight.net/) 是付费的、闭源软件和 16 位软件，允许它在低端硬件上运行
* [BLHeli\_S BlueJay](https://github.com/mathiasvr/bluejay) 是免费的开源软件和 16 位

### 直通支持[¶](https://ardupilot.org/copter/docs/common-blheli32-passthru.html#pass-through-support)

直通功能允许使用相应的BLHeliSuite32或BLHeliSuite应用程序（在用户的PC上运行）升级和配置BLHeli32和BLHeli\_S电调，同时电调保持与自动驾驶仪的连接。要使用此功能，请按照以下步骤操作

* 在您的PC上下载并安装[BLHeliSuite32](https://github.com/bitdump/BLHeli/releases)（用于BLHeli32 ESC），[BLHeliSuite](https://github.com/bitdump/BLHeli)（用于BLHeli\_S ESC）或JESC配置器（用于BLHeli\_S [JESC](https://github.com/jflight-public/jesc-configurator/releases)）
* 使用USB电缆将PC连接到自动驾驶仪，然后与地面站（例如任务规划器，QGC）连接。
* 将[SERVO\_BLH\_AUTO](https://ardupilot.org/copter/docs/parameters.html#servo-blh-auto)设置为 1 可在配置为多旋翼飞行器和四翼飞机的电机（例如 SERVOx\_FUNCTION = “电机 1”、“电机 2”等）或油门（例如[SERVOx\_FUNCTION](https://ardupilot.org/copter/docs/parameters.html#servo9-function)设置为 70（“油门”）、73（“油门左”）或 74（“油门右”））的所有输出上自动启用直通。对于大多数多旋翼飞行器、四翼飞机和漫游车来说，这将做正确的事情，但对于飞机，设置[SERVO\_BLH\_MASK](https://ardupilot.org/copter/docs/parameters.html#servo-blh-mask)以在适当的伺服输出上启用直通。
* 如果你的电脑使用遥测无线电连接到自动导航仪（而不是如上所述使用 USB 电缆），请将[SERVO\_BLH\_PORT](https://ardupilot.org/copter/docs/parameters.html#servo-blh-port)设置为连接到遥测无线电的自动导航仪端口。请注意，这并没有指定用于向自动驾驶仪进行[ESC遥测](https://ardupilot.org/copter/docs/common-blheli32-passthru.html#blheli32-esc-telemetry)反馈的端口！
* 如果使用安全开关，请确保按下（或通过设置 [BRD\_SAFETY\_DEFLT](https://ardupilot.org/copter/docs/parameters.html#brd-safety-deflt) = 0 将其禁用）。（在较旧的固件版本中）`BRD_SAFETYENABLE`
* 断开地面站的连接（但保持 USB 电缆连接）
*   启动ESC配置软件，并通过从界面菜单中选择“BLHeli32引导加载程序（Betaflight/Cleanflight）”连接到自动驾驶仪的COM端口。按“连接”和“读取设置”。您应该能够升级和配置所有连接的电调

    [![../\_images/blhelisuite32.jpg](https://ardupilot.org/copter/\_images/blhelisuite32.jpg)](https://ardupilot.org/copter/\_images/blhelisuite32.jpg)

注意

ArduPilot固件支持具有最新BLHeli32固件和BLHeliSuite32的直通协议，或仅支持BLHeli\_S固件和BLHeliSuite的直通协议。

警告

要使直通正常工作，必须将自动驾驶仪配置为使用 DShot 协议之一。如果您希望最终使用ESC支持的其他协议之一（例如PWM，OneShot125），您仍然可以使用直通配置ESC（例如更改电机方向，设置最小值/最大值等），但最终将自动驾驶仪重新配置为_不使用_DShot。一旦自动导航仪和电调重新启动，电调应自动检测电调是否不再使用 DShot。

### 可逆 DShot 电调[¶](https://ardupilot.org/copter/docs/common-blheli32-passthru.html#reversible-dshot-escs)

可逆DShot（又名3D模式）允许电机在任一方向上旋转，这对于[具有反向推力的](https://ardupilot.org/plane/docs/reverse-thrust-setup.html#reverse-thrust-setup)漫游车，船只和飞机非常重要。

目前，仅支持 BLHeli32 和具有 BLHeli\_S 功能的可逆 DShot 电调。为了使用一个，驱动它的输出必须在[SERVO\_BLH\_3DMASK](https://ardupilot.org/copter/docs/parameters.html#servo-blh-3dmask)位掩码参数中使用适当的位指定。这会将输出 1000-1500-2000 值映射到正确的数字值，以便 ESC 分别提供全反向-空闲-全正向范围操作。

如果启用了[DShot命令](https://ardupilot.org/copter/docs/common-dshot-escs.html#dshot-commands)，则ArduPilot将在[SERVO\_BLH\_3DMASK](https://ardupilot.org/copter/docs/parameters.html#servo-blh-3dmask)启动时自动将ESC配置为可逆模式（3D模式）。启用 DShot 命令将允许将其他 DShot 命令发送到由 DShot [设置说明](https://ardupilot.org/copter/docs/common-dshot-escs.html#common-dshot-escs)中讨论的 DShot 掩码参数配置为 [DShot](https://ardupilot.org/copter/docs/common-dshot-escs.html#dshot-commands) 的任何其他 ESC。

否则，您必须手动将电调的“电机方向”配置为“双向 3D”，如下所示。

> [![../\_images/blheli-reverse-dshot.png](https://ardupilot.org/copter/\_images/blheli-reversible-dshot.png)](https://ardupilot.org/copter/\_images/blheli-reversible-dshot.png)

注意

目前，ArduPilot仅支持对飞机和漫游车使用可逆电调，不支持直升机。

### 电调遥测[¶](https://ardupilot.org/copter/docs/common-blheli32-passthru.html#esc-telemetry)

如果 ESC 具有此功能，则允许监视和记录以前需要其他传感器（如电源模块和 RPM 传感器）的性能数据。每个ESC提供的详细数据允许实时决策和单独的ESC或电机性能调整和故障分析。请注意，给定的ESC可能会也可能不会通过遥测传输特定传感器的数据。4合1电调通常提供电压和电流传感器，但不通过遥测传输数据，而是直接连接到自动驾驶仪。有关详细信息，请查看 ESC 数据手册和连接信息。

注意

ArduPilot 目前不支持在非 DShot 协议中通过信号线上的限制空闲消息轮询 ESC 以获取遥测数据。

### 连接电调遥测线[¶](https://ardupilot.org/copter/docs/common-blheli32-passthru.html#connecting-the-escs-telemetry-wire)

[![../\_images/dshot-pixhawk.jpg](https://ardupilot.org/copter/\_images/dshot-pixhawk.jpg)](https://ardupilot.org/copter/\_images/dshot-pixhawk.jpg)

将所有ESC遥测线连接到自动驾驶仪上单个串行端口的RX引脚（上图以Serial5为例）。用于电调遥测的引脚或电线在大多数 BLHeli32 电调上预先焊接。如果电线没有预先焊接，则需要自己焊接。CubePilot串行端口引脚输出可以[在这里](https://ardupilot.org/copter/docs/common-thecube-overview.html#common-thecube-overview)找到。

设置以下参数以启用 BLHeli32 遥测反馈到自动驾驶仪的串行端口：

* [SERIALx\_PROTOCOL](https://ardupilot.org/copter/docs/parameters.html#serial5-protocol) 16（= ESC 遥测），其中“x”是连接到 ESC 遥测线的自动导航仪串行端口号。自动驾驶仪的串行端口编号和UART物理端口之间的映射应记录在此处链接[的](https://ardupilot.org/copter/docs/common-autopilots.html#common-autopilots)描述页面中。
* [SERVO\_BLH\_TRATE](https://ardupilot.org/copter/docs/parameters.html#servo-blh-trate)默认为 10，通常不需要更改。这将启用来自 ESC 的 10Hz 更新速率的遥测。如果使用[谐波陷波功能](https://ardupilot.org/copter/docs/common-imu-notch-filtering.html#common-imu-notch-filtering)，则可以将其提高到100。
* [SERVO\_BLH\_POLES](https://ardupilot.org/copter/docs/parameters.html#servo-blh-poles)默认为 14，适用于大多数无刷电机，通常不需要更改。如果您使用极数不是 14 的电机来计算电调的电场 RPM 的真实电机轴 RPM，请根据需要进行调整。

### ESC 遥测日志记录和报告[¶](https://ardupilot.org/copter/docs/common-blheli32-passthru.html#esc-telemetry-logging-and-reporting)

自动驾驶仪一次从一个 ESC 请求状态信息，并在它们之间循环。此信息记录到板载日志的ESCn消息中，并且可以在任何[与ArduPilot兼容的日志查看器](https://ardupilot.org/copter/docs/common-logs.html#common-logs)中查看。

* .RPM
* 电压
* 当前
* 温度
* 总电流

RCOU 消息也会写入板载日志，这些日志包含发送到 ESC 的请求输出电平，表示为 1000（表示停止）到 2000（表示完全输出）的数字。

这些数据也可以使用地面站实时查看。如果使用任务规划器，请转到飞行数据屏幕的状态选项卡并查找esc1\_rpm。

[![../\_images/dshot-realtime-esc-telem-in-mp.jpg](https://ardupilot.org/copter/\_images/dshot-realtime-esc-telem-in-mp.jpg)](https://ardupilot.org/copter/\_images/dshot-realtime-esc-telem-in-mp.jpg)

注意

将 BLHeli32 遥测数据发送到 GCS 需要遥测连接使用 MAVLink2。ArduPilot默认在USB端口上使用MAVLink2，但如果使用另一个端口，则可能需要将SERIALx\_PROTOCOL参数设置为2（其中“x”是用于遥测连接的串行端口号）。

此外，如果您的自动驾驶仪有遥测仪，则可以在集成的[板载 OSD](https://ardupilot.org/copter/docs/common-osd-overview.html#common-osd-overview) 上显示一些遥测值。

#### 用作电池监视器[¶](https://ardupilot.org/copter/docs/common-blheli32-passthru.html#use-as-battery-monitor)

通过将电池监视器实例设置为 BLHeli32 ESC 类型（例如 [BATT2\_MONITOR](https://ardupilot.org/copter/docs/parameters.html#batt2-monitor) = 9），所有连接的 BLHeli32 ESC 以及连接到配置的自动导航仪串行端口的遥测接线，都将聚合为单个源。报告的电压将被平均，总计的电流和累积的消耗电流。

#### 双向 DShot[¶](https://ardupilot.org/copter/docs/common-blheli32-passthru.html#bi-directional-dshot)

较新版本的 BLHeli32（32.7 及更高版本）和 BLHeli\_S（16.73 及更高版本）支持通过 DShot 信号线返回电机 RPM 值。支持双向DShot需要独占使用一个或多个DMA通道，因此并非所有版本的ArduPilot都支持它。下面列出了本机支持双向 DShot 的版本。对于其他自动驾驶仪，请加载以“-bdshot”结尾的ArduPilot固件版本。

* 野兽F7， 野兽F7v2， 野兽H7， 野兽H7v2
* 飞宇F745， 飞宇F745纳米
* KakuteF4Mini， KakuteF7Mini， KakuteH7Mini

只能使用最低的 4 个支持 DShot 的伺服输出。对于带有IOMCU（例如Pixhawk，CubeOrange）的自动驾驶仪，这意味着可以使用AUX1到AUX4。对于Pixracer和其他没有单独IOMCU协处理器的自动驾驶仪，这意味着可以使用输出1到4。

### 设置[¶](https://ardupilot.org/copter/docs/common-blheli32-passthru.html#setup)

首先，请确保您的 ESC 上安装了适当版本的 BLHeli32 或BLHeli\_S。大多数 ESC 未预装这些版本。BLHeli32 的官方 7.32 版本支持双向 DShot。BLHeli\_S的正式版本不支持双向DShot，您需要从[BLHeli\_S JESC](https://jflight.net/index.php?route=common/home\&language=en-gb)购买版本或使用[BLHeli\_S BlueJay](https://github.com/mathiasvr/bluejay)。如果您尝试使用错误的固件版本启用双向 DShot，则可能会出现不可预测的电机操作。

[![../\_images/blheli-version-check.png](https://ardupilot.org/copter/\_images/blheli-version-check.png)](https://ardupilot.org/copter/\_images/blheli-version-check.png)

设置以下参数以启用 BLHeli32 并BLHeli\_S双向 DShot：

* [SERVO\_BLH\_BDMASK](https://ardupilot.org/copter/docs/parameters.html#servo-blh-bdmask)：用于启用 BLHeli32 或BLHeli\_S双向 DShot 支持的位图。在没有IOMCU的自动驾驶仪上，这通常设置为15，以指示四个活动通道。在带有 IOMCU 的自动驾驶仪上，可以将其设置为 3840 以指示四个活动的 AUX 通道（双向 DShot 仅适用于 AUX 输出）。
* [SERVO\_BLH\_POLES](https://ardupilot.org/copter/docs/parameters.html#servo-blh-poles)默认为 14，适用于大多数无刷电机，通常不需要更改。如果您使用极数不是 14 的电机来计算 ESC 的电场 RPM（小型电机可能有 12 个极），请根据需要进行调整。
