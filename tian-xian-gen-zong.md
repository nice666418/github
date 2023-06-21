# 天线跟踪

## 天线跟踪[¶](https://ardupilot.org/copter/docs/common-antenna-tracking.html#antenna-tracking)

_天线跟踪器是跟踪_车辆位置的系统，并且 使用此信息正确对齐定向天线。这 方法显著改善了信号可以同时存在的范围 从地面站发送和接收。

ArduPilot支持两种天线跟踪方法。两种方法都使用 来自车辆和地面站的GPS信息，用于瞄准天线。 主要区别在于[天线跟踪](https://ardupilot.org/antennatracker/index.html#home)器是独立的 任何特定的GCS。

[天线跟踪器](https://ardupilot.org/antennatracker/index.html#home)

* AntennaTracker固件转动ArduPilot支持的板（[Autopilot硬件选项](https://ardupilot.org/copter/docs/common-autopilots.html#common-autopilots)） 进入天线跟踪器的控制器。
* 该板计算所需的天线方向，并可以驱动 天线的直接伺服。
* 可以使用任务规划器（或任何其他GCS），但不是必需的。

[基于任务规划器的GPS跟踪](https://ardupilot.org/copter/docs/common-mission-planner-gps-based-antenna-tracking.html#common-mission-planner-gps-based-antenna-tracking)

* 使用_任务规划器_GCS确定瞄准的方向 天线。
* 运行任务规划器的 PC 必须具有 GPS。
* 您将需要一个特殊的伺服驱动器板来控制伺服器。
* [任务规划器天线跟踪](https://ardupilot.org/copter/docs/common-mission-planner-gps-based-antenna-tracking.html)
* [天线设计概述](https://ardupilot.org/copter/docs/common-antenna-design.html)
