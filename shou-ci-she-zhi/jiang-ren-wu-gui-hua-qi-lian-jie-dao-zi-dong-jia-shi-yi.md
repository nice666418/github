# 将任务规划器连接到自动驾驶仪

本文介绍如何将_任务规划器_连接到自动驾驶仪 为了接收遥测数据并控制车辆。

注意

对于现有的ArduPilot固件安装或[没有现有ArduPilot固件的](https://ardupilot.org/copter/docs/common-loading-firmware-onto-chibios-only-boards.html#common-loading-firmware-onto-chibios-only-boards)板，为了[加载固件](https://ardupilot.org/copter/docs/common-loading-firmware-onto-pixhawk.html#common-loading-firmware-onto-pixhawk)，有单独的连接说明。

### 设置连接[¶](https://ardupilot.org/copter/docs/common-connect-mission-planner-autopilot.html#setting-up-the-connection)

要建立连接，您必须首先选择通信 要使用的方法/通道，然后设置物理硬件 和视窗设备驱动程序。您可以使用以下方法连接PC和自动驾驶仪 USB 电缆、[遥测无线电](https://ardupilot.org/copter/docs/common-telemetry-landingpage.html#common-telemetry-landingpage)、[蓝牙](https://ardupilot.org/copter/docs/common-mission-planner-bluetooth-connectivity.html#common-mission-planner-bluetooth-connectivity-detailed-connecting-with-mission-planner)、 IP 连接等

注意

连接硬件的驱动程序必须存在于 Windows 上 因为这会使连接的COM端口和默认数据速率可用 到_任务规划师_。

[![../\_images/pixhawk\_usb\_connection.jpg](https://ardupilot.org/copter/\_images/pixhawk\_usb\_connection.jpg)](https://ardupilot.org/copter/\_images/pixhawk\_usb\_connection.jpg)

像素鹰 USB 连接[¶](https://ardupilot.org/copter/docs/common-connect-mission-planner-autopilot.html#id2)

[![../\_images/new-radio-laptop.jpg](https://ardupilot.org/copter/\_images/new-radio-laptop.jpg)](https://ardupilot.org/copter/\_images/new-radio-laptop.jpg)

使用 SiK 无线电进行连接[¶](https://ardupilot.org/copter/docs/common-connect-mission-planner-autopilot.html#id3)

在_任务规划器_上，连接和数据速率使用 屏幕右上角的下拉框。

[![../\_images/MisionPlanner\_ConnectButton.png](https://ardupilot.org/copter/\_images/MisionPlanner\_ConnectButton.png)](https://ardupilot.org/copter/\_images/MisionPlanner\_ConnectButton.png)

连接USB或遥测无线电后，Windows将 自动为您的自动驾驶仪分配一个COM端口号，这将 显示在下拉菜单中（实际数字无关紧要）。这 还设置了适当的连接数据速率（通常是 USB 连接数据速率为 115200，无线电连接速率为 57600）。

选择所需的端口和数据速率，然后按**连接**按钮连接到自动驾驶仪。连接后，**任务规划器**将从自动驾驶仪下载参数，按钮将更改 **断开连接，**如下所示：

[![../\_images/MisionPlanner\_DisconnectButton.png](https://ardupilot.org/copter/\_images/MisionPlanner\_DisconnectButton.png)](https://ardupilot.org/copter/\_images/MisionPlanner\_DisconnectButton.png)

提示

“选择端口”下拉列表还包含 TCP 或 UDP 端口选项 可用于通过网络连接自动驾驶仪。

“统计...”端口选择框下方的热链接（如果单击）将提供有关连接的信息，例如[签名安全性](https://ardupilot.org/copter/docs/common-MAVLink2-signing.html#common-mavlink2-signing)是否处于活动状态、链接统计信息等。有时此窗口会在当前屏幕下方弹出，必须放在前面才能看到。

[![../\_images/MP-stats.png](https://ardupilot.org/copter/\_images/MP-stats.png)](https://ardupilot.org/copter/\_images/MP-stats.png)

#### 连接多辆车[¶](https://ardupilot.org/copter/docs/common-connect-mission-planner-autopilot.html#connecting-to-multiple-vehicles)

可以通过右键单击“连接”按钮并从下拉列表中选择**“连接选项**”来建立其他**连接**。

[![../\_images/MP-connect-rightclick-menu.png](https://ardupilot.org/copter/\_images/MP-connect-rightclick-menu.png)](https://ardupilot.org/copter/\_images/MP-connect-rightclick-menu.png)

可以使用“连接列表”下拉选项加载具有预先编写的连接**列表**的文件。这是文件的示例格式：

```
tcp://127.0.0.1:5670
udp://127.0.0.1:14550
udpcl://192.168.1.255:14550
serial:com4:115200
```

### 故障 排除[¶](https://ardupilot.org/copter/docs/common-connect-mission-planner-autopilot.html#troubleshooting)

如果任务规划器无法连接：

* 检查所选方法是否使用了正确的波特率 （USB 上为 115200，无线电/遥测上为 57600）
* 如果通过 USB 连接，请确保在通电后几秒钟后再尝试连接。如果您尝试在引导加载程序初始化期间进行连接，Windows 可能会获得错误的 USB 信息。在此之后的连接尝试可能需要拔下并重新插入USB连接，然后等待引导加载程序输入主代码（几秒钟），然后尝试连接。有时，如果在引导加载程序初始化期间尝试连接，则必须重新启动 MP。
* 如果在 Windows 上使用 COM 端口，请检查连接的 COM 端口 存在于 Windows 设备管理器的串行端口列表中。
* 如果您的自动驾驶仪具有 F7 或 H7 处理器并具有 CAN 端口，请参阅以下复合[连接故障排除](https://ardupilot.org/copter/docs/common-connect-mission-planner-autopilot.html#troubleshooting-composite-connections)部分
* 如果使用 USB 端口，请尝试使用其他物理 USB 端口
* 如果使用 UDP 或 TCP 连接，请检查防火墙是否未阻止 IP 流量

您还应该确保自动导航仪控制器板具有 安装了相应的 ArduPilot 固件并已正确启动（在 Pixhawk 有有用的 [LED](https://ardupilot.org/copter/docs/common-leds-pixhawk.html#common-leds-pixhawk) 和[声音](https://ardupilot.org/copter/docs/common-sounds-pixhawkpx4.html#common-sounds-pixhawkpx4)，可以告诉您自动驾驶仪的状态）。

如果使用远程链接（不是 USB）并且任务规划器连接，但不下载参数，或者您无法获取命令（例如操作的模式更改），则自动驾驶仪可能已打开签名。请参阅 [MAVLink2 签名](https://ardupilot.org/copter/docs/common-MAVLink2-signing.html#common-mavlink2-signing)。

### 复合连接疑难解答[¶](https://ardupilot.org/copter/docs/common-connect-mission-planner-autopilot.html#troubleshooting-composite-connections)

具有 F7 或 H7 处理器并具有 CAN 接口的自动驾驶仪使用提供两个 USB 接口的固件：一个用于正常的 MAVLink 连接，另一个用于与 CAN 接口的 SLCAN 串行连接，用于配置和固件更新。这称为复合 USB 设备。

默认情况下，MAVLink USB 接口为 SERIAL0，SLCAN USB 接口是主板提供的最高 SERIALx 端口。当前随Mission Planner一起安装的Windows驱动程序可以选择使用其中任何一个，并且由于默认情况下两者都在MAVLINK协议的ArduPilot固件中设置，因此无论它选择哪个作为COM端口，它都可以正常工作。

但是，在某些情况下，用户会发现它不会连接到任务规划器下拉框中明显的COM端口。当用户意外地将 Windows 驱动程序用作 MAVLink COM 端口的任何 SERIALx 端口的协议更改为 MAVLink 以外的其他端口时，会发生这种情况。如果用户从与协议已更改的不同自动驾驶仪一起使用的车辆配置中获取现有参数文件，则很容易发生这种情况。例如，用户有一架没有F7 / H7 CAN功能的自动驾驶仪的飞机，并将其升级到该飞机，然后在使用新的自动驾驶仪设置飞机时加载他现有的参数文件。一旦加载参数文件并重新启动自动驾驶仪，通信就会丢失，无法重新建立。

已经发生的情况是，Windows使用的SERIALx端口的协议已更改。几乎总是，这是编号最高的SERIALx端口，因为在不支持CAN的自动驾驶仪上通常设置为-1，并且Windows COM端口驱动程序已选择此接口作为COM端口而不是SERIAL0。

恢复过程如下：

* 转到Windows设备管理器，然后在端口列表中找到自动驾驶仪正在使用的COM端口。它将具有您最初用于连接到任务规划器的 COM 端口 #。右键单击，它将显示“更新驱动程序软件”作为选项之一。单击它。

![../\_images/devicemanager.png](https://ardupilot.org/copter/\_images/devicemanager.png)

* 点击“浏览我的电脑...”选项，然后单击“从列表中选择...”选项，您将看到此屏幕：

![../\_images/composite-driver.png](https://ardupilot.org/copter/\_images/composite-driver.png)

* 向下滚动顶部列表，直到出现“复合USB”选项并单击它。
* 现在将您的自动驾驶仪重新连接到PC，将显示两个COM端口。一个将连接（其余一个使用 MAVLink 协议），另一个不会。如果未连接到其中一个，请尝试另一个。但不要断开自动驾驶仪与PC的连接，否则复合驱动程序将卸载，您将不得不重新开始。
* 现在您已连接到任务规划器，请将串行端口协议的协议更改回 2 （MAVLink2）。您现在可以断开并重新连接自动驾驶仪，它将只显示一个COM端口，从现在开始您应该能够连接。从现在开始不要更改此协议，除非尝试使用 SLCAN 接口。这可能有点陌生，因为正在使用的任务规划器SERIALx端口不再是正常的SERIAL0，而是最高的端口，但这不会影响自动驾驶仪配置和操作中的任何内容。

### 相关主题[¶](https://ardupilot.org/copter/docs/common-connect-mission-planner-autopilot.html#related-topics)

[任务规划器蓝牙连接](https://ardupilot.org/copter/docs/common-mission-planner-bluetooth-connectivity.html#common-mission-planner-bluetooth-connectivity-detailed-connecting-with-mission-planner)
