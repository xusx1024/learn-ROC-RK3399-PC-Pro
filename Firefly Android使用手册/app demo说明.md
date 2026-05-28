+   [Docs](https://wiki.t-firefly.com/zh_CN/Firefly-Android-Manual/index.html) »
+   1\. 概述
+   [View page source](https://wiki.t-firefly.com/zh_CN/Firefly-Android-Manual/_sources/app_demo.md.txt)

* * *

## 1\. 概述[¶](#gai-shu "永久链接至标题")

App Demo 一般内置在固件里，对于不同的设备，内置的 App Demo 会有些区别，具体以实际设备烧录的固件为准。

## 2\. FireflyDemo[¶](#fireflydemo "永久链接至标题")

FireflyDemo 应用可快速确认 Firefly 平台系列产品支持的解码路数，并支持本地和 rtsp 播放流播放。

详细参考[高效确认视频解码路数](http://www.t-firefly.com/doc/case/443.html)。

**NOTE:** 支持Firefly全系列产品

## 3\. firefly\_sdkapi\_demo[¶](#firefly-sdkapi-demo "永久链接至标题")

详细参考[FIREFLYAPI 说明](https://wiki.t-firefly.com/zh_CN/Firefly-Android-Manual/firefly_api.html)。

**NOTE:** 仅支持Android 7.1/Android10

## 4\. Rmsl3DCameraIQCTest[¶](#rmsl3dcameraiqctest "永久链接至标题")

用于 RMSL201-1301 结构光模组的老化测试。

详细参考[RMSL201-1301结构光模组](http://wiki.t-firefly.com/Face-RK3399/module_camera.html#rmsl201-1301-jie-gou-guang-mo-zu)。

**NOTE:** 仅支持Android 7.1/Android10

## 5\. RmslPreview[¶](#rmslpreview "永久链接至标题")

供 Rmsl3DCameraIQCTest 调用

详细参考[RMSL201-1301结构光模组](http://wiki.t-firefly.com/Face-RK3399/module_camera.html#rmsl201-1301-jie-gou-guang-mo-zu)。

**NOTE:** 仅支持Android 7.1/Android10

## 6\. CAEDemo[¶](#caedemo "永久链接至标题")

Firefly 智能语音套件支持科大讯飞 AIUI 云服务，通过 CAEDemo 程序在智能语音套件上实现语音识别、关键词唤醒、降噪、回声消除等示范功能。

详细参考[智能语音CAEDemo程序](http://www.t-firefly.com/doc/case/452.html)。

**NOTE:** 仅支持Android 7.1/Android10

## 7\. HDMI IN[¶](#hdmi-in "永久链接至标题")

HDMI IN 功能，RK3399和RK3288主要作用是采集 HDMI IN 过来的信号转换为 MIPI 信号给主控，其数据格式是 YUV422 8bit。 如下格式中 I 表示交错式扫描显示方式，P 表示逐行扫描显示方式。

+   RK3399 HDMI IN 输入分辨率支持列表
    
    +   640X480 P
        
    +   720X480 I/P
        
    +   720X576 I/P
        
    +   1280X720 P
        
    +   1920X1080 I/P
        

**NOTE:** 支持Android 7.1

+   RK3288 HDMI IN 输入分辨率支持列表
    
    +   1280X720 P
        
    +   1920X1080 P
        

**NOTE:** 支持Android 5.1

+   [RK3588 HDMI IN 支持格式和使用方式](https://wiki.t-firefly.com/zh_CN/Core-3588J/usage_hdmiin.html)
    

## 8\. ScheduleOnOff[¶](#scheduleonoff "永久链接至标题")

定时开关机演示APK。

**NOTE:** 固件默认内置，如果没有，请联系商务`sales@t-firefly.com`。