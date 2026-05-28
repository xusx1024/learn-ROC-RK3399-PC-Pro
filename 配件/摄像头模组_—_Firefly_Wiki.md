[ROC-RK3399-PC Pro Manual](https://wiki.t-firefly.com/zh_CN/ROC-RK3399-PC-Pro/index.html)

![](https://www.t-firefly.com/upload/portal/20211215/a4cd7652c20fb128c684bf3b08f9f0d1.png)

ROC-RK3399-PC Pro

ROC-RK3399-PC Pro 采用 RK3399 六核(A72x2+A53x4) 64 位处理器，主频高达1.8GHz，集成了四核 Mali-T860 GPU，性能优异。

+   [Docs](https://wiki.t-firefly.com/zh_CN/ROC-RK3399-PC-Pro/index.html) »
+   摄像头模组
+   [View page source](https://wiki.t-firefly.com/zh_CN/ROC-RK3399-PC-Pro/_sources/module_camera.md.txt)

* * *

## 摄像头模组[¶](#she-xiang-tou-mo-zu "永久链接至标题")

## [OV13850 摄像头模组](https://store.t-firefly.com/goods.php?id=6)(已停产)  
[¶](#ov13850-she-xiang-tou-mo-zu-font-color-ff0000-yi-ting-chan-font-br "永久链接至标题")

### 产品参数[¶](#chan-pin-can-shu "永久链接至标题")

+   品牌：Omnivision
    
+   型号：CMK-OV13850
    
+   接口：MIPI
    
+   像素：1320W
    

### 参考固件[¶](#can-kao-gu-jian "永久链接至标题")

+   Android 7.1 公版固件默认支持 CMK-OV13850 摄像头模组
    
+   Android 10.0 公版固件须手动修改DTS
    

#### 10.0 固件修改方法[¶](#gu-jian-xiu-gai-fang-fa "永久链接至标题")

```markdown
--- a/kernel/arch/arm64/boot/dts/rockchip/rk3399-roc-pc-plus.dtsi
+++ b/kernel/arch/arm64/boot/dts/rockchip/rk3399-roc-pc-plus.dtsi
 &i2c1{

-    XC6130b@23{
+    ov13850b@10{
     status = "okay";
     };
-    XC7022b@1b{
+    ov13850f@10{
     status = "okay";
     };

-    /delete-node/ ov13850b@10;
-    /delete-node/ ov13850f@10;
+    /delete-node/ XC6130b@23;
+    /delete-node/ XC7022b@1b;

 };
```

修改以上补丁后重新编译内核并烧写boot.img后重启。

### 实物图[¶](#shi-wu-tu "永久链接至标题")

![_images/module_camera_ov13850-1.jpg](https://wiki.t-firefly.com/zh_CN/ROC-RK3399-PC-Pro/_images/module_camera_ov13850-1.jpg)

![_images/module_camera_ov13850-2.jpg](https://wiki.t-firefly.com/zh_CN/ROC-RK3399-PC-Pro/_images/module_camera_ov13850-2.jpg)

### 连接方法[¶](#lian-jie-fang-fa "永久链接至标题")

![_images/module_camera_connection.jpg](https://wiki.t-firefly.com/zh_CN/ROC-RK3399-PC-Pro/_images/module_camera_connection.jpg)

### 实拍图片[¶](#shi-pai-tu-pian "永久链接至标题")

![_images/module_camera_photographs.png](https://wiki.t-firefly.com/zh_CN/ROC-RK3399-PC-Pro/_images/module_camera_photographs.png)

## [CAM-8MS1M 单目摄像头模组](https://item.taobao.com/item.htm?ft=t&id=659032651408)[¶](#cam-8ms1m-dan-mu-she-xiang-tou-mo-zu "永久链接至标题")

### 产品参数[¶](#id1 "永久链接至标题")

+   **品牌**：SV
    
+   **ISP**：XC7160
    
+   **Sensor**: SC8238
    
+   **接口**: MIPI
    
+   **像素**: 800W(当前仅支持1080P，4K仍在适配中)
    

### 实物图参考[¶](#shi-wu-tu-can-kao "永久链接至标题")

![_images/cam_8ms1m_front.jpg](https://wiki.t-firefly.com/zh_CN/ROC-RK3399-PC-Pro/_images/cam_8ms1m_front.jpg) ![_images/cam_8ms1m_back.jpg](https://wiki.t-firefly.com/zh_CN/ROC-RK3399-PC-Pro/_images/cam_8ms1m_back.jpg)

### 连接方法[¶](#id3 "永久链接至标题")

![_images/camera_8ms1m.jpg](https://wiki.t-firefly.com/zh_CN/ROC-RK3399-PC-Pro/_images/camera_8ms1m.jpg)

### 实拍图片[¶](#id4 "永久链接至标题")

![_images/camera_8ms1m_shoot.jpg](https://wiki.t-firefly.com/zh_CN/ROC-RK3399-PC-Pro/_images/camera_8ms1m_shoot.jpg)

## SV-TAYSH-TQ摄像头模组[¶](#sv-taysh-tq-she-xiang-tou-mo-zu "永久链接至标题")

### 产品参数[¶](#id5 "永久链接至标题")

+   型号：XC7022(RGB)/XC6130(IR)
    
+   接口：MIPI
    
+   像素：200W
    

### 修改方法 (手动修改)[¶](#xiu-gai-fang-fa-shou-dong-xiu-gai "永久链接至标题")

「 Android 7.1 」device/rockchip/rk3399/rk3399\_roc\_pc\_plus.mk

```
 BOARD_NFC_SUPPORT := false
 BOARD_HAS_GPS := false
+BOARD_XC7022_XC6130_SUPPORT := true

 #for 3G/4G modem dongle support
 BOARD_HAVE_DONGLE := false
```

修改上述补丁后重新 [编译Android](https://wiki.t-firefly.com/zh_CN/ROC-RK3399-PC-Pro/compile_android7.1_industry_firmware.html#zheng-ti-bian-yi)并烧写 system.img 后重启。

「 Android 10 」kernel/arch/arm64/boot/dts/rockchip/rk3399-roc-pc-plus.dtsi

```
    xc7160b@1b{
+    status = "disabled";
    };
    xc7160f@1b{
+    status = "disabled";
    };

    XC6130b@23{
+    status = "okay";
    };
    XC7022b@1b{
+    status = "okay";
    };
```

修改上述补丁后重新[编译内核](https://wiki.t-firefly.com/zh_CN/ROC-RK3399-PC-Pro/compile_android10.0_firmware.html#fen-bu-bian-yi)并烧写 boot.img 后重启。

### 实物图[¶](#id6 "永久链接至标题")

![_images/camera_SV-TAYSH-TQ.jpg](https://wiki.t-firefly.com/zh_CN/ROC-RK3399-PC-Pro/_images/camera_SV-TAYSH-TQ.jpg)

### 连接方式[¶](#lian-jie-fang-shi "永久链接至标题")

![_images/camera_SV-TAYSH-TQ_connect.jpg](https://wiki.t-firefly.com/zh_CN/ROC-RK3399-PC-Pro/_images/camera_SV-TAYSH-TQ_connect.jpg)

### 实拍图片[¶](#id7 "永久链接至标题")

![_images/camera_SV-TAYSH-TQ_shoot.png](https://wiki.t-firefly.com/zh_CN/ROC-RK3399-PC-Pro/_images/camera_SV-TAYSH-TQ_shoot.png)