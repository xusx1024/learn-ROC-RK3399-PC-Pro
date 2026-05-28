[ROC-RK3399-PC Pro Manual](https://wiki.t-firefly.com/zh_CN/ROC-RK3399-PC-Pro/index.html)

![](https://www.t-firefly.com/upload/portal/20211215/a4cd7652c20fb128c684bf3b08f9f0d1.png)

ROC-RK3399-PC Pro

ROC-RK3399-PC Pro 采用 RK3399 六核(A72x2+A53x4) 64 位处理器，主频高达1.8GHz，集成了四核 Mali-T860 GPU，性能优异。

+   [Docs](https://wiki.t-firefly.com/zh_CN/ROC-RK3399-PC-Pro/index.html) »
+   屏幕模组
+   [View page source](https://wiki.t-firefly.com/zh_CN/ROC-RK3399-PC-Pro/_sources/module_display.md.txt)

* * *

## 屏幕模组[¶](#ping-mu-mo-zu "永久链接至标题")

## [DM-M10R800V2 MIPI 屏模组](https://item.taobao.com/item.htm?ft=t&id=655100190974)[¶](#dm-m10r800v2-mipi-ping-mo-zu "永久链接至标题")

### 产品参数[¶](#chan-pin-can-shu "永久链接至标题")

+   型号：M101014\_BE45\_A1
    
+   尺寸：10.1 寸
    
+   分辨率：800x1280
    
+   显示接口：MIPI
    
+   可视角度：160°
    
+   触摸屏：多点电容触摸
    

### 参考固件[¶](#can-kao-gu-jian "永久链接至标题")

**注意：** 支持 10.1 寸 MIPI 屏的官方固件名带有 `MIPI` 字样，下面是固件的链接：

+   [下载](https://www.t-firefly.com/doc/download/125.html)
    

### 编译命令[¶](#bian-yi-ming-ling "永久链接至标题")

+   Android 7.1
    

```
./FFTools/make.sh -j8 -d rk3399-roc-pc-plus-mipi101-JDM101014_BC45_A1 -l rk3399_roc_pc_plus_mipi101-userdebug
./FFTools/mkupdate/mkupdate.sh -l rk3399_roc_pc_plus_mipi101-userdebug
```

+   Android 10.0
    

```
./FFTools/make.sh -j8 -d rk3399-roc-pc-plus-mipi101-JDM101014_BC45_A1 -l rk3399_roc_pc_plus_mipi-userdebug
./FFTools/mkupdate/mkupdate.sh -l rk3399_roc_pc_plus_mipi-userdebug
```

### 实物图[¶](#shi-wu-tu "永久链接至标题")

![_images/panel_mipi101.jpg](https://wiki.t-firefly.com/zh_CN/ROC-RK3399-PC-Pro/_images/panel_mipi101.jpg)