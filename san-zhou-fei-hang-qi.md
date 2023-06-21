# 三轴飞行器

## 三轴飞行器配置[¶](https://ardupilot.org/copter/docs/tricopter.html#tricopter-configuration)

本页概述了获得三轴飞行器所需的特殊设置 飞行。[设置多旋翼飞行器的更一般说明](https://ardupilot.org/copter/docs/initial-setup.html#initial-setup)应 用于设置的所有其他方面。

[![../\_images/APM\_2\_5\_MOTORS\_TRI.jpg](https://ardupilot.org/copter/\_images/APM\_2\_5\_MOTORS\_TRI.jpg)](https://ardupilot.org/copter/\_images/APM\_2\_5\_MOTORS\_TRI.jpg)

加载固件后，请设置：

* [FRAME\_CLASS](https://ardupilot.org/copter/docs/parameters.html#frame-class) 至 7（“三”）

与早期版本相比，RC输入和输出参数的更好分离也导致了一些变化。以下是三轴飞行器特定参数的完整列表：

* [MOT\_YAW\_SV\_ANGLE](https://ardupilot.org/copter/docs/parameters.html#mot-yaw-sv-angle)：尾部伺服的最大倾斜角度（以度为单位）。这允许根据后电机的倾斜角度适当调整后电机的推力。默认值为 30 度。“0”表示尾部伺服器只能直接指向上方（不允许飞行器飞行），“90”表示尾部伺服器可以水平指向。
* [SERVO7\_MIN](https://ardupilot.org/copter/docs/parameters.html#servo7-min)：尾部伺服在绑定发生前的最低PWM值。
* [SERVO7\_MAX](https://ardupilot.org/copter/docs/parameters.html#servo7-max)：尾部伺服在绑定发生前的最高PWM值。
* [SERVO7\_TRIM](https://ardupilot.org/copter/docs/parameters.html#servo7-trim)：尾部伺服器的PWM值接近防止尾部旋转所需的PWM值。
* [SERVO7\_REVERSED](https://ardupilot.org/copter/docs/parameters.html#servo7-reversed)：尾部伺服的反向设置。0 = 伺服沿默认方向移动，1 表示反向移动。

通过将适当的SERVOX\_FUNCTION设置为 7，可以将用于尾部伺服的 RC 输出通道从其默认值（通道 39）更改为 6。 例如，[Pixracer](https://ardupilot.org/copter/docs/common-pixracer-overview.html#common-pixracer-overview) 只有 5 个输出通道，因此通过将[SERVO5\_FUNCTION](https://ardupilot.org/copter/docs/parameters.html#servo5-function)设置为 39，可以将尾部伺服移动到输出通道 <>。 请注意，如果更改了输出通道，则必须为新的输出通道正确设置SERVOx\_MIN、SERVOx\_MAX、SERVOx\_TRIM和SERVOx\_REVERSED。
