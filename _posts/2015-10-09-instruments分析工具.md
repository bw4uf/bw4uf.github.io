#Instruments分析工具

    要点：这是一篇关于API或者开发技术的基础文档。苹果提供这些信息来帮助读者
    
附录里提供了关于Instruments分析工具的简要介绍来帮助读者理解[Best Practices for Developing Cellular Apps](developer.apple.com/library/prerelease/ios/documentation/Performance/Conceptual/CellularBestPractices/BestPractices/BestPractices.html#//apple_ref/doc/uid/TP40013998-CH3-SW1)这篇文档所描述的最好的实践中的数据展示。

##Instruments的主要特点
Instruments是Xcode开发者工具的一种，收录在Open Developer Tools菜单中。这篇附录表述了你可以如何使用Instruments分析工具通过检查app的网络以及在设备上的效率来监测问题区域。

尽管Instruments广泛被多数iPhone开发者熟知，但仍值得我们回顾一些测试网络app很重要的特点:

* 使用方便
* 方便快速找出问题和异常值，而不需要学习关于数据管道机制的诸多细节知识
* 识别出设备端还是网络断的影响
* 测出消耗秒级的数据或者是数天时间的日志
* 在任何时间段都能提供合适的粒度
* 使用工具对设备和app行为都几乎没有影响

Instruments分析工具包含了一套的单个仪表，你可以用它们来识别网络活动中不正常的部分。Connections工具和App Profiling工具对识别低效率app可能引起的网络问题类型尤为有效。

关于Instruments用户界面的概述可以在[Instruments User Guide](developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/InstrumentsUserGuide/)的[Touring Instruments](developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/InstrumentsUserGuide/UsingtheTraceDocument/UsingtheTraceDocument.html)中查看。

在如下图A-1中，图的上半部分是轨道窗口，中间是导航栏，下半部分是细节窗口。

![](https://developer.apple.com/library/prerelease/ios/documentation/Performance/Conceptual/CellularBestPractices/Art/cbp_tour_instruments_ui_2x.png)

这篇文档并不是要写成一篇使用Instruments工具的教程，而是让你对Instruments有所了解以能够理解[Best Practices for Developing Celluar Apps]()中的案例展示。

##快速浏览Instruments视图
Connections仪表展示了开发者应当很熟悉的一些活动。它包含了三个视图：Interfaces，Connections和Processes。

##Interfaces视图
Connections工具的界面视图(图A-2)监测蜂窝网络和Wi-Fi接口的通信情况。

![](https://developer.apple.com/library/prerelease/ios/documentation/Performance/Conceptual/CellularBestPractices/Art/CBP_Tour_Interfaces_2x.png)

Interfaces的细节窗口展示了标准化参数以及每个接口的其他细节。当你选中一个接口后，轨道窗口就会随着时间展示数据量。
##Connections视图
当app触发它们，Connections工具的连接视图(图A-3)会监测所有的TCP和UDP连接。

![](https://developer.apple.com/library/prerelease/ios/documentation/Performance/Conceptual/CellularBestPractices/Art/cbp_tour_connections_2x.png)































