# 代工定制

## 代工定制[¶](https://ardupilot.org/copter/docs/common-oem-customizations.html#oem-customization)

ArduPilot 为 OEM 提供了几种方法，可以在其产品上提供针对其特定系统配置定制的固件：

* 能够为参数设置特定的默认值，以匹配包含的系统组件（如万向节）或整个系统的外围设备（如在准备飞行的车辆中）。这允许用户使用Mission Planner或MAVProxy“重置为默认值”，以防意外更改参数的问题，并且最多只需重新校准指南针/ IMU /和RC即可准备飞行。
* 能够在ROM中为特殊功能提供Lua脚本，而无需最终用户将其加载到SD卡上。[在此处](https://ardupilot.org/copter/docs/common-lua-scripts.html#common-lua-scripts)阅读有关 ArduPilot 中 Lua 脚本的更多信息。
* 能够更改向用户显示的固件字符串。
* 能够在可用的可用闪存空间中包含图片和信息文件。
* 能够更改参数并将其标记为只读，以便用户无法使用 [APJ 工具](https://ardupilot.org/dev/docs/apjtools-intro.html#apjtools-intro)更改它们。

### 自定义步骤[¶](https://ardupilot.org/copter/docs/common-oem-customizations.html#customization-steps)

本节假设 OEM 已设置构建环境（构建代码）并在本地克隆 ArduPilot GitHub 存储库（[下载代码/使用 Git](https://ardupilot.org/dev/docs/where-to-get-the-code.html#where-to-get-the-code)），以[构建](https://ardupilot.org/dev/docs/building-the-code.html#building-the-code)其自定义版本的固件。

1.  使用您希望基于自定义的固件版本创建一个分支。这通常是当前的稳定版本。例如，要为 ArduPlane Stable 执行此操作，假设您已经在 PC 上的 ArduPilot 目录中：

    > ```
    > git fetch https://github.com/ArduPilot/ardupilot.git <version>
    >                     where <version> is the tag for the stable version for the
    >                     desired vehicle: ArduPlane-stable, ArduCopter-stable,
    >                     APMrover2-stable,etc.
    >
    > git checkout -b <your branch name> FETCH_HEAD
    > git submodule update --init --recursive
    > ```
2. 在目录中，为自定义板定义创建新的子目录。在此示例中，将命名目录以创建该板的衍生产品。`libraries/AP_HAL_ChibiOS/hwdefOEM_CubeOrange`
3.  创建此格式的新文件。在这种情况下，我们的准备飞行的飞机将使用CubeOrange自动驾驶仪，只需要一条线：`hwdef.dat`

    > ```
    > include ../CubeOrange/hwdef.dat
    > ```
4.  可以通过向文件添加一行来自定义固件名称。`hwdef.dat`

    > ```
    > define AP_CUSTOM_FIRMWARE_STRING "MyMagicFrame"
    > ```
    >
    > 注意
    >
    > 自定义帧类型字符串可以通过Lua脚本方法创建。`motors:set_frame_string("Custom frame name")`
5.  现在在同一目录中，复制基板的引导加载程序文件，然后包含一个名为 的文件。此文件将是标准默认值的参数覆盖，以匹配系统的配置。诸如输出功能分配、辅助 RC 开关、飞行和调谐参数等。`hwdef_bl.datdefaults.parm`

    > 警告
    >
    > 文件应尽可能小。某些主板只允许此文件总共 1024 字节。文件中的每个 ASCII 字节都计入此限制（注释行除外）。尽可能使用整数值。下面是一个简单的例子。串行端口protcols，波特率和选项defaultscan直接在hwdef中设置，以及NTF\_LED\_TYPES和电池监视器默认值，并且应该在那里完成，而不是默认文件。`defaults.parm`
    >
    > ```
    > # setup for NTF LEDs on output5
    > SERVO5_FUNCTION 120
    > NTF_LED_TYPES 256
    > ```
6.  您还可以在将自动运行的芯片的ROM中嵌入[Lua脚本](https://ardupilot.org/copter/docs/common-lua-scripts.html#common-lua-scripts)。由于Lua目前仅在具有大量闪存空间的自动驾驶仪上运行，因此它们的总总大小仅限于可用的可用闪存。将脚本放在名为 的子目录中，即 。文件必须以 结尾。`scriptslibraries/AP_HAL_ChibiOS/hwdef/OEM_CubeOrange/scripts.lua`

    > 警告
    >
    > 用户还可以从 SD 卡上运行 Lua 脚本，因此在命名嵌入式脚本文件名时应小心，以免与潜在的用户文件名冲突。建议在产品文档中为用户提供嵌入式 Lua 脚本的文件名。
7. 您还可以在芯片的 ROM 中嵌入小块文档，这些文档在通过 MAVFtp 检查@ROMFS文件夹时是可读的。这些可以是图片或小型信息文档。这些必须适合自动驾驶仪的自由闪光空间。这些文件可以位于 （例如 ） 中的子目录中。`libraries/AP_HAL_ChibiOS/hwdef/OEM_CubeOrangelibraries/AP_HAL_ChibiOS/hwdef/OEM_CubeOrange/AircraftManual`
8. 现在，使用OEM-CubeOrange作为配置中的板名进行正常构建。默认参数、Lua 脚本和自定义固件名称将适当嵌入。

#### 自定义 hwdef 的替代方法.dat[¶](https://ardupilot.org/copter/docs/common-oem-customizations.html#alternative-to-customizing-hwdef-dat)

除了创建单独的分支并修改 hwdef 文件之外，您还可以将 Lua 脚本甚至信息文件插入到构建的 ROMFS 中。只需转到本地 ardupilot 存储库的“build”文件夹并创建一个名为“ROMFS\_custom”的子文件夹。将 LUA 脚本放在此目录中名为“scripts”（即路径）的子文件夹中。您可以为信息文件使用其他子文件夹，在使用 MAVFtp 检查@ROMFS文件夹时，这些子文件夹将包含在内并可查看。`ardupilot/build/ROMFS_custom/scripts`
