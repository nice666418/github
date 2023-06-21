# EKF Affinity & Lane Switch

## EKF3 亲和力和通道切换[¶](https://ardupilot.org/copter/docs/common-ek3-affinity-lane-switching.html#ekf3-affinity-and-lane-switching)

[EKF](https://ardupilot.org/dev/docs/extended-kalman-filter.html#extended-kalman-filter) 实例化名为“通道”的筛选器的多个实例。主车道是提供状态估计的车道，其余车道在后台更新并可供切换。可能的通道数与启用使用的 IMU 数完全相等。通常，每条车道都使用空速、气压计、GPS 和磁力计传感器的主要实例。主传感器可以设置为用户可修改的参数，但以后可以由系统更改，即使在飞行中，以防发生驾驶员级故障。然而，众所周知，现代车辆安装了多个高质量的传感器。亲和力是 EKF 车道在任何运行车道内使用非主传感器的一种方式。这提供了一种统计上一致的方法来利用多个高质量传感器，并使用通道切换来选择具有最佳性能传感器组合的通道。车道误差分数考虑了车道使用的所有传感器的创新。这样，也可以使用嘈杂的非IMU传感器使车辆免于事故。

**具有 1 个气压计、2 个 GPS、2 个空速、3 个磁力计和 3 个 IMU 的车辆的亲和配置的简单示例 -**

| 车道     | 1 | 2 | 3 |
| ------ | - | - | - |
| 空速     | 1 | 2 | 1 |
| 晴雨表    | 1 | 1 | 1 |
| 全球定位系统 | 1 | 2 | 1 |
| 磁力计    | 1 | 2 | 3 |

_数字是相应的传感器实例_

### 配置参数[¶](https://ardupilot.org/copter/docs/common-ek3-affinity-lane-switching.html#configuration-parameters)

注意

关联仅适用于 EKF3，因此请确保通过确保[EK3\_ENABLE](https://ardupilot.org/copter/docs/parameters.html#ek3-enable)设置为“1”且[AHRS\_EKF\_TYPE](https://ardupilot.org/copter/docs/parameters.html#ahrs-ekf-type)设置为“3”来使用它

[EK3\_AFFINITY](https://ardupilot.org/copter/docs/parameters.html#ek3-affinity)参数是一个位掩码，它使您可以选择要为其启用关联关系的传感器。未启用将遵循默认的主传感器分配。

[EK3\_ERR\_THRESH](https://ardupilot.org/copter/docs/parameters.html#ek3-err-thresh)参数控制车道切换的灵敏度。车道误差是相对于活动主车道随时间累积的。此阈值控制非主通道和主通道之间需要多少误差差异才能认为前者性能更好。降低此参数可使车道切换对较小的“相对”错误更灵敏，实际上您会看到更积极的车道切换，反之亦然。

警告

错误配置[EK3\_ERR\_THRESH](https://ardupilot.org/copter/docs/parameters.html#ek3-err-thresh)参数可能会对车道切换机构产生不利影响，并产生严重后果，可能导致车辆损失。请仔细调整。

### 测试结果[¶](https://ardupilot.org/copter/docs/common-ek3-affinity-lane-switching.html#test-results)

以下图表来自 SITL 测试，显示当主通道的传感器受到噪音/故障影响时，启用了亲和力的车道变换。

#### 空速[¶](https://ardupilot.org/copter/docs/common-ek3-affinity-lane-switching.html#airspeed)

启用了 2 个空速传感器并启用了空速关联性的飞机的车道切换示例。有 2 个 IMU，因此有 2 个活动通道。主车道的空速传感器未能显示压力变化，因此报告了一个恒定值。飞机的速度增加并发生车道切换。同样，第二车道（现在是主车道）的第二个空速传感器发生故障，飞机的速度降低，再次触发车道切换。

![../\_images/airspeed\_affinity.png](https://ardupilot.org/copter/\_images/airspeed\_affinity.png)

#### 晴雨表[¶](https://ardupilot.org/copter/docs/common-ek3-affinity-lane-switching.html#barometer)

启用了 2 个气压计和气压计亲和力的飞机的车道切换示例。有 2 个 IMU，因此有 2 个活动通道。主车道的气压计未能显示压力变化，因此报告了一个恒定值。飞机的高度增加并发生车道切换。同样，第二条车道（现在是主车道）的第二个气压计出现故障，飞机的高度降低，再次触发车道切换。

![../\_images/barometer\_affinity.png](https://ardupilot.org/copter/\_images/barometer\_affinity.png)

#### 全球定位系统[¶](https://ardupilot.org/copter/docs/common-ek3-affinity-lane-switching.html#gps)

启用了 2 个 GPS 和 GPS 关联性的飞机的车道切换示例。有 2 个 IMU，因此有 2 个活动通道。主车道的 GPS 使用所有 2 轴范围为 ±3m 的随机 GPS 速度噪声进行模拟。实际速度可以用第二个GPS跟踪。随后，EKF 主通道开始报告持续高误差，当误差超过设定阈值时发生通道切换。

![../\_images/gps\_affinity.png](https://ardupilot.org/copter/\_images/gps\_affinity.png)

#### 磁力计[¶](https://ardupilot.org/copter/docs/common-ek3-affinity-lane-switching.html#magnetometer)

启用了 2 个磁力计和磁力计亲和力的飞机的车道切换示例。有 2 个 IMU，因此有 2 个活动通道。通过在飞行时更改 z 轴的偏移量，在主车道的磁力计中模拟误差。偏移变化可以用第二个磁力计跟踪。随后，EKF 主通道开始报告持续高误差，当误差超过设定阈值时发生通道切换。

![../\_images/mag\_affinity.png](https://ardupilot.org/copter/\_images/mag\_affinity.png)
