# 直升机简介

Copter 是一种先进的开源自动驾驶系统，适用于多旋翼飞行器、直升机和其他旋翼飞行器。它提供了从全手动到全自动的各种飞行模式。

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

作为更广泛的ArduPilot软件平台的一部分，它与各种地面控制站程序无缝协作，这些程序用于设置车辆，实时监控车辆的飞行并执行强大的任务规划活动。它还受益于ArduPilot生态系统的其他部分，包括模拟器，日志分析工具和用于车辆控制的更高级别的API。

ArduPilot已经是众多商用自动驾驶系统的首选平台，但您也可以使用它来增强自己的DIY多旋翼的能力。

## 主要功能

主要功能包括：

* 高精度[杂技模式](https://ardupilot.org/copter/docs/acro-mode.html#acro-mode)：执行激进的动作，包括翻转！
* [自动调平](https://ardupilot.org/copter/docs/stabilize-mode.html#stabilize-mode)和[高度保持](https://ardupilot.org/copter/docs/altholdmode.html#altholdmode)模式：轻松水平和直线飞行或添加[简单](https://ardupilot.org/copter/docs/simpleandsuper-simple-modes.html#simpleandsuper-simple-modes)模式，无需飞行员跟踪车辆的航向。只需按照您希望车辆行驶的方式推动操纵杆，自动驾驶仪就会弄清楚这对直升机所处的任何方向意味着什么。
* [徘徊](https://ardupilot.org/copter/docs/loiter-mode.html#loiter-mode)和保持模式：车辆将使用其GPS，加速度计和气压计[保持](https://ardupilot.org/copter/docs/poshold-mode.html#poshold-mode)其位置。
* [返回发射：](https://ardupilot.org/copter/docs/rtl-mode.html#rtl-mode)拨动开关，让直升机飞回发射位置并自动降落。
* 飞行[中的临时命令](https://ardupilot.org/copter/docs/ac2\_guidedmode.html#ac2-guidedmode)：安装双向遥测无线电后，只需单击地图，飞行器就会飞到所需位置。
* [自主任务](https://ardupilot.org/copter/docs/auto-mode.html#auto-mode)：使用地面站定义具有多达数百个 GPS 航点的复杂任务。然后将飞行器切换到“AUTO”并观察它起飞，执行任务，然后返回家园，着陆并解除武装，而无需任何人为干预。
* [故障保护](https://ardupilot.org/copter/docs/failsafe-landing-page.html#failsafe-landing-page)：该软件监控系统状态，并在与飞行员失去联系、电池电量不足或车辆偏离定义的地理围栏之外时触发自动返航。
* **灵活且可定制**：Copter可以按照您想要的方式飞行[各种形状和大小的车辆](https://ardupilot.org/copter/docs/common-all-vehicle-types.html#common-all-vehicle-types)，因为用户可以访问数百个控制其行为的参数。您不需要触摸其中的大多数，但如果您需要它们，它们就在那里。
* **没有供应商锁定**：ArduPilot是完全开源的，背后有多元化的开发人员社区。您可以完全控制车辆上的软件及其性能。

## 开始

您需要的第一件事是带有[ArduPilot兼容自动驾驶仪](https://ardupilot.org/copter/docs/common-autopilots.html#common-autopilots)的多旋翼飞行器。 以下是准备[飞行的车辆](https://ardupilot.org/copter/docs/common-rtf.html#common-rtf)列表，可以快速开始使用，或者您可以选择自己构建。

如果您在准备飞行[的飞行器](https://ardupilot.org/copter/docs/common-rtf.html#common-rtf)上使用直升机，那么它应该预先配置和调整，为您的首次飞行做好准备。 我们建议您在飞行前阅读制造商的说明，尤其是有关安全的部分。 然后[，在安装地面站后，](https://ardupilot.org/copter/docs/common-install-gcs.html#common-install-gcs)您可能会跳到[首次飞行](https://ardupilot.org/copter/docs/flying-arducopter.html#flying-arducopter)说明。

{% hint style="info" %}
无论是使用RTF还是DIY车辆，自动驾驶汽车都是 有潜在的危险！始终遵循[最佳安全实践](https://ardupilot.org/copter/docs/safety-multicopter.html#safety-multicopter)并密切关注所有安全 警告。
{% endhint %}

如果您打算构建自己的多旋翼飞行器，以下页面将帮助您入门。 请首先阅读本节，以了解多旋翼飞行器可以做什么，以及如何选择框架、自动驾驶仪板、 和其他基本组件。 然后继续首次[设置](https://ardupilot.org/copter/docs/initial-setup.html#initial-setup)以了解如何组装直升机，然后进行[首次飞行](https://ardupilot.org/copter/docs/flying-arducopter.html#flying-arducopter)以学习如何配置和调整它。

### 了解有关直升机的更多信息[¶](https://ardupilot.org/copter/docs/introduction.html#learn-more-about-copter)

要了解有关直升机的更多信息以及您的主要配置决策， 请参阅以下主题：

* [多旋翼飞行器的工作原理](https://ardupilot.org/copter/docs/what-is-a-multicopter-and-how-does-it-work.html)
* [选择多旋翼框架](https://ardupilot.org/copter/docs/choosing-a-frame.html)
* [选择自动驾驶仪](https://ardupilot.org/copter/docs/common-choosing-a-flight-controller.html)
* [选择地面站](https://ardupilot.org/copter/docs/common-choosing-a-ground-station.html)
* [构建自己的框架](https://ardupilot.org/copter/docs/what-you-need.html)
* [多旋翼安全](https://ardupilot.org/copter/docs/safety-multicopter.html)
* [准备飞行车辆](https://ardupilot.org/copter/docs/common-rtf.html)
* [支持的车辆类型](https://ardupilot.org/copter/docs/common-all-vehicle-types.html)
* [用例概述](https://ardupilot.org/copter/docs/copter-use-case-overview.html)
