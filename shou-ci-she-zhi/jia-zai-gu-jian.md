# 加载固件

## 加载固件

这些说明将向您展示如何将最新固件下载到已安装ArduPilot固件的自动驾驶仪硬件上。此过程将使用任务规划器地面控制站。请参阅[在没有现有 ArduPilot 固件的情况下将固件加载到板上](https://ardupilot.org/copter/docs/common-loading-firmware-onto-chibios-only-boards.html#common-loading-firmware-onto-chibios-only-boards)。

### 将自动驾驶仪连接到计算机

在计算机上[安装地面站](https://ardupilot.org/copter/docs/common-install-gcs.html#common-install-gcs)后，连接 使用 USB 电缆的自动驾驶仪，如图所示 下面。使用计算机上的直接 USB 端口（不是 USB 集线器）。

<figure><img src="https://ardupilot.org/copter/_images/pixhawk_usb_connection.jpg" alt=""><figcaption></figcaption></figure>

像素鹰 USB 连接

Windows 应自动检测并安装正确的驱动程序 软件。

### 选择 COM 端口

如果使用_任务规划器_作为 GCS，请选择窗口右上角“**连接**”按钮附近的 COM 端口下拉列表。选择**“自动”**或主板的特定端口。如图所示，将波特率设置为 **115200**。暂时不要点击**连接**。

<figure><img src="https://ardupilot.org/copter/_images/Pixhawk_ConnectWithMP.png" alt=""><figcaption></figcaption></figure>

### 安装固件

在任务规划器的设置中 **|安装固件**屏幕 选择与您的车辆或车架类型（即四边形、六边形）匹配的适当图标。 **当它**问你“你确定吗？

<figure><img src="https://ardupilot.org/copter/_images/Pixhawk_InstallFirmware.jpg" alt=""><figcaption></figcaption></figure>

任务规划器：安装固件屏幕

任务规划器将尝试检测您正在使用的板。它可能会要求您拔下主板，按 OK，然后重新插入以检测主板类型。

<figure><img src="https://ardupilot.org/copter/_images/Pixhawk_InstallFirmware2.png" alt=""><figcaption></figcaption></figure>

任务规划器：安装固件提示

通常，您会看到一个下拉框，其中包含主板的固件变体，您可以从中进行选择（例如双向 DShot 变体，如果可用）。对于共享 Pixhawk 板 ID 的板，列表将非常广泛，如下所示：

<figure><img src="https://ardupilot.org/copter/_images/pixhawk-firmware.png" alt=""><figcaption></figcaption></figure>

为您的主板选择适当的固件。对于标有“Pixhawk”的主板，Pixhawk1固件通常是最佳选择。

警告

某些标记为 Pixhawk 2.4.x 的主板可能有传感器替换，这可能会导致预布防检查或没有辅助 IMU。请参阅 BARO\_OPTIONS 参数，了解在应使用 MS5607 的 MS5611 气压计的某些主板上更换已知传感器的解决方法。IMU 也可以被替换。在可能的情况下，请从ArduPilot合作伙伴处采购自动驾驶仪。

如果一切顺利，您将在右下角看到一个状态，包括：“擦除...”，“程序...”，“验证..”和“上传完成”。固件已成功上传到主板。

引导加载程序通常需要几秒钟才能在编程或上电后退出并输入主代码。等待按连接，直到发生这种情况。

注意

将固件更新到较新版本不会更改现有参数，除非固件适用于其他车辆，在这种情况下，参数将重置为该车辆的默认值。但是，在进行任何固件更新之前，最好使用任务规划器的“**配置/完整参数树**”选项卡上的“保存到文件”按钮将参数保存到文件中，以防更新时出现任何问题。升级到新版本后，请勿应用所有参数，因为某些参数可能具有不同的含义。

### 使用测试版和开发人员版本

#### 试用版

在发布之前，将发布版本。如果您想尝试较新的功能或帮助开发人员测试新代码，则可以使用这些。由于这些是“测试版”，因此可能仍然存在错误。即使在稳定版固件中也可以这样做。但是，Beta 版本已经过开发团队的测试，并且已经过飞行测试。此版本允许更广泛的用户群在发布为 .我们鼓励有经验的ArduPilot用户试飞此固件并提供反馈。`StableBetaStable`

Mission Planner 在**“安装固件**”页面上有一个选项来上传此版本，但更高版本可能已经可用。请务必先检查正常的车辆上传选项。`Stable`

#### 最新开发者版本

这反映了 ArduPilot 代码开发分支的当前状态。它已经过开发团队的审查，通过了所有自动化测试套件，并且在大多数情况下进行了测试。此代码每天构建，可供有经验的用户测试。这对应于“alpha”版本，并且可能存在错误，尽管很少“导致崩溃”。在添加更改或引入功能的添加后不久，Wiki 的[“即将使用](https://ardupilot.org/copter/docs/common-master-features.html#common-master-features)的功能”部分会更新有关添加或更改的信息。

此代码必须从固件下载页面手动[下载](https://firmware.ardupilot.org/)，然后使用任务规划师在其**安装固件页面上**的“加载自定义固件”选项上传`latest`

#### 自定义固件构建服务器

ArduPilot目前正在实验性地测试一个自定义固件构建服务器，该服务器将允许用户为具有可选功能的自动驾驶仪生成固件构建。由于所有 1MB 闪存大小的电路板现在都有功能限制以允许代码适应，这将提供一个路径，使用户能够选择哪些功能将包含或不包含，从而为 1MB 自动驾驶仪的用户提供一定的灵活性。

服务器位于[此处](https://custom.ardupilot.org/)

它允许创建自定义构建，可以下载，并使用任务规划器在其**安装固件页面上**的“加载自定义固件”选项切换到自动驾驶仪

**固件限制**

* 有关任何给定自动驾驶仪的当前“最新”固件中**不包含**的功能的列表，请参阅[此页面](https://ardupilot.org/copter/docs/binary-features.html#binary-features)。
* 默认情况下，当前**未**包含在 1MB 自动驾驶仪中的所有功能选项都在自定义固件构建服务器上的选项列表中。1MB自动驾驶仪中还包含许多功能，这些功能可能不是您的应用程序需要的。因此，可以创建一个包含一些当前排除的功能，同时删除一些不需要的功能的构建。功能选项列表将不断扩展，允许删除其他大型功能，并将更多受限功能添加到自定义构建中。例如，不包括四平面功能将为不需要它的飞机节省空间。驱动程序和外设支持可以单独选择，只允许代码中曾经使用的驱动程序和外设支持，从而允许在自定义固件中包含其他功能。
* 当前版本仅来自每日主分支（“最新”）。将来，将可以选择稳定版和测试版分支。

### 测试

您可以通过切换到_任务规划器飞行数据_屏幕并按**连接**按钮来测试固件是否在基本级别工作。HUD 应在您倾斜电路板时更新。

[将任务规划器连接到自动驾驶仪具有](https://ardupilot.org/copter/docs/common-connect-mission-planner-autopilot.html#common-connect-mission-planner-autopilot)更多功能 有关连接到任务规划器的信息。
