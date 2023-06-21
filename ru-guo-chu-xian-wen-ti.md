# 如果出现问题

## 当问题出现时[¶](https://ardupilot.org/copter/docs/common-when-problems-arise.html#when-problems-arise)

ArduPilot，非常有能力和灵活。但是，随着高性能和灵活性的提高，带来了许多配置、参数和复杂性。

本 WIKI 文档试图通过提供有关配置、参数和操作模式的尽可能多的准确信息来减少配置和操作基于 ArduPilot 的车辆的工作量，并且随着新版本的发布或需要进一步解释的领域出现而不断更新。欢迎并请求你们协助这一努力。请参阅[维基编辑指南](https://ardupilot.org/copter/docs/common-wiki\_editing\_guide.html#common-wiki-editing-guide)

### 遇到问题该怎么办[¶](https://ardupilot.org/copter/docs/common-when-problems-arise.html#what-to-do-if-you-have-an-issue)

1. 确保您已遵循车辆的“首次设置”和“首次飞行/驾驶”部分，并仔细阅读提供的文档。如果处理高级配置或硬件选项，请仔细阅读相应的文档。
2. 如果这不能帮助您解决问题，请在适合您的车辆或地面站的讨论[论坛](https://discuss.ardupilot.org/)部分寻求帮助。不要在 GitHub 软件存储库中输入问题，除非已在代码或文档中确认为实际问题。将在相应的讨论论坛中提供支持。
3. 拥有[数据闪存日志](https://ardupilot.org/copter/docs/common-diagnosing-problems-using-logs.html#common-diagnosing-problems-using-logs)将帮助您或帮助您的人诊断问题。

注意

监视狗重置（“WDG：”）应在此[页面上](https://github.com/ArduPilot/ardupilot/issues/15915)报告，内部错误（“内部错误：”）应[在此处](https://github.com/ArduPilot/ardupilot/issues/15916)报告

### 直升机常见问题[¶](https://ardupilot.org/copter/docs/common-when-problems-arise.html#copter-common-problems)

* 新直升机起飞后立即翻转。这通常是由 由于电机顺序不正确或方向错误 或使用不正确的螺旋桨（顺时针与逆时针）。 检查自动驾驶仪的 rc 连接。
* 直升机在横滚轴或俯仰轴上摆动。这通常意味着速率P 值不正确。有关以下方面的一些提示，请参阅[“调整](https://ardupilot.org/copter/docs/common-tuning.html#common-tuning)”部分 如何调整这些增益。
* 直升机在快速下降时摇晃。这是由直升机引起的 掉进自己的道具清洗中，几乎不可能调音 尽管提高速率滚动/音高 P 值可能会有所帮助。
* 直升机起飞时向右或向左偏航 15 度。有些电机可能不会 笔直或[电调尚未校准](https://ardupilot.org/copter/docs/esc-calibration.html#esc-calibration)。
* 即使在无风的情况下，直升机也总是倾向于朝一个方向飞行 环境。尝试“保存修剪”[或“自动修剪”](https://ardupilot.org/copter/docs/autotrim.html#autotrim)来调平 直升机。
* 即使飞行员拉下油门，直升机也会迅速爬升。这可能是由高振动引起的。有关改善隔振的方法，请参阅 [https://ardupilot.org/copter/docs/common-vibration-damping.html](https://ardupilot.org/copter/docs/common-vibration-damping.html)。
* 偶尔在滚动或俯仰时抽搐。通常由某种原因引起 接收器上的干扰（例如 FPV 设备也放置了 靠近接收器）或通过电调问题，这些问题可以通过[校准来解决](https://ardupilot.org/copter/docs/esc-calibration.html#esc-calibration)。
* 飞行过程中突然翻转。这几乎总是由电机或电调的[机械故障](https://ardupilot.org/copter/docs/common-diagnosing-problems-using-logs.html#common-diagnosing-problems-using-logs-mechanical-failures)引起的。

### 可用内存问题[¶](https://ardupilot.org/copter/docs/common-when-problems-arise.html#free-ram-issues)

在初始化期间，某些功能/子系统可能无法分配足够的 RAM。有时会宣布这一点，例如在内存不足的情况下启动 LUA 脚本：“脚本需要更大的最小堆栈大小”，或者对于地形：“地形：分配失败”等。此外，可用内存不足可能导致指南针校准失败或 MAVftp 无法初始化。有关详细信息[，请参阅 RAM 限制](https://ardupilot.org/copter/docs/common-limited-firmware.html#ram-limitations)。

### H7 自动驾驶仪无法初始化[¶](https://ardupilot.org/copter/docs/common-when-problems-arise.html#h7-autopilot-will-not-initialize)

在极少数情况下，使用 H7 系列处理器的自动驾驶仪可能会进入不再完成初始化的状态。症状是：从不退出引导加载程序（电源应用永不停止后立即快速闪烁 LED）或自动驾驶仪在初始化期间冻结，并且无法连接到它。

据信，这可能是内存损坏问题，可能是由中断闪存写入（如更改参数时）引起的。不幸的是，由于处理器的架构，固件中无法自动更正此问题。如果自动驾驶仪看起来“砖砌”，请尝试此操作以将自动驾驶仪完全重置为完全未编程的状态。这应该允许安装固件并解决损坏问题。

* 首先，通过加载[包含](https://firmware.ardupilot.org/Tools/STM32-tools/2MByte\_allzero.bin)所有零数据的文件，用零对整个2MB闪存空间进行编程。使用[此处](https://ardupilot.org/copter/docs/common-loading-firmware-onto-chibios-only-boards.html#common-loading-firmware-onto-chibios-only-boards)的说明，但使用上面的文件。
* 接下来，从[这里](https://firmware.ardupilot.org/Tools/Bootloaders/)下载适用于您的AutoPilot的ArduPilot引导加载程序。然后使用该引导加载程序文件重复上述步骤。这会将引导加载程序置于自动驾驶仪上。重新打开自动驾驶仪的电源。此时，它将通电并保留在引导加载程序中，直到安装操作固件。
* 最后，使用Mission Planner的“设置/安装固件”选项卡或[Uploader](https://raw.githubusercontent.com/ArduPilot/ardupilot/master/Tools/scripts/uploader.py) python脚本来加载所需的ArduPilot固件版本。

这应该可以解决由内存损坏引起的问题，并且将恢复正常操作。
