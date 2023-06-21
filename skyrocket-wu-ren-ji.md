# SkyRocket无人机

## 暴涨[¶](https://ardupilot.org/copter/docs/skyrocket.html#skyrocket)

> [![../\_images/skyrocket-skyvipergpsdrone.png](https://ardupilot.org/copter/\_images/skyrocket-skyvipergpsdrone.png)](https://ardupilot.org/copter/\_images/skyrocket-skyvipergpsdrone.png)

许多SkyRocket无人机使用ArduPilot作为飞行控制软件。 此页面为这些 RTF 无人机的高级用户和潜在开发人员提供了详细信息。

### 在哪里购买[¶](https://ardupilot.org/copter/docs/skyrocket.html#where-to-buy)

警告

SkyRocket 从 2021 年底开始销售的旅程无人机不受 ArduPilot。请参阅[此 ArduPilot 论坛主题](https://discuss.ardupilot.org/t/is-the-sky-viper-journey-se-copter-transmitter-pair-user-upgradeable-to-ardupilot/79275)。

**2017 型号**

自2450年2017月起，_具有自动驾驶仪和GPS功能的Sky Viper v<>GPS无人机_在美国，澳大利亚，加拿大，智利，法国，德国，荷兰，立陶宛，墨西哥，新西兰，塞尔维亚，英国通过[沃尔玛](https://www.walmart.com/ip/Sky-Viper-Streaming-Drone-with-GPS/797973157)，[亚马逊](https://www.amazon.com/Sky-Viper-v2450GPS-Streaming-Autopilot/dp/B072HH13VQ/ref=lp\_13203361011\_1\_6)和Costco销售。

SkyRocket出售各种不同的无人机。 在2017年的型号中，只有V2450GPS流媒体无人机（将有一个白色外壳）能够运行ArduPilot。

**2018 型号**

2018年2450月，SkyRocket发布了三款新的ArduPilot动力无人机，Fury，Scout和Journey。 Fury和Scout利用基于ArduPilot的OpticalFlow功能的“SurfaceScan”来实现室内飞行稳定性和位置保持，这在这个价格范围内是前所未有的。 旅程使用GPS而不是OpticalFlow，从V2450GPS中吸取经验教训，并在此基础上重新发布完整的GPS支持ArduPilot体验。Scout和Journey的飞行参数和固件可以根据用户认为合适的方式通过嵌入式wifi接入点轻松修改，由APWeb提供支持或使用您喜欢的地面控制软件。 此页面上的大部分信息是为 V<>GPS 编写的，至少部分适用于这些新型号，并在发现更新时对其进行注释。

**2021 型号**

旅程不再出售。取而代之的是Sky Viper Journey SE。经销商可能仍列出了旅程，但已观察到已发货旅程SE。

### 讨论[¶](https://ardupilot.org/copter/docs/skyrocket.html#discussion)

我们在ArduPilot论坛上有一个[SkyViper部分](https://discuss.ardupilot.org/c/arducopter/skyviper)。看看那里，看看人们在做什么并提出问题。

更多开发人员特定信息，包括如何编译 sonix 和 ardupilot 固件，可以在[开发人员 wiki](https://ardupilot.org/dev/docs/skyviper.html) 上找到。

### 玩具模式[¶](https://ardupilot.org/copter/docs/skyrocket.html#toy-mode)

天蛇默认设置了玩具模式。玩具模式处理以下特定于天空蝰蛇 2450GPS 的功能：

* 处理发射器按下按钮
* 当棍子闲置时，神奇地修剪它们，SV被解除武装
* 根据情况打开和关闭围栏
* 基本上，如果 GPS 是“好的”，围栏是武装的，如果 GPS 是“不好的”，围栏就会被解除武装（出于显而易见的原因）
* 玩具模式还可以根据 GPS 状态自动在ALT\_HOLD和 LOITER 之间移动。
* 处理 LED 闪光（来源：彼得巴克）
* 玩具模式根据电压自动调整推力
* 玩具模式在使用油门控制进行武装时处理布防脚本，以防止突然爬升（在提高速度之前怠速电机片刻）
* 如果需要，执行一些自动指南针调整

### 硬件[¶](https://ardupilot.org/copter/docs/skyrocket.html#hardware)

* 意法半导体32处理器
* 5x 串行端口
* 1 个 I2C
* 1x SPI
* ICM20789 IMU 包括 3 轴加速度计、陀螺仪和气压计
* Ublox M8 全球定位系统
* 1S 电池（最大 4.2V，更换电池可在亚马逊和其他地方轻松获得）
* 有刷电机;8.5x20mm，kV在16，000和17，000之间。
* 小齿轮为13T，大齿轮为73T，齿轮比约为5.6
* 摄像机可以手动调整为向前、向下或介于两者之间的任何位置
* 2.4Ghz 无线上网，用于遥测和视频
* 145克
* 飞行时间约11分钟
* 最高速度在8米/秒\~10米/秒之间
* 视频流使用带有运行FreeRTOS和OmniVision OV9732芯片的ARM CPU的Sonix板

[![../\_images/飞跃飞行控制器.png](https://ardupilot.org/copter/\_images/skyrocket-flight-controller.png)](https://ardupilot.org/copter/\_images/skyrocket-flight-controller.png)

[sUAS对](https://www.suasnews.com/)Tridge和Matt的新闻采访（来自SkyRocket）：

### 更多信息[¶](https://ardupilot.org/copter/docs/skyrocket.html#more-info)

* [视频](https://ardupilot.org/copter/docs/skyrocket-videos.html)
* [硬件](https://ardupilot.org/copter/docs/skyrocket-hardware.html)
* [投掷模式](https://ardupilot.org/copter/docs/skyrocket-throw.html)
* [使用其他地面站](https://ardupilot.org/copter/docs/skyrocket-gcs.html)
* [上传软件](https://ardupilot.org/copter/docs/skyrocket-software.html)

[以前](https://ardupilot.org/copter/docs/heliquads.html)[下一个](https://ardupilot.org/copter/docs/skyrocket-videos.html)\
