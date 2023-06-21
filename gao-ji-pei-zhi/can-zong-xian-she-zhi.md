# CAN总线设置

## CAN总线设置[¶](https://ardupilot.org/copter/docs/common-canbus-setup-advanced.html#can-bus-setup)

本文介绍如何设置CAN总线以及用户有哪些选项 完成适合其特定需求的设置。

提示

[DroneCAN设置页面在这里](https://ardupilot.org/copter/docs/common-uavcan-setup-advanced.html#common-uavcan-setup-advanced)。但是必须正确配置以下参数才能使用 DroneCAN 驱动程序。

注意

DroneCAN以前被称为UAVCAN。

### 概述[¶](https://ardupilot.org/copter/docs/common-canbus-setup-advanced.html#overview)

控制器局域网（CAN总线）是一种强大的车辆总线标准，设计自如。 允许微控制器和设备在 没有主机的应用程序。它是一个基于消息的协议，旨在 最初用于汽车内的多路复用电线以节省铜， 但也用于许多其他上下文。

所有节点都通过双线总线相互连接。电线是 120 Ω标称双绞线。

大多数运行ArduPilot的自动驾驶仪都有一个或两个CAN接口。 用于连接不同的设备。ArduPilot最多可以支持3个CAN接口。 接口的设置可以以提供冗余或 最大吞吐量或两者兼而有之。 这是通过三层方法实现的，除了物理之外 接口 存在一个表示特定协议的驱动程序层和一个 软件层（ArduPilot），通过这些驱动程序在CAN总线上进行通信。

每个物理接口都可以虚拟连接到最多三个驱动程序之一 表示要使用的协议。 例如，最常见的情况是 连接到 DroneCAN 驱动程序的接口。此类设置将为具有以下特征的设备提供冗余 多达三个CAN接口，具有一个CAN接口的设备具有全部功能。

### 配置设置[¶](https://ardupilot.org/copter/docs/common-canbus-setup-advanced.html#configuration-settings)

#### 启用CAN接口[¶](https://ardupilot.org/copter/docs/common-canbus-setup-advanced.html#enabling-can-interfaces)

每个物理端口都可以关闭或连接到相应的驱动程序 参数 ，其中 x 是 CAN 端口的编号。 此参数的值是将与此关联的驱动程序的 id 端口（接口）。`CAN_Px_DRIVER`

每个启用的总线/驱动程序将使用一个RAM内存块（不是闪存），具体取决于驱动程序的类型以及是否启用了CANFD。例如，DroneCAN将默认为其驱动程序分配12KB（如果为CANFD，则为24K），但如果由其硬件定义文件设置，则可能因板而异，具体取决于其默认值。该参数可用于更改池大小。所需的池大小取决于连接的 DroneCAN 外设所需的总线流量，有时可以减少 GPS 或指南针等外围设备，而 ESC 等外围设备需要更多的总线流量，因此池大小更大。`CAN_Dx_UC_POOL`

例如，最常见的设置将有一个驱动程序，并且将连接所有接口 到它。 此配置中的[CAN\_P1\_DRIVER](https://ardupilot.org/copter/docs/parameters.html#can-p1-driver)和[CAN\_P2\_DRIVER](https://ardupilot.org/copter/docs/parameters.html#can-p2-driver)参数应设置为 1（第一个 司机）。并且该驱动程序 （ [CAN\_D1\_PROTOCOL](https://ardupilot.org/copter/docs/parameters.html#can-d1-protocol)） 设置为 1 （DroneCAN）。

[![../\_images/can-driver-parameters.png](https://ardupilot.org/copter/\_images/can-driver-parameters.png)](https://ardupilot.org/copter/\_images/can-driver-parameters.png)

更改任何或必须重新启动自动驾驶仪后才能进行更改。`CAN_Px_DRIVERCAN_Dx_PROTOCOL`

#### CAN接口的配置[¶](https://ardupilot.org/copter/docs/common-canbus-setup-advanced.html#configuration-of-can-interfaces)

启用界面并重新启动后，可以为每个参数设置两个参数 启用的接口。

这些是：

* `CAN_Px_BITRATE`- 在此接口上设置所需的传输速率
* `CAN_Px_DEBUG`- 允许输出调试消息

通常默认使用的比特率为 1 Mbit。 调试级别也可以根据用户的偏好和需求进行设置。

[![../\_images/can-driver-parameters-bitrate.png](https://ardupilot.org/copter/\_images/can-driver-parameters-bitrate.png)](https://ardupilot.org/copter/\_images/can-driver-parameters-bitrate.png)

当任何接口与任何驱动程序关联时，该驱动程序将是 加载指定的协议。

#### CAN驱动程序的配置[¶](https://ardupilot.org/copter/docs/common-canbus-setup-advanced.html#configuration-of-can-driver)

驱动程序应设置为使用某些协议。目前支持DroneCAN设备， 编号为1，以及许多CAN电调。 参数 ，其中 x 是驱动程序的数量，应该填写 与此驱动程序的协议编号。`CAN_Dx_PROTOCOL`

[![../\_images/can-driver-parameters-protocol.png](https://ardupilot.org/copter/\_images/can-driver-parameters-protocol.png)](https://ardupilot.org/copter/\_images/can-driver-parameters-bitrate.png)

更改协议后，必须重新启动自动驾驶仪才能进行更改。

### 罐头电调[¶](https://ardupilot.org/copter/docs/common-canbus-setup-advanced.html#can-escs)

支持几种类型的基于CAN的电调：DroneCAN，KDECAN，ToshibaCAN，UAVCAN和PiccoloCAN。 对于这些 ESC，每种类型都使用多个参数进行配置。[在此处](https://ardupilot.org/copter/docs/common-escs-and-motors.html#common-escs-and-motors)查看 ESC 的个人描述页面。
