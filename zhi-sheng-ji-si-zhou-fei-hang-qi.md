# 直升机四轴飞行器

## 直升机四轴飞行器（可变螺距多旋翼飞行器）[¶](https://ardupilot.org/copter/docs/heliquads.html#heliquads-variable-pitch-multicopters)

ArduPilot支持HeliQuads，也称为Collective Pitch Quadboards或Variable Pitch Multicopters。

![../\_images/heliquad.png](https://ardupilot.org/copter/\_images/heliquad.png)

注意

直升机四轮摩托车需要[一架传统的直升机](https://ardupilot.org/copter/docs/traditional-helicopters.html#traditional-helicopters)作为基础固件。它可从[固件服务器](https://firmware.ardupilot.org/)下载。当Copter被编译时，它现在可以生成传统的直升机和多旋翼固件。

这些车辆在 4 个转子中的每一个上都使用独立控制的集体变桨，单个电动机通过皮带和扭矩管以相同的速度为所有 4 个转子提供动力。 它是高度特技飞行的，能够倒置飞行，但可能会遭受[高振动水平](https://ardupilot.org/copter/docs/common-measuring-vibration.html#common-measuring-vibration)。

### 在哪里购买[¶](https://ardupilot.org/copter/docs/heliquads.html#where-to-buy)

* WLtoys Assassin V383可从零售商处购买，包括 [WLtoys.eu](https://wltoys.eu/wltoys-v383)

### 连接和配置[¶](https://ardupilot.org/copter/docs/heliquads.html#connecting-and-configuring)

[![../\_images/heliquad-pixhawk.png](https://ardupilot.org/copter/\_images/heliquad-pixhawk.png)](https://ardupilot.org/copter/\_images/heliquad-pixhawk.png)

* 每个伺服器应使用与常规多旋翼飞行器上的电机相同的输出进行连接（[请参阅此处的订单](https://ardupilot.org/copter/docs/connect-escs-and-motors.html#connect-escs-and-motors)）)
* 电机的电调应连接到自动驾驶仪的通道 8 输出
* [传统的直升机固件](https://ardupilot.org/copter/docs/traditional-helicopters.html#traditional-helicopters)应加载到车辆上。

如果使用[WLToys Assassin V383，则可以在此处找到参数文件](https://github.com/ArduPilot/ardupilot/blob/master/Tools/Frame\_params/WLToys\_V383\_HeliQuad.param)，该文件可用于立即设置所有参数。 对于其他构建，这些是应该设置的标准参数：

* [FRAME\_CLASS](https://ardupilot.org/copter/docs/parameters.html#frame-class)至13（直升机四轮）
* [FRAME\_TYPE](https://ardupilot.org/copter/docs/parameters.html#frame-class) 到 1（如果右前电机逆时针旋转，则为“X”）或 3（如果右前电机顺时针旋转，则为“H”）

与传统[直升机](https://ardupilot.org/copter/docs/traditional-helicopters.html#traditional-helicopters)类似，[辅助开关](https://ardupilot.org/copter/docs/common-auxiliary-functions.html#common-auxiliary-functions)应设置为“电机联锁”以打开/关闭电机。通常这是通道 8，因此您可以将[RC8\_OPTION](https://ardupilot.org/copter/docs/parameters.html#rc8-option)设置为 32。

### 视频[¶](https://ardupilot.org/copter/docs/heliquads.html#videos)

倒飞测试

堪培拉无人机图片

![../\_images/heliquad-canberrauav.jpg](https://ardupilot.org/copter/\_images/heliquad-canberrauav.jpg)
