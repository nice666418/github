# 单轴飞行器和同轴直升机

## 单轴飞行器和同轴直升机[¶](https://ardupilot.org/copter/docs/singlecopter-and-coaxcopter.html#singlecopter-and-coaxcopter)

[![../\_images/单旋翼龙.jpg](https://ardupilot.org/copter/\_images/single-copter-droner.jpg)](https://ardupilot.org/copter/\_images/single-copter-droner.jpg)

单旋翼飞机，垂直安装自动驾驶仪。图片由“droner”提供

单轴和同轴直升机有一个或两个螺旋桨来提供推力，2到4个单独的襟翼来提供横滚、俯仰和偏航控制。单轴直升机和同轴直升机之间的区别在于：

_单轴飞行器_

* 具有单个电机和 4 个独立襟翼。
* 车辆的偏航通过调整所有四个鳍片以稍微顺时针或逆时针指向来控制。

_同轴直升机_

* 有两个反向旋转电机和至少 2 个独立襟翼（可以使用 4 个单独的伺服/襟翼，但车辆两侧的鳍片将一起移动）
* 车辆的偏航通过调节两个电机的速度来控制。即加速顺时针电机，同时减速逆时针电机将导致车辆逆时针旋转

### 安装和连接自动驾驶仪[¶](https://ardupilot.org/copter/docs/singlecopter-and-coaxcopter.html#mounting-and-connecting-the-autopilot)

[![../\_images/single-copter-layout.png](https://ardupilot.org/copter/\_images/single-copter-layout.png)](https://ardupilot.org/copter/\_images/single-copter-layout.png)

默认情况下，自动驾驶仪的安装方式应类似于“加号”四边形。电路板应水平，白色箭头指向前襟翼。 与其他车辆一样，电路板应靠近车辆的重心放置。 如果将自动舵朝上安装更方便，请将[AHRS\_ORIENTATION](https://ardupilot.org/copter/docs/parameters.html#ahrs-orientation)设置为 25 （Pitch270）。

将舵机连接到自动驾驶仪的输出，通常用于 Copter 的电机，并在其SERVOx\_FUNCTION中指定为电机 1 到电机 6：

* 电机 1 ： 前襟翼
* 电机 2 ： 右襟翼
* 电机 3 ： 后襟翼（同轴直升机可选）
* 电机 4 ： 左襟翼（同轴直升机可选）
* 电机 5 ： 上部 （CCW） 电机
* 电机 6 ： 下部 （CW） 电机 （CW，仅适用于同轴直升机）

### 加载固件[¶](https://ardupilot.org/copter/docs/singlecopter-and-coaxcopter.html#loading-the-firmware)

从Copter-3.5.x开始，所有多旋翼固件（四旋翼，六旋翼，八频，八旋翼，y6，三，单轴，同轴）包括单轴和同轴直升机，已合并到单个固件中。 这意味着四轴（或其他多旋翼）固件应加载到自动驾驶仪上，然后请设置：

* [单](https://ardupilot.org/copter/docs/parameters.html#frame-class)轴飞行器为 FRAME\_CLASS 至 8，同轴直升机为 9

#### 设置襟翼[¶](https://ardupilot.org/copter/docs/singlecopter-and-coaxcopter.html#setting-up-the-flaps)

每个襟翼的中性位置、运动方向、最小和最大偏转可以使用SERVOx\_TRIM、SERVOx\_REVERSED、SERVOx\_MIN和SERVOx\_MAX参数进行配置（其中“x”是 RC 输出编号）。例如，这些是连接到 RC 输出 1 的前襟翼/伺服的参数：

* [SERVO1\_MIN](https://ardupilot.org/copter/docs/parameters.html#servo1-min)：前向襟翼/伺服在达到其物理极限之前的最低 PWM 值。
* [SERVO1\_MAX](https://ardupilot.org/copter/docs/parameters.html#servo1-max)：前向襟翼/伺服在达到其物理极限之前的最高 PWM 值。
* [SERVO1\_TRIM](https://ardupilot.org/copter/docs/parameters.html#servo1-trim)：前襟翼/舵机的PWM值接近保持车辆旋转所需的PWM值。
* [SERVO1\_REVERSED](https://ardupilot.org/copter/docs/parameters.html#servo1-reversed)：正向襟翼/舵机的反向设置。0 = 伺服沿默认方向移动，1 表示反向移动。

#### 测试襟翼运动[¶](https://ardupilot.org/copter/docs/singlecopter-and-coaxcopter.html#testing-the-flap-movement)

* 拆下螺旋桨
* 将车辆放在飞行员前方的平坦表面上
* 在稳定模式下武装战车
* 抬起发射机上的油门并移动横滚杆、俯仰杆和偏航杆，并确认襟翼移动，如下所述

_单轴飞行器_

* 发射机右滚使前后鳍片向右移动
* 发射机向前俯仰导致左右鳍片向前移动
* 发射器右偏航使前鳍向左移动，右鳍向前移动，后鳍向右移动，左鳍向后移动

_同轴直升机_

* 发射机右滚使前后鳍片向右移动
* 发射机向前俯仰导致左右鳍片向前移动
* 发射器右偏航不会导致鳍片运动发生变化，但电机速度会发生变化。顶部（ccw）电机应加速，底部（cw）应减速。

#### 第一架ArduPilot驱动的单旋翼飞行器的视频[¶](https://ardupilot.org/copter/docs/singlecopter-and-coaxcopter.html#video-of-the-first-ardupilot-powered-singlecopter)

以下是非ArduPilot单旋翼和同轴直升机，以提供灵感：

下图所示的车辆使用反向旋转电机对，两个螺旋桨位于电机上方，底部电机的轴向上穿过顶部电机的空心轴。

[![../\_images/vtol.jpg](https://ardupilot.org/copter/\_images/vtol.jpg)](https://ardupilot.org/copter/\_images/vtol.jpg)

下面的车辆有两个电机背靠背安装，一个螺旋桨在上面，另一个在下面，带有适当的支撑支柱。

[![../\_images/mav\_electric.jpg](https://ardupilot.org/copter/\_images/mav\_electric.jpg)](https://ardupilot.org/copter/\_images/mav\_electric.jpg) [![../\_images/vtolcustom2.jpg](https://ardupilot.org/copter/\_images/vtolcustom2.jpg)](https://ardupilot.org/copter/\_images/vtolcustom2.jpg) [![../\_images/P1060929.jpg](https://ardupilot.org/copter/\_images/P1060929.jpg)](https://ardupilot.org/copter/\_images/P1060929.jpg)\
