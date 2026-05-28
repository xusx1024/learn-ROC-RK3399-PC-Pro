[ROC-RK3399-PC Pro Manual](https://wiki.t-firefly.com/zh_CN/ROC-RK3399-PC-Pro/index.html)

![](https://www.t-firefly.com/upload/portal/20211215/a4cd7652c20fb128c684bf3b08f9f0d1.png)

ROC-RK3399-PC Pro

ROC-RK3399-PC Pro 采用 RK3399 六核(A72x2+A53x4) 64 位处理器，主频高达1.8GHz，集成了四核 Mali-T860 GPU，性能优异。

+   [Docs](https://wiki.t-firefly.com/zh_CN/ROC-RK3399-PC-Pro/index.html) »
+   定时器使用
+   [View page source](https://wiki.t-firefly.com/zh_CN/ROC-RK3399-PC-Pro/_sources/driver_timer.md.txt)

* * *

## 定时器使用[¶](#ding-shi-qi-shi-yong "永久链接至标题")

## 前言[¶](#qian-yan "永久链接至标题")

RK3399有 12 个 Timers (timer0-timer11)，有 12 个 Secure Timers(stimer0~stimer11) 和 2 个 Timers(pmutimer0~pmutimer1)， 我们主要用到的是 Timers(timer0-timer11) 时钟频率为 24MHZ ，工作模式有 `free-running` 和 `user-defined count` 模式。

## 框架图[¶](#kuang-jia-tu "永久链接至标题")

![_images/timer_frame.jpg](https://wiki.t-firefly.com/zh_CN/ROC-RK3399-PC-Pro/_images/timer_frame.jpg)

## 工作模式[¶](#gong-zuo-mo-shi "永久链接至标题")

+   `user-defined count`：Timer 先载入初始值到 TIMERn\_LOAD\_COUNT3 和 TIMER\_LOADn\_COUNT2 寄存器， 当时间累加的值在寄存器 TIMERn\_LOAD\_COUNT1 和 TIMERn\_LOAD\_COUNT0 时，将不会自动载入到计数寄存器。 用户需要重新关闭计数器和然后重新设置计数器相关才能继续工作。
    
+   `free-running`：Timer 先载入初始值到 TIMER\_LOAD\_COUNT3 和 TIMER\_LOAD\_COUNT2 寄存器， 当时间累加的值在寄存器 TIMERn\_LOAD\_COUNT1 和 TIMERn\_LOAD\_COUNT0 时，Timer 将一直自动加载计数寄存器。
    

## 软件配置[¶](#ruan-jian-pei-zhi "永久链接至标题")

1.在 dts 文件中定义 Timer 的相关配置 `kernel/arch/arm64/boot/dts/rockchip/rk3399.dtsi`

```html
rktimer: rktimer@ff850000 {
	compatible = "rockchip,rk3399-timer";
	reg = <0x0 0xff850000 0x0 0x1000>;
	interrupts = <GIC_SPI 81 IRQ_TYPE_LEVEL_HIGH 0>;
	clocks = <&cru PCLK_TIMER0>, <&cru SCLK_TIMER00>;
	clock-names = "pclk", "timer";
};
```

其中定义的 Timer0 的寄存器和中断号和时钟等。

其他 Timer 对应的中断号可看如下图片：

![_images/timer_interrupt.jpg](https://wiki.t-firefly.com/zh_CN/ROC-RK3399-PC-Pro/_images/timer_interrupt.jpg)

2.对应的驱动文件 `Kernel/drivers/clocksource/rockchip_timer.c`

## 对应寄存器和使用[¶](#dui-ying-ji-cun-qi-he-shi-yong "永久链接至标题")

1.  寄存器如下图片：
    

![_images/timer_register.jpg](https://wiki.t-firefly.com/zh_CN/ROC-RK3399-PC-Pro/_images/timer_register.jpg)

1.  使用 `io` 命令方式查看对应寄存器：
    

```
root@host_name:/ # io -4 0xff85001c  //查看当前控制寄存器的状态
ff85001c:  00000007

root@host_name:/ # io -4 0xff850000  //查看寄存器时时的值
ff850000:  0001639f
```

控制对应寄存器：

```
root@host_name:/ # io -4 -w 0xff85001c 0x06  //关闭时间计数功能
```