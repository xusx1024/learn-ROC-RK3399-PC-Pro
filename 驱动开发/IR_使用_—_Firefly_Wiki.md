[ROC-RK3399-PC Pro Manual](https://wiki.t-firefly.com/zh_CN/ROC-RK3399-PC-Pro/index.html)

![](https://www.t-firefly.com/upload/portal/20211215/a4cd7652c20fb128c684bf3b08f9f0d1.png)

ROC-RK3399-PC Pro

ROC-RK3399-PC Pro 采用 RK3399 六核(A72x2+A53x4) 64 位处理器，主频高达1.8GHz，集成了四核 Mali-T860 GPU，性能优异。

+   [Docs](https://wiki.t-firefly.com/zh_CN/ROC-RK3399-PC-Pro/index.html) »
+   IR 使用
+   [View page source](https://wiki.t-firefly.com/zh_CN/ROC-RK3399-PC-Pro/_sources/driver_ir.md.txt)

* * *

## IR 使用[¶](#ir-shi-yong "永久链接至标题")

## 红外遥控配置[¶](#hong-wai-yao-kong-pei-zhi "永久链接至标题")

其配置步骤可分为两个部分：

+   修改内核驱动：内核空间修改，Linux 和 Android 都要修改这部分的内容。
    
+   修改键值映射：用户空间修改（仅限 Android 系统）。
    

## 内核驱动[¶](#nei-he-qu-dong "永久链接至标题")

在 Linux 内核中，IR 驱动仅支持 NEC 编码格式。以下是在内核中配置红外遥控的方法。

所涉及到的文件：

```
kernel/arch/arm64/boot/dts/rockchip/rk3399-firefly-port.dtsi
kernel/drivers/input/remotectl/rockchip_pwm_remotectl.c
```

### 定义相关数据结构[¶](#ding-yi-xiang-guan-shu-ju-jie-gou "永久链接至标题")

添加键值表结构体数组和配置对应如下：

```
&pwm3 {
    status = "okay";
    interrupts = ;
    compatible = "rockchip,remotectl-pwm";
    remote_pwm_id = ;
    handle_cpu_id = ;
    ir_key1{
    rockchip,usercode = ;
    rockchip,key_table = {
         {0xeb, KEY_POWER},        // Power
         //Control
         {0xa3, 250},              // Settings
         {0xec, KEY_MENU},         // Menu
         {0xfc, KEY_UP},           // Up
         {0xfd, KEY_DOWN},         // Down
         {0xf1, KEY_LEFT},         // Left
         {0xe5, KEY_RIGHT},        // Right
         {0xf8, KEY_REPLY},        // Ok
         {0xb7, KEY_HOME},         // Home
         {0xfe, KEY_BACK},         // Back
         // Vol
         {0xa7, KEY_VOLUMEDOWN},   // Vol-
         {0xf4, KEY_VOLUMEUP},     // Vol+
   };
```

注：第一列为键值，第二列为要响应的按键码。

### 如何获取用户码和IR 键值[¶](#ru-he-huo-qu-yong-hu-ma-he-ir-jian-zhi "永久链接至标题")

在 remotectl\_do\_something 函数中获取用户码和键值：

```html
    case RMC_USERCODE:
        {
            //ddata->scanData <<= 1;
            //ddata->count ++;
            if ((RK_PWM_TIME_BIT1_MIN < ddata->period) && (ddata->period < RK_PWM_TIME_BIT1_MAX)){
                ddata->scanData |= (0x01<<ddata->count);;
            }
            ddata->count ++;
            if (ddata->count == 0x10){//16 bit user code
                DBG_CODE("GET USERCODE=0x%x\n",((ddata->scanData) & 0xffff));
                if (remotectl_keybdNum_lookup(ddata)){
                    ddata->state = RMC_GETDATA;
                    ddata->scanData = 0;
                    ddata->count = 0;
                }else{                //user code error
                    ddata->state = RMC_PRELOAD;
                }
            }
        }
```

注：用户可以使用 `DBG_CODE()` 函数打印用户码。

使用下面命令可以使能 DBG\_CODE 打印：

```bash
echo 1 > /sys/module/rockchip_pwm_remotectl/parameters/code_print
```

### 将 IR 驱动编译进内核[¶](#jiang-ir-qu-dong-bian-yi-jin-nei-he "永久链接至标题")

将 IR 驱动编译进内核的步骤如下所示：

(1)、向配置文件 `kernel/drivers/input/remotectl/Kconfig` 中添加如下配置：

```
config ROCKCHIP_REMOTECTL_PWM
        bool "rockchip remoctrl pwm capture"
        default n
```

(2)、修改 `kernel/drivers/input/remotectl/Makefile` 文件,添加如下编译选项：

```
obj-$(CONFIG_ROCKCHIP_REMOTECTL_PWM)    += rockchip_pwm_remotectl.o
```

(3)、在 kernel 路径下使用 make menuconfig ，按照如下方法将 IR 驱动选中。

```
Device Drivers
  --->Input device support
  ----->  [*]   rockchip remotectl
  ------->[*]   rockchip remoctrl pwm capture
```

保存后，执行 `make` 命令即可将该驱动编进内核。

### Android 键值映射[¶](#android-jian-zhi-ying-she "永久链接至标题")

文件 `/system/usr/keylayout/ff420030_pwm.kl` 用于将 Linux 层获取的键值映射到 Android 上对应的键值。用户可以添加或者修改该文件的内容以实现不同的键值映射。

该文件内容如下所示：

```
key 28    ENTER
key 116   POWER             WAKE
key 158   BACK
key 139   MENU
key 217   SEARCH
key 232   DPAD_CENTER
key 108   DPAD_DOWN
key 103   DPAD_UP
key 102   HOME
key 105   DPAD_LEFT
key 106   DPAD_RIGHT
key 115   VOLUME_UP
key 114   VOLUME_DOWN
key 143   NOTIFICATION      WAKE
key 113   VOLUME_MUTE
key 388   TV_KEYMOUSE_MODE_SWITCH
key 400   TV_MEDIA_MULT_BACKWARD
key 401   TV_MEDIA_MULT_FORWARD
key 402   TV_MEDIA_PLAY_PAUSE
key 64    TV_MEDIA_PLAY
key 65    TV_MEDIA_PAUSE
key 66    TV_MEDIA_STOP
```

注：通过 ADB 修改该文件重启后即可生效。

## IR 使用[¶](#id1 "永久链接至标题")

如下图是通过按红外遥控器按钮，所产生的波形，主要由 head, Control, information, signed free 这四部分组成，具体可以参考 RC6 Protocol。

![_images/ir.jpg](https://wiki.t-firefly.com/zh_CN/ROC-RK3399-PC-Pro/_images/ir.jpg)