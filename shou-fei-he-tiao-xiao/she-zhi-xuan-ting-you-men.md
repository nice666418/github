# 设置悬停油门

Copter包括悬停油门的自动学习（以前称为“中油门”） 每当飞行器在非手动飞行模式（即除稳定和 Acro 之外的所有模式）中保持稳定悬停时，[MOT\_THST\_HOVER](https://ardupilot.org/copter/docs/parameters.html#mot-thst-hover)值将缓慢向平均电机输出移动。

如果要手动设置[MOT\_THST\_HOVER](https://ardupilot.org/copter/docs/parameters.html#mot-thst-hover)值，最好下载数据闪存日志并将该值设置为CTUN中显示的值。ThO 字段。该值应介于 0.2 和 0.8 之间。

如果出于某种原因您希望禁用学习，则可以将 [MOT\_HOVER\_LEARN](https://ardupilot.org/copter/docs/parameters.html#mot-hover-learn) 参数设置为 0。

<figure><img src="https://ardupilot.org/copter/_images/throttle_mid_learning.png" alt=""><figcaption></figcaption></figure>
