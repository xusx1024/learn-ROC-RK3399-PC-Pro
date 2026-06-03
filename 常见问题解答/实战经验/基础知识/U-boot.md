U-Boot (Universal Boot Loader)

主要作用是生成设备的**“引导程序”**

U-Boot 扮演的角色就相当于我们普通电脑主板上的 BIOS 或 UEFI。它是系统上电后运行的第一段软件代码。

任务:
1. 初始化核心硬件
刚通电时，板子上的 CPU、内存（DDR）、时钟等都处于未就绪状态。U-Boot 的首要任务就是把最核心的硬件跑起来。如果你更换了内存颗粒、改了时钟频率，就需要修改 U-Boot 源码并重新编译。
2. 加载内核 (Kernel) 与 Android 系统
U-Boot 负责将存放在 eMMC 或 SD 卡里的 Linux/Android 内核（Kernel）读取到内存中，并将设备树（Device Tree）等关键参数传递给内核，然后把系统的控制权交给内核，从而真正把 Android 系统拉扯启动起来。
3. 提供烧写和调试模式
对于 Android 开发板，U-Boot 还提供了多种启动模式。比如长按某个按键进入 Loader 模式、MaskROM 模式或 Fastboot 模式。这些模式允许你通过 USB 线连接电脑，向主板的各个分区重新烧录固件（也就是烧写 update.img 或各个分区的 .img 文件）。