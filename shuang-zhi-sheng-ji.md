# 双直升机

## 双直升机[¶](https://ardupilot.org/copter/docs/dual-helicopter.html#dual-helicopter)

注意

双直升机框架需要[传统的直升机](https://ardupilot.org/copter/docs/traditional-helicopters.html#traditional-helicopters)作为基础固件。它可从[固件服务器](https://firmware.ardupilot.org/)下载。当为固件服务器生成 Copter 时，它会生成多旋翼和传统直升机（带 -heli 后缀）固件。

### 连接和配置[¶](https://ardupilot.org/copter/docs/dual-helicopter.html#connecting-and-configuring)

* 电机的电调应连接到自动驾驶仪的通道 8 输出
* [传统的直升机固件](https://ardupilot.org/copter/docs/traditional-helicopters.html#traditional-helicopters)应加载到车辆上。
* [FRAME\_CLASS](https://ardupilot.org/copter/docs/parameters.html#frame-class) 至 11 （Heli\_Dual）
* [H\_DUAL\_MODE](https://ardupilot.org/copter/docs/parameters.html#h-dual-mode)

与传统[直升机](https://ardupilot.org/copter/docs/traditional-helicopters.html#traditional-helicopters)类似，[辅助开关](https://ardupilot.org/copter/docs/common-auxiliary-functions.html#common-auxiliary-functions)应设置为“电机联锁”以打开/关闭电机。通常这是通道 8，因此您可以将[RC8\_OPTION](https://ardupilot.org/copter/docs/parameters.html#rc8-option)设置为 32。

注意

请参阅[传统直升机 – 斜盘设置](https://ardupilot.org/copter/docs/traditional-helicopter-swashplate-setup.html#traditional-helicopter-swashplate-setup)，了解有关如何使用以下参数设置每个斜盘的基本信息。

#### 串联（纵向）[¶](https://ardupilot.org/copter/docs/dual-helicopter.html#tandem-longitudinal)

[![../\_images/dual\_heli\_chinook.jpeg](https://ardupilot.org/copter/\_images/dual\_heli\_chinook.jpeg)](https://ardupilot.org/copter/\_images/dual\_heli\_chinook.jpeg)

此设置假定前转子斜盘由伺服输出 1、2 和 3 控制，后转子斜盘由伺服输出 4、5 和 6 控制。

参数设置：

* [H\_DUAL\_MODE](https://ardupilot.org/copter/docs/parameters.html#h-dual-mode) - 纵向配置为 0
* [H\_DCP\_SCALER](https://ardupilot.org/copter/docs/parameters.html#h-dcp-scaler) - 将差分集体输出缩放到转子，以实现节距轴输入
* [H\_DCP\_YAW](https://ardupilot.org/copter/docs/parameters.html#h-dcp-yaw) - 前馈输入到偏航轴，用于俯仰轴 （DCP） 输入
* [H\_YAW\_SCALER](https://ardupilot.org/copter/docs/parameters.html#h-yaw-scaler) - 根据偏航轴输入缩放差分横向循环。对于此设置，这是一个正数。
* [H\_COL\_MAX](https://ardupilot.org/copter/docs/parameters.html#h-col-max) - PWM，用于前转子头上对应于[H\_COL\_ANG\_MAX](https://ardupilot.org/copter/docs/parameters.html#h-col-ang-max)的最大集体螺距
* [H\_COL\_MIN](https://ardupilot.org/copter/docs/parameters.html#h-col-min) - PWM 用于前转子头上对应于 [H\_COL\_ANG\_MIN](https://ardupilot.org/copter/docs/parameters.html#h-col-ang-min) 的最小集体螺距
* [H\_SW\_TYPE](https://ardupilot.org/copter/docs/parameters.html#h-sw-type-ap-motorsheli-dual) - 用于前转子头的斜盘式
* [H\_SW\_COL\_DIR](https://ardupilot.org/copter/docs/parameters.html#h-sw-col-dir-ap-motorsheli-dual) - 前转子头的斜盘集体方向
* [H\_SW\_LIN\_SVO](https://ardupilot.org/copter/docs/parameters.html#h-sw-lin-svo-ap-motorsheli-dual) - 启用前转子头的线性伺服功能
* [H\_COL2\_MIN](https://ardupilot.org/copter/docs/parameters.html#h-col2-min) - PWM 用于后转子头上对应于 [H\_COL\_ANG\_MIN](https://ardupilot.org/copter/docs/parameters.html#h-col-ang-min) 的最小集体螺距
* [H\_COL2\_MAX](https://ardupilot.org/copter/docs/parameters.html#h-col2-max)- PWM，用于后转子头上对应于[H\_COL\_ANG\_MAX](https://ardupilot.org/copter/docs/parameters.html#h-col-ang-max)的最大集体螺距
* [H\_SW2\_TYPE](https://ardupilot.org/copter/docs/parameters.html#h-sw2-type) - 后旋翼头斜盘式
* [H\_SW2\_COL\_DIR](https://ardupilot.org/copter/docs/parameters.html#h-sw2-col-dir) - 后旋翼头的斜盘集体方向
* [H\_SW2\_LIN\_SVO](https://ardupilot.org/copter/docs/parameters.html#h-sw2-lin-svo) - 启用后转子头的线性伺服功能
* [H\_DCP\_TRIM](https://ardupilot.org/copter/docs/parameters.html#h-dcp-trim) - 消除斜盘设置中由于重心偏移或转子之间的差异而导致的节距 I 项偏差。如果在风平浪静的风中徘徊时俯仰轴具有 I 项偏差，请使用 DCP\_TRIM 中的偏差值将 I 项重新居中。

仅当前斜盘设置为 H3 通用时[H\_SW\_TYPE](https://ardupilot.org/copter/docs/parameters.html#h-sw-type-ap-motorsheli-dual)才需要这些。

* [H\_SW\_H3\_ENABLE](https://ardupilot.org/copter/docs/parameters.html#h-sw-h3-enable-ap-motorsheli-dual) - 不要手动设置！一旦[H\_SW\_TYPE](https://ardupilot.org/copter/docs/parameters.html#h-sw-type-ap-motorsheli-dual)设置为 H3 通用，就会自动设置
* [H\_SW\_H3\_SV1\_POS](https://ardupilot.org/copter/docs/parameters.html#h-sw-h3-sv1-pos-ap-motorsheli-dual)
* [H\_SW\_H3\_SV2\_POS](https://ardupilot.org/copter/docs/parameters.html#h-sw-h3-sv2-pos-ap-motorsheli-dual)
* [H\_SW\_H3\_SV3\_POS](https://ardupilot.org/copter/docs/parameters.html#h-sw-h3-sv3-pos-ap-motorsheli-dual)
* [H\_SW\_H3\_PHANG](https://ardupilot.org/copter/docs/parameters.html#h-sw-h3-phang-ap-motorsheli-dual)

只有当[H\_SW2\_TYPE](https://ardupilot.org/copter/docs/parameters.html#h-sw2-type)设置为H3通用时，后斜盘才需要这些。

* [H\_SW2\_H3\_ENABLE](https://ardupilot.org/copter/docs/parameters.html#h-sw2-h3-enable) - 不要手动设置！一旦[H\_SW2\_TYPE](https://ardupilot.org/copter/docs/parameters.html#h-sw2-type)设置为 H3 通用，就会自动设置
* [H\_SW2\_H3\_SV1\_POS](https://ardupilot.org/copter/docs/parameters.html#h-sw2-h3-sv1-pos)
* [H\_SW2\_H3\_SV2\_POS](https://ardupilot.org/copter/docs/parameters.html#h-sw2-h3-sv2-pos)
* [H\_SW2\_H3\_SV3\_POS](https://ardupilot.org/copter/docs/parameters.html#h-sw2-h3-sv3-pos)
* [H\_SW2\_H3\_PHANG](https://ardupilot.org/copter/docs/parameters.html#h-sw2-h3-phang)

此参数不用于纵向配置 - [H\_YAW\_REV\_EXPO](https://ardupilot.org/copter/docs/parameters.html#h-yaw-rev-expo)

#### 并排（横向）[¶](https://ardupilot.org/copter/docs/dual-helicopter.html#side-by-side-transverse)

[![../\_images/dual\_heli\_transverse.jpg](https://ardupilot.org/copter/\_images/dual\_heli\_transverse.jpg)](https://ardupilot.org/copter/\_images/dual\_heli\_transverse.jpg)

此设置假定左转子斜盘由伺服输出 1、2 和 3 控制，右转子斜盘由伺服输出 4、5 和 6 控制。

参数设置：

* [H\_DUAL\_MODE](https://ardupilot.org/copter/docs/parameters.html#h-dual-mode) - 横向配置为 1
* [H\_DCP\_SCALER](https://ardupilot.org/copter/docs/parameters.html#h-dcp-scaler) - 将差分集合输出缩放到转子以进行滚动轴输入
* [H\_DCP\_YAW](https://ardupilot.org/copter/docs/parameters.html#h-dcp-yaw) - 前馈输入到偏航轴，用于横滚轴 （DCP） 输入
* [H\_YAW\_SCALER](https://ardupilot.org/copter/docs/parameters.html#h-yaw-scaler) - 根据偏航轴输入缩放差分纵向循环。对于此设置，这是一个正数。
* [H\_COL\_MAX](https://ardupilot.org/copter/docs/parameters.html#h-col-max) - PWM 用于左转子头上对应于 [H\_COL\_ANG\_MAX](https://ardupilot.org/copter/docs/parameters.html#h-col-ang-max) 的最大集体螺距
* [H\_COL\_MIN](https://ardupilot.org/copter/docs/parameters.html#h-col-min) - PWM 用于左转子头上对应于[H\_COL\_ANG\_MIN](https://ardupilot.org/copter/docs/parameters.html#h-col-ang-min)的最小集体螺距
* [H\_SW\_TYPE](https://ardupilot.org/copter/docs/parameters.html#h-sw-type-ap-motorsheli-dual) - 左转子头斜盘式
* [H\_SW\_COL\_DIR](https://ardupilot.org/copter/docs/parameters.html#h-sw-col-dir-ap-motorsheli-dual) - 左旋翼头的斜盘集体方向
* [H\_SW\_LIN\_SVO](https://ardupilot.org/copter/docs/parameters.html#h-sw-lin-svo-ap-motorsheli-dual) - 启用左转子头的线性伺服功能
* [H\_COL2\_MIN](https://ardupilot.org/copter/docs/parameters.html#h-col2-min) - PWM 用于右转子头上对应于[H\_COL\_ANG\_MIN](https://ardupilot.org/copter/docs/parameters.html#h-col-ang-min)的最小集体螺距
* [H\_COL2\_MAX](https://ardupilot.org/copter/docs/parameters.html#h-col2-max) - PWM，用于右转子头上对应于[H\_COL\_ANG\_MAX](https://ardupilot.org/copter/docs/parameters.html#h-col-ang-max)的最大集体螺距
* [H\_SW2\_TYPE](https://ardupilot.org/copter/docs/parameters.html#h-sw2-type) - 右转子头斜盘式
* [H\_SW2\_COL\_DIR](https://ardupilot.org/copter/docs/parameters.html#h-sw2-col-dir) - 右转子头的斜盘集体方向
* [H\_SW2\_LIN\_SVO](https://ardupilot.org/copter/docs/parameters.html#h-sw2-lin-svo) - 启用右转子头的线性伺服功能
* [H\_DCP\_TRIM](https://ardupilot.org/copter/docs/parameters.html#h-dcp-trim) - 消除斜盘设置中由于重心偏移或转子之间的差异而导致的卷 I 项偏差。如果在风平浪静的风中徘徊时，滚动轴具有 I 项偏差，请使用 DCP\_TRIM 中的偏差值将 I 项重新居中。

仅当[H\_SW\_TYPE](https://ardupilot.org/copter/docs/parameters.html#h-sw-type-ap-motorsheli-dual)设置为H3通用时，左侧斜盘才需要这些。

* [H\_SW\_H3\_ENABLE](https://ardupilot.org/copter/docs/parameters.html#h-sw-h3-enable-ap-motorsheli-dual) - 不要手动设置！一旦[H\_SW\_TYPE](https://ardupilot.org/copter/docs/parameters.html#h-sw-type-ap-motorsheli-dual)设置为 H3 通用，就会自动设置
* [H\_SW\_H3\_SV1\_POS](https://ardupilot.org/copter/docs/parameters.html#h-sw-h3-sv1-pos-ap-motorsheli-dual)
* [H\_SW\_H3\_SV2\_POS](https://ardupilot.org/copter/docs/parameters.html#h-sw-h3-sv2-pos-ap-motorsheli-dual)
* [H\_SW\_H3\_SV3\_POS](https://ardupilot.org/copter/docs/parameters.html#h-sw-h3-sv3-pos-ap-motorsheli-dual)
* [H\_SW\_H3\_PHANG](https://ardupilot.org/copter/docs/parameters.html#h-sw-h3-phang-ap-motorsheli-dual)

仅当 [H\_SW2\_TYPE](https://ardupilot.org/copter/docs/parameters.html#h-sw2-type) 设置为 H3 通用时，正确的斜盘才需要这些。

* [H\_SW2\_H3\_ENABLE](https://ardupilot.org/copter/docs/parameters.html#h-sw2-h3-enable) - 不要手动设置！一旦[H\_SW2\_TYPE](https://ardupilot.org/copter/docs/parameters.html#h-sw2-type)设置为 H3 通用，就会自动设置
* [H\_SW2\_H3\_SV1\_POS](https://ardupilot.org/copter/docs/parameters.html#h-sw2-h3-sv1-pos)
* [H\_SW2\_H3\_SV2\_POS](https://ardupilot.org/copter/docs/parameters.html#h-sw2-h3-sv2-pos)
* [H\_SW2\_H3\_SV3\_POS](https://ardupilot.org/copter/docs/parameters.html#h-sw2-h3-sv3-pos)
* [H\_SW2\_H3\_PHANG](https://ardupilot.org/copter/docs/parameters.html#h-sw2-h3-phang)

此参数不用于纵向配置

* [H\_YAW\_REV\_EXPO](https://ardupilot.org/copter/docs/parameters.html#h-yaw-rev-expo)

#### 啮合[¶](https://ardupilot.org/copter/docs/dual-helicopter.html#intermeshing)

[![../\_images/dual\_heli\_intermeshing.jpg](https://ardupilot.org/copter/\_images/dual\_heli\_intermeshing.jpg)](https://ardupilot.org/copter/\_images/dual\_heli\_intermeshing.jpg)

此设置假定左转子斜盘由伺服输出 1、2 和 3 控制，右转子斜盘由伺服输出 4、5 和 6 控制。

参数设置：

* [H\_DUAL\_MODE](https://ardupilot.org/copter/docs/parameters.html#h-dual-mode) - 设置为2进行网格划分配置
* [H\_DCP\_SCALER](https://ardupilot.org/copter/docs/parameters.html#h-dcp-scaler) - 将差分集合输出缩放到偏航轴输入的转子。对于正值，左转子将逆时针旋转以给出正确的偏航响应。
* [H\_YAW\_SCALER](https://ardupilot.org/copter/docs/parameters.html#h-yaw-scaler) - 根据偏航轴输入缩放差分纵向循环。对于此设置，这是一个正数。
* [H\_COL\_MAX](https://ardupilot.org/copter/docs/parameters.html#h-col-max) - PWM 用于左转子头上对应于 [H\_COL\_ANG\_MAX](https://ardupilot.org/copter/docs/parameters.html#h-col-ang-max) 的最大集体螺距
* [H\_COL\_MIN](https://ardupilot.org/copter/docs/parameters.html#h-col-min) - PWM 用于左转子头上对应于[H\_COL\_ANG\_MIN](https://ardupilot.org/copter/docs/parameters.html#h-col-ang-min)的最小集体螺距
* [H\_SW\_TYPE](https://ardupilot.org/copter/docs/parameters.html#h-sw-type-ap-motorsheli-dual) - 左转子头斜盘式
* [H\_SW\_COL\_DIR](https://ardupilot.org/copter/docs/parameters.html#h-sw-col-dir-ap-motorsheli-dual) - 左旋翼头的斜盘集体方向
* [H\_SW\_LIN\_SVO](https://ardupilot.org/copter/docs/parameters.html#h-sw-lin-svo-ap-motorsheli-dual) - 启用左转子头的线性伺服功能
* [H\_COL2\_MIN](https://ardupilot.org/copter/docs/parameters.html#h-col2-min) - PWM 用于右转子头上对应于[H\_COL\_ANG\_MIN](https://ardupilot.org/copter/docs/parameters.html#h-col-ang-min)的最小集体螺距
* [H\_COL2\_MAX](https://ardupilot.org/copter/docs/parameters.html#h-col2-max) - PWM，用于右转子头上对应于[H\_COL\_ANG\_MAX](https://ardupilot.org/copter/docs/parameters.html#h-col-ang-max)的最大集体螺距
* [H\_SW2\_TYPE](https://ardupilot.org/copter/docs/parameters.html#h-sw2-type) - 右转子头斜盘式
* [H\_SW2\_COL\_DIR](https://ardupilot.org/copter/docs/parameters.html#h-sw2-col-dir) - 右转子头的斜盘集体方向
* [H\_SW2\_LIN\_SVO](https://ardupilot.org/copter/docs/parameters.html#h-sw2-lin-svo) - 启用右转子头的线性伺服功能
* [H\_YAW\_REV\_EXPO](https://ardupilot.org/copter/docs/parameters.html#h-yaw-rev-expo) - 偏航崇敬者平滑指数，平滑过渡接近零集合区域。将此参数增加到平整范围。设置为 -1 可禁用反向器。

仅当[H\_SW\_TYPE](https://ardupilot.org/copter/docs/parameters.html#h-sw-type-ap-motorsheli-dual)设置为H3通用时，左侧斜盘才需要这些。

* [H\_SW\_H3\_ENABLE](https://ardupilot.org/copter/docs/parameters.html#h-sw-h3-enable-ap-motorsheli-dual) - 不要手动设置！一旦[H\_SW\_TYPE](https://ardupilot.org/copter/docs/parameters.html#h-sw-type-ap-motorsheli-dual)设置为 H3 通用，就会自动设置
* [H\_SW\_H3\_SV1\_POS](https://ardupilot.org/copter/docs/parameters.html#h-sw-h3-sv1-pos-ap-motorsheli-dual)
* [H\_SW\_H3\_SV2\_POS](https://ardupilot.org/copter/docs/parameters.html#h-sw-h3-sv2-pos-ap-motorsheli-dual)
* [H\_SW\_H3\_SV3\_POS](https://ardupilot.org/copter/docs/parameters.html#h-sw-h3-sv3-pos-ap-motorsheli-dual)
* [H\_SW\_H3\_PHANG](https://ardupilot.org/copter/docs/parameters.html#h-sw-h3-phang-ap-motorsheli-dual)

仅当 [H\_SW2\_TYPE](https://ardupilot.org/copter/docs/parameters.html#h-sw2-type) 设置为 H3 通用时，正确的斜盘才需要这些。

* [H\_SW2\_H3\_ENABLE](https://ardupilot.org/copter/docs/parameters.html#h-sw2-h3-enable) - 不要手动设置！一旦[H\_SW2\_TYPE](https://ardupilot.org/copter/docs/parameters.html#h-sw2-type)设置为 H3 通用，就会自动设置
* [H\_SW2\_H3\_SV1\_POS](https://ardupilot.org/copter/docs/parameters.html#h-sw2-h3-sv1-pos)
* [H\_SW2\_H3\_SV2\_POS](https://ardupilot.org/copter/docs/parameters.html#h-sw2-h3-sv2-pos)
* [H\_SW2\_H3\_SV3\_POS](https://ardupilot.org/copter/docs/parameters.html#h-sw2-h3-sv3-pos)
* [H\_SW2\_H3\_PHANG](https://ardupilot.org/copter/docs/parameters.html#h-sw2-h3-phang)

这些参数不用于网格划分配置

* [H\_DCP\_YAW](https://ardupilot.org/copter/docs/parameters.html#h-dcp-yaw)
* [H\_DCP\_TRIM](https://ardupilot.org/copter/docs/parameters.html#h-dcp-trim)

#### 同轴的[¶](https://ardupilot.org/copter/docs/dual-helicopter.html#coaxial)

[![../\_images/dual\_heli\_coaxial.jpg](https://ardupilot.org/copter/\_images/dual\_heli\_coaxial.jpg)](https://ardupilot.org/copter/\_images/dual\_heli\_coaxial.jpg)

此设置假设逆时针转子斜盘由伺服输出 1、2 和 3 控制，顺时针转子斜盘由伺服输出 4、5 和 6 控制。

参数设置：

* [H\_DUAL\_MODE](https://ardupilot.org/copter/docs/parameters.html#h-dual-mode) - 设置为2进行网格划分配置
* [H\_DCP\_SCALER](https://ardupilot.org/copter/docs/parameters.html#h-dcp-scaler) - 将差分集合输出缩放到偏航轴输入的转子。
* [H\_YAW\_SCALER](https://ardupilot.org/copter/docs/parameters.html#h-yaw-scaler) - 对于同轴配置，此参数设置为零。
* [H\_COL\_MAX](https://ardupilot.org/copter/docs/parameters.html#h-col-max)- PWM，用于逆时针转子头上对应于[H\_COL\_ANG\_MAX](https://ardupilot.org/copter/docs/parameters.html#h-col-ang-max)的最大集体螺距
* [H\_COL\_MIN](https://ardupilot.org/copter/docs/parameters.html#h-col-min) - PWM 用于逆时针转子头上对应于 [H\_COL\_ANG\_MIN](https://ardupilot.org/copter/docs/parameters.html#h-col-ang-min) 的最小集体螺距
* [H\_SW\_TYPE](https://ardupilot.org/copter/docs/parameters.html#h-sw-type-ap-motorsheli-dual) - 逆时针转子头斜盘式
* [H\_SW\_COL\_DIR](https://ardupilot.org/copter/docs/parameters.html#h-sw-col-dir-ap-motorsheli-dual) - 逆时针转子头的斜盘集合方向
* [H\_SW\_LIN\_SVO](https://ardupilot.org/copter/docs/parameters.html#h-sw-lin-svo-ap-motorsheli-dual) - 启用逆时针转子头的线性伺服功能
* [H\_COL2\_MIN](https://ardupilot.org/copter/docs/parameters.html#h-col2-min) - PWM 表示顺时针转子头上对应于[H\_COL\_ANG\_MIN](https://ardupilot.org/copter/docs/parameters.html#h-col-ang-min)的最小集体螺距
* [H\_COL2\_MAX](https://ardupilot.org/copter/docs/parameters.html#h-col2-max) - PWM，用于顺时针转子头上对应于[H\_COL\_ANG\_MAX](https://ardupilot.org/copter/docs/parameters.html#h-col-ang-max)的最大集体螺距
* [H\_SW2\_TYPE](https://ardupilot.org/copter/docs/parameters.html#h-sw2-type) - 顺时针转子头斜盘式
* [H\_SW2\_COL\_DIR](https://ardupilot.org/copter/docs/parameters.html#h-sw2-col-dir) - 顺时针转子头的斜盘集合方向
* [H\_SW2\_LIN\_SVO](https://ardupilot.org/copter/docs/parameters.html#h-sw2-lin-svo) - 启用顺时针转子头的线性伺服功能
* [H\_YAW\_REV\_EXPO](https://ardupilot.org/copter/docs/parameters.html#h-yaw-rev-expo) - 偏航崇敬者平滑指数，平滑过渡接近零集合区域。将此参数增加到平整范围。设置为 -1 可禁用反向器。

只有当逆时针斜盘设置为 H3 通用时[H\_SW\_TYPE](https://ardupilot.org/copter/docs/parameters.html#h-sw-type-ap-motorsheli-dual)这些才需要。

* [H\_SW\_H3\_ENABLE](https://ardupilot.org/copter/docs/parameters.html#h-sw-h3-enable-ap-motorsheli-dual) - 不要手动设置！一旦[H\_SW\_TYPE](https://ardupilot.org/copter/docs/parameters.html#h-sw-type-ap-motorsheli-dual)设置为 H3 通用，就会自动设置
* [H\_SW\_H3\_SV1\_POS](https://ardupilot.org/copter/docs/parameters.html#h-sw-h3-sv1-pos-ap-motorsheli-dual)
* [H\_SW\_H3\_SV2\_POS](https://ardupilot.org/copter/docs/parameters.html#h-sw-h3-sv2-pos-ap-motorsheli-dual)
* [H\_SW\_H3\_SV3\_POS](https://ardupilot.org/copter/docs/parameters.html#h-sw-h3-sv3-pos-ap-motorsheli-dual)
* [H\_SW\_H3\_PHANG](https://ardupilot.org/copter/docs/parameters.html#h-sw-h3-phang-ap-motorsheli-dual)

仅当[H\_SW2\_TYPE](https://ardupilot.org/copter/docs/parameters.html#h-sw2-type)设置为H3通用时，顺时针斜盘才需要这些。

* [H\_SW2\_H3\_ENABLE](https://ardupilot.org/copter/docs/parameters.html#h-sw2-h3-enable) - 不要手动设置！一旦[H\_SW2\_TYPE](https://ardupilot.org/copter/docs/parameters.html#h-sw2-type)设置为 H3 通用，就会自动设置
* [H\_SW2\_H3\_SV1\_POS](https://ardupilot.org/copter/docs/parameters.html#h-sw2-h3-sv1-pos)
* [H\_SW2\_H3\_SV2\_POS](https://ardupilot.org/copter/docs/parameters.html#h-sw2-h3-sv2-pos)
* [H\_SW2\_H3\_SV3\_POS](https://ardupilot.org/copter/docs/parameters.html#h-sw2-h3-sv3-pos)
* [H\_SW2\_H3\_PHANG](https://ardupilot.org/copter/docs/parameters.html#h-sw2-h3-phang)

这些参数不用于同轴配置

* [H\_DCP\_YAW](https://ardupilot.org/copter/docs/parameters.html#h-dcp-yaw)
* [H\_DCP\_TRIM](https://ardupilot.org/copter/docs/parameters.html#h-dcp-trim)
