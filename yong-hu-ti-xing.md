# 用户提醒

## 用户提醒[¶](https://ardupilot.org/copter/docs/common-user-alerts.html#user-alerts)

用户警报是可能影响车辆安全运行的 ArduPilot 问题的正式报告。

强烈建议所有ArduPilot用户定期查看此页面，以获取可能影响其车辆的任何用户警报。

用户警报仅适用于ArduPilot软件问题。此阶段不包括制造商硬件，尽管可能会在以后进行审查。

用户警报文档可在[开发人员 wiki](https://ardupilot.org/dev/docs/user-alerts-developer.html#user-alerts-developer) 上找到。

有关特定用户警报的详细信息，请参阅[用户警报 数据库](https://firmware.ardupilot.org/userAlerts/alerts.html)。

注意

从 16 年 09 月 2020 日（或更高版本）报告的所有用户警报都在用户警报数据库中。没有保证 数据库包含在此日期之前报告的所有用户警报。

以下警报适用：

| 警报 ID           | 临界     | 受影响的主板 | 受影响的版本       | 描述                                                                                                                                                                                                                                                | 缓解          | 地位            |
| --------------- | ------ | ------ | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- | ------------- |
| 编号段：编号： UA00001 | 次要 （4） | 都      | 4.0.5 <的所有版本 | 在基于STM32的电路板上使用中断驱动输入时，如果发生外部硬件故障，产生极高的中断率（每秒超过500，000次中断），飞行控制器可能会过载并停止运行。这会影响以下类型的输入：带RPM\_TYPE 1 或 2 的 RPM 传感器、带CAM\_FEEDBACK\_PIN的摄像机反馈、WENC\_TYPE=1 的车轮编码器、BATT\_MONITOR=11 或 12 的液体燃料流量监视器、RFND 类型 5、22 或 30 的 PWM 测距仪、RSSI\_TYPE=4 的 RSSI。 | 升级到版本 4.0.5 | 版本 4.0.5 中已修复 |