# 引导加载程序更新

## 更新引导加载程序[¶](https://ardupilot.org/copter/docs/common-bootloader-update.html#updating-the-bootloader)

引导加载程序是一小段代码，在自动驾驶仪打开电源时运行（通常只有几秒钟）。引导加载程序的主要职责之一是允许轻松升级主固件（即ArduPilot）。

几乎所有自动驾驶仪都预装了引导加载程序，大多数用户永远不需要升级它，但升级到最新的ArduPilot特定引导加载程序有一些优势：

* 错误修复，如 Copter-4.0.4、Plane-4.0.6 中包含的“参数重置”问题修复
* COM 端口名称可能更容易识别。例如，它可能包括“ArduPilot”

警告

更新引导加载程序可能会使开发板“变砖”（即使其无响应且无法上传新固件）。注意不要在更新过程中关闭自动驾驶仪的电源

### 在哪里可以下载最新的引导加载程序？[¶](https://ardupilot.org/copter/docs/common-bootloader-update.html#where-can-i-download-the-latest-bootloader)

ArduPilot特定的引导加载程序包含在ArduPilot固件中，但默认情况下处于休眠状态。必须向主 ArduPilot 固件发送特殊命令才能安装新的引导加载程序。

> [![../\_images/bootloader-file-description.png](https://ardupilot.org/copter/\_images/bootloader-file-description.png)](https://ardupilot.org/copter/\_images/bootloader-file-description.png)

### 使用任务规划器升级[¶](https://ardupilot.org/copter/docs/common-bootloader-update.html#upgrading-using-mission-planner)

* 将最新版本的 ArduPilot 安装到自动驾驶仪（使用现有的 ArduPilot 固件，[没有现有的 ArduPilot 固件](https://ardupilot.org/copter/docs/common-loading-firmware-onto-chibios-only-boards.html#common-loading-firmware-onto-chibios-only-boards)）)
*   连接并检查自动驾驶仪是否至少有 20k 的可用内存。打开数据屏幕的快速选项卡，双击任何条目并选择“freemem”。

    [![../\_images/bootloader-update-MP-memory-check.png](https://ardupilot.org/copter/\_images/bootloader-update-MP-memory-check.png)](https://ardupilot.org/copter/\_images/bootloader-update-MP-memory-check.png)
*   打开设置>>安装固件页面，然后按“引导加载程序更新”按钮

    [![../\_images/bootloader-update-MP.png](https://ardupilot.org/copter/\_images/bootloader-update-MP.png)](https://ardupilot.org/copter/\_images/bootloader-update-MP.png)
* 重新启动自动驾驶仪

### 使用 QGC 升级[¶](https://ardupilot.org/copter/docs/common-bootloader-update.html#upgrading-using-qgc)

该过程类似于使用Mission Planner（见上文），除了“Flash ChibiOS引导加载程序”按钮位于固件页面的配置（齿轮图标）上。

> [![../\_images/bootloader-update-QGC.png](https://ardupilot.org/copter/\_images/bootloader-update-QGC.png)](https://ardupilot.org/copter/\_images/bootloader-update-QGC.png)

### 使用 MAVProxy 升级[¶](https://ardupilot.org/copter/docs/common-bootloader-update.html#upgrading-with-mavproxy)

* 在 MAVProxy 终端中，键入“flashbootloader”

### 额外信息[¶](https://ardupilot.org/copter/docs/common-bootloader-update.html#extra-information)

* 有关引导加载程序的开发人员特定信息可[在此处](https://ardupilot.org/dev/docs/bootloader.html)找到
* 引导加载程序的源代码可以在[工具/AP\_Bootloader](https://github.com/ArduPilot/ardupilot/tree/master/Tools/AP\_Bootloader)中找到
* 可以在 [firmware.ardupilot.org/Tools/Bootloaders](https://firmware.ardupilot.org/Tools/Bootloaders/) 上找到预编译的二进制文件

\
