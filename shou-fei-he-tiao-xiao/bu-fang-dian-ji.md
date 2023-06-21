# 布防电机

武装车辆可以让电机开始旋转。在布防之前， 确保所有的人、物体和任何身体部位（例如手）都是 清除螺旋桨。然后执行以下操作：

1. 打开发射器。
2. 插入锂聚合物电池。校准陀螺仪时，红灯和蓝灯应闪烁几秒钟（不要移动直升机）
3. 预布防检查将自动运行，如果发现任何问题，RGB LED 将闪烁黄色，故障将显示在地面站上。请参考[此页面](https://ardupilot.org/copter/docs/common-prearm-safety-checks.html#common-prearm-safety-checks)
4. 检查您的飞行模式开关是否设置为稳定、ACRO、AltHold、Loiter 或 PosHold
5. 如果使用带安全开关的自动驾驶仪，请按下它直到指示灯变常亮
6. 如果您打算使用自主模式（即悬停、RTL、自动等），请将车辆切换到悬停或 PosHold，并等待 LED 闪烁绿色表示 GPS 锁定良好
7. 按住油门并右舵 5 秒钟来武装电机。不要将方向舵靠右放置太久（>15 秒），否则您将开始[自动修剪](https://ardupilot.org/copter/docs/autotrim.html#autotrim)功能
8. 一旦布防，LED将变常亮，螺旋桨将开始旋转
9. 升起油门起飞

注意

如果您在任何情况下至少将油门保持在 15 秒 在上述模式下，电机将自动撤防。

注意

在某些模式下，您无法布防。请参阅下表：

| 不允许布防的模式  | 异常                                                                                                                                                                                                                                                                                                                    |
| --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 自动        | [AUTO\_OPTIONS](https://ardupilot.org/copter/docs/parameters.html#auto-options)位 0 已设置（允许在模式下布防）                                                                                                                                                                                                                      |
| 自动调谐      |                                                                                                                                                                                                                                                                                                                       |
| 制动        |                                                                                                                                                                                                                                                                                                                       |
| 圈         |                                                                                                                                                                                                                                                                                                                       |
| 空翻        |                                                                                                                                                                                                                                                                                                                       |
| 引导        | 通过 MAVLink DO\_ARM/DISARM 命令、[Lua 脚本](https://ardupilot.org/copter/docs/common-lua-scripts.html#common-lua-scripts)或[常用辅助功能](https://ardupilot.org/copter/docs/common-auxiliary-functions.html#common-auxiliary-functions)开关（如果使用 [GUID\_OPTIONS](https://ardupilot.org/copter/docs/parameters.html#guid-options) 启用） |
| 土地        |                                                                                                                                                                                                                                                                                                                       |
| 劳教        |                                                                                                                                                                                                                                                                                                                       |
| 智能特尔      |                                                                                                                                                                                                                                                                                                                       |
| 系统ID      |                                                                                                                                                                                                                                                                                                                       |
| AVOIDADSB |                                                                                                                                                                                                                                                                                                                       |
| 跟随        |                                                                                                                                                                                                                                                                                                                       |
| 自动调谐      |                                                                                                                                                                                                                                                                                                                       |

### 解除电机防[¶](https://ardupilot.org/copter/docs/arming\_the\_motors.html#disarming-the-motors)

撤防电机将导致电机停止旋转。要解除电机的撤防，请执行以下操作：

1. 检查您的飞行模式开关是否设置为稳定、ACRO、AltHold、Loiter 或 PosHold
2. 至少踩下油门并向左舵 2 秒钟
3. LED 将开始闪烁，指示车辆已撤防
4. 如果使用带安全开关的自动导航仪，请按下它直到 LED 开始闪烁
5. 断开锂电池。
6. 关闭发射机。
