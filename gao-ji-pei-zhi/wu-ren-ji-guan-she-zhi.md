# 无人机罐设置

## 无人机罐设置[¶](https://ardupilot.org/copter/docs/common-uavcan-setup-advanced.html#dronecan-setup)

DroneCAN的创建是为了继续开发广泛使用的UAVCAN v0协议。该协议已被证明是强大且功能丰富的，并已广泛应用于商用无人机行业，并得到行业合作伙伴的广泛支持。拟议引入的 UAVCAN v1 协议涉及对 UAVCAN 的更改，这增加了复杂性，并且无法为现有部署提供平滑的迁移路径。经过UAVCAN联盟内部的长时间讨论，决定最好的解决方案是以DroneCAN的名义继续开发UAVCAN v0。

本文提供了在ArduPilot上设置DroneCAN协议的指导。

提示

应首先启用物理CAN端口及其选择为DroneCAN协议的驱动程序。请参考[CAN总线设置](https://ardupilot.org/copter/docs/common-canbus-setup-advanced.html#common-canbus-setup-advanced)

### 概述[¶](https://ardupilot.org/copter/docs/common-uavcan-setup-advanced.html#overview)

DroneCAN是一种轻量级协议，专为可靠通信而设计 通过CAN总线在航空航天和机器人应用中。 DroneCAN网络是一个分散的对等网络，其中每个对等点 （node）有一个唯一的数字标识符 - 节点ID，只有一个 需要为基本设置设置参数。

协议的详细说明可以在 [https://uavcan.org/](https://uavcan.org/)

### 支持的无人机CAN外设类型[¶](https://ardupilot.org/copter/docs/common-uavcan-setup-advanced.html#dronecan-peripheral-types-supported)

ArduPilot目前支持以下类型的DroneCAN外围设备：

| 全球定位系统      | 指南针      | 晴雨表  |
| ----------- | -------- | ---- |
| 测距          | ADSB 接收器 | 电源模块 |
| 发光二极管       | 蜂鸣器      | 空速   |
| 安全开关/指示灯    |          |      |
| 无人机CAN适配器节点 |          |      |

DroneCAN设备类型由以下方式选择：

* GPS，指南针，气压计，ADSB接收器，LED，蜂鸣器，安全开关/ LED和空速设备在DroneCAN协议中自动识别
* 测距仪： = 24`RNGFNDx_TYPE`
* 电源模块：[BATT\_MONITOR](https://ardupilot.org/copter/docs/parameters.html#batt-monitor)或 = 8`BATTx_MONITOR`

### 无人机CAN设置参数[¶](https://ardupilot.org/copter/docs/common-uavcan-setup-advanced.html#dronecan-setup-parameters)

显示第一个 DroneCAN 驱动程序，第二个驱动程序具有相同的参数

[![../\_images/uavcan-main-settings.png](https://ardupilot.org/copter/\_images/uavcan-main-settings.png)](https://ardupilot.org/copter/\_images/uavcan-main-settings.png)

* [如果](https://ardupilot.org/copter/docs/parameters.html#can-d1-protocol)为 DroneCAN（1） 设置CAN\_D1\_PROTOCOL则具有以下相关参数：
* [CAN\_D1\_UC\_POOL](https://ardupilot.org/copter/docs/parameters.html#can-d1-uc-pool)：如果可能，将为此大小的驱动程序分配内存池。如果CAN流量较轻，则通常可以减小默认大小，从而节省RAM用于其他功能和特性，例如GPS或指南针，而不是ESC。

### 无人机CAN适配器节点[¶](https://ardupilot.org/copter/docs/common-uavcan-setup-advanced.html#dronecan-adapter-node)

这些设备是具有I / O端口的通用DroneCAN节点，允许通过UART端口，I2C，SPI和/或GPIO将非DroneCAN ArduPilot外围设备连接到DroneCAN总线。请参阅 [DroneCAN 适配器节点](https://ardupilot.org/copter/docs/common-uavcan-adapter-node.html#common-uavcan-adapter-node)。

### 无人机罐电调和伺服配置设置[¶](https://ardupilot.org/copter/docs/common-uavcan-setup-advanced.html#dronecan-esc-and-servo-configuration-settings)

有关DroneCAN电调的信息，请参阅[DroneCAN电调](https://ardupilot.org/copter/docs/common-uavcan-escs.html#common-uavcan-escs)。

每个DroneCAN电调或伺服都将具有与自动驾驶仪的伺服/电机输出通道相对应的编程ID或通道地址。这些由电调上的开关或通过设置/配置程序设置，具体取决于电调。

有三个参数可以确定将哪些自动舵伺服/电机通道发送到CAN电调和/或舵机： 对于以下示例，显示了CAN驱动程序#1的值。

* [CAN\_D1\_UC\_NODE](https://ardupilot.org/copter/docs/parameters.html#can-d1-uc-node) - 这是将命令发送到ESC的自动驾驶仪的节点ID，以便可以区分CAN总线上的多个源
* [CAN\_D1\_UC\_ESC\_BM](https://ardupilot.org/copter/docs/parameters.html#can-d1-uc-esc-bm) - 位掩码，用于确定将哪些自动驾驶仪伺服/电机输出信号发送到 DroneCAN 电调。
* [CAN\_D1\_UC\_ESC\_SRV](https://ardupilot.org/copter/docs/parameters.html#can-d1-uc-srv-bm) - 位掩码，用于确定将哪些自动驾驶仪伺服/电机输出信号发送到DroneCAN舵机上的舵机

在位图掩码中，每个位位置表示一个 ESC 或伺服 ID 号 相应的自动驾驶仪伺服/电机通道命令将被定向到。例如，00001111（15 十进制）会将命令发送到 ESC 或 SERVO ID 0 到 3。

注意

使用 DroneCAN 电调/伺服时，您可以设置这些，但仍使用 [SERVO\_GPIO\_MASK](https://ardupilot.org/copter/docs/parameters.html#servo-gpio-mask) 参数在 GPIO 的自动驾驶仪上使用这些输出。自动驾驶仪输出将成为GPIOS，相应的输出将被发送到DroneCAN中。`SERVOx_FUNCTIONSERVOx_FUNCTION`

要减少带宽，应设置[CAN\_D1\_UC\_ESC\_BM](https://ardupilot.org/copter/docs/parameters.html#can-d1-uc-esc-bm)和[CAN\_D1\_UC\_ESC\_SRV\_BM](https://ardupilot.org/copter/docs/parameters.html#can-d1-uc-srv-bm)参数 仅启用需要发送CAN信号的电机和伺服通道。此外，[CAN\_D1\_UC\_ESC\_OF](https://ardupilot.org/copter/docs/parameters.html#can-d1-uc-esc-of)参数允许您通过将 ESC 位置偏移到总线上的第一个时隙来进一步最大化带宽，从而消除空时隙。例如，如果电调位于输出 5 到 8 上，则偏移量 4 将在前 4 个时隙中传输它们，否则这些时隙将为空并消耗带宽。

* 示例：对于通道 1、2、4 上的 CAN 伺服和通道 3 上的 ESC 电机的配置，请设置：
* 示例：[CAN\_D1\_UC\_ESC\_BM](https://ardupilot.org/copter/docs/parameters.html#can-d1-uc-esc-bm) = 0x0B
* 示例：[CAN\_D1\_UC\_ESC\_SRV](https://ardupilot.org/copter/docs/parameters.html#can-d1-uc-srv-bm) = 0x04

### 全球定位系统配置设置[¶](https://ardupilot.org/copter/docs/common-uavcan-setup-advanced.html#gps-configuration-settings)

如果有 DroneCAN GPS 设备，则必须在参数子组中启用它。 对于自动驾驶仪中相应的 GPS 接收器，该参数应设置为 9。`GPSTYPE`

[![../\_images/uavcan-gnss-settings.png](https://ardupilot.org/copter/\_images/uavcan-gnss-settings.png)](https://ardupilot.org/copter/\_images/uavcan-gnss-settings.png)

### 无人机罐灯配置[¶](https://ardupilot.org/copter/docs/common-uavcan-setup-advanced.html#dronecan-led-configuration)

通过在[NTF\_LED\_TYPES](https://ardupilot.org/copter/docs/parameters.html#ntf-led-types)位掩码中设置位 5 来启用 DroneCAN LED。[CAN\_D1\_UC\_NTF\_RT](https://ardupilot.org/copter/docs/parameters.html#can-d1-uc-ntf-rt)设置通知消息在 DroneCAN 中传输的速率。

### 无人机测距仪配置[¶](https://ardupilot.org/copter/docs/common-uavcan-setup-advanced.html#dronecan-rangefinder-configuration)

设置 = 24 以启用 DroneCAN 测距仪类型。通过 DroneCAN 接收的测距仪数据仅在收到的sensor\_id与参数匹配时才使用。对于AP\_Periph基于固件的适配器节点，此值为 0，因此必须设置为 0。其他无人机CAN测距仪可能有所不同。另请参阅 [DroneCAN 适配器节点](https://ardupilot.org/copter/docs/common-uavcan-adapter-node.html#common-uavcan-adapter-node)说明。`RNGFNDx_TYPERNGFNDx_ADDRRNGFNDx_ADDR`

### 无人机罐选项[¶](https://ardupilot.org/copter/docs/common-uavcan-setup-advanced.html#dronecan-options)

每个 DroneCAN 驱动程序的多个选项可以通过[CAN\_D1\_UC\_OPTION](https://ardupilot.org/copter/docs/parameters.html#can-d1-uc-option)和[CAN\_D2\_UC\_OPTION](https://ardupilot.org/copter/docs/parameters.html#can-d2-uc-option)位掩码参数进行选择。未设置默认值：

| CAN\_Dx\_UC\_OPTION位 | 设置时的功能                                                                                                                      |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| 0                    | ClearDNADatabase，[见下文](https://ardupilot.org/copter/docs/common-uavcan-setup-advanced.html#dronecan-node-conflicts)         |
| 1                    | 忽略DNA网络冲突，[见下文](https://ardupilot.org/copter/docs/common-uavcan-setup-advanced.html#dronecan-node-conflicts)                |
| 2                    | EnableCanfd，[CANFD 在下面](https://ardupilot.org/copter/docs/common-uavcan-setup-advanced.html#dronecan-node-flexibledatarate) |
| 3                    | 忽略 DNA 不健康，忽略断开连接的节点 ID                                                                                                     |
| 4                    | 发送伺服AsPWM，而不是将伺服位置作为-1发送到-1，而是作为PWM值发送。                                                                                     |
| 5                    | 发送GNSS，通过DroneCAN发送GPS定位和状态信息，由一些云台使用                                                                                       |

### 无人机CAN节点ID冲突[¶](https://ardupilot.org/copter/docs/common-uavcan-setup-advanced.html#dronecan-node-id-conflicts)

当设备被连接和识别时，它的节点 ID 和硬件 ID 被输入到一个数据库中，该数据库在电源周期之间存储。如果使用具有相同节点 ID 和不同硬件 ID 的多个设备（例如，交换具有相同节点 ID 的智能电池），则数据库中将出现冲突。这将需要使用 [CAN\_D1\_UC\_OPTION](https://ardupilot.org/copter/docs/parameters.html#can-d1-uc-option) 参数以允许在下次引导时重置数据库，或者忽略数据库中的冲突。

### CAN FD（灵活数据速率）[¶](https://ardupilot.org/copter/docs/common-uavcan-setup-advanced.html#can-fd-flexible-data-rate)

如果 DroneCAN 端口连接到 CAN FD 外设，则[CAN\_D1\_UC\_OPTION](https://ardupilot.org/copter/docs/parameters.html#can-d1-uc-option)位 2（+ 值 4）设置将启用此模式。

注意

CAN FD 需要比正常情况更大的内存池分配。默认值为 24KB，而不是正常的 12KB。

### 斯堪[¶](https://ardupilot.org/copter/docs/common-uavcan-setup-advanced.html#slcan)

注意

当武装以降低CPU负载时，通过COM端口的SLCAN访问被禁用。请通过MAVLink改用SLCAN。无论如何，这种方法通常是优选的。

ArduPilot和DroneCAN提供了一种直接与连接到自动驾驶仪的CAN总线上的DroneCAN设备通信的方法：SLCAN。启用SLCAN并与DroneCAN设备通信取决于自动驾驶仪的处理器。F7/H7 处理器使用一种方法，F4 使用另一种方法。

* [任务规划师 SLCAN](https://ardupilot.org/planner/docs/mission-planner-initial-setup.html#dronecan-uavcan-slcan)
* [基于 F4 的自动驾驶仪上的 SLCAN 访问](https://ardupilot.org/copter/docs/common-slcan-f4.html)
* [基于 F7/H7 的自动驾驶仪上的 SLCAN 访问](https://ardupilot.org/copter/docs/common-slcan-f7h7.html)
* [无人机罐](https://ardupilot.org/copter/docs/common-uavcan-gui.html)
