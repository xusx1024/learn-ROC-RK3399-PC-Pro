# ROC-RK3399-PC-Pro Android 10 经典 ADB 调试命令速查手册

在进行 Android 底层及 Launcher/Framework 调试时，合理使用 ADB 命令行工具能极大提高开发调试效率。以下是整理的高频实用调试命令。

---

### 1. 系统权限与挂载命令 (Root & Remount)
在修改或替换系统分区文件（如 `/system` 或 `/product` 下的 APK、壁纸等）前，必须获得 root 权限并重新挂载分区为可读写模式。
```bash
# 1. 提升 ADB 调试服务的权限为 root 权限
adb root

# 2. 重新挂载系统分区为可读写状态（在 Android 10+ 中会同时挂载 system, product, vendor 等分区）
adb remount
```

---

### 2. 模拟用户输入 (Keyevent Simulation)
使用命令行模拟物理按键或屏幕操作，常用于远程操控和调试自动化。
```bash
# 模拟按下 Home 键（返回主屏幕，常用于唤醒和触发桌面重启）
adb shell input keyevent 3

# 模拟按下 Back 返回键
adb shell input keyevent 4

# 模拟按下 Power 电源键
adb shell input keyevent 26
```

---

### 3. 应用管理命令 (Package Management)
常用于清理缓存、重置桌面数据库、定位 APK 路径等。
```bash
# 1. 清除应用的数据和缓存（常用于重置 Launcher 桌面布局数据库，使其重新加载 XML 配置文件）
adb shell pm clear com.android.launcher3

# 2. 获取指定包名应用的实际 APK 安装路径（常用于确认系统使用的是 Launcher3 还是 Launcher3QuickStep 及其分区位置）
adb shell pm path com.android.launcher3

# 3. 强制停止某个正在运行的应用进程
adb shell am force-stop com.android.launcher3
```

---

### 4. 屏幕与显示属性查看 (Display Properties)
在适配壁纸分辨率或进行 UI 像素密度（DPI）适配时，用于获取屏幕的第一手物理数据。
```bash
# 1. 查看当前连接屏幕的物理分辨率大小（例如输出：Physical size: 1920x1080）
adb shell wm size

# 2. 查看屏幕像素密度/DPI（例如输出：Physical density: 240）
adb shell wm density
```

---

### 5. 系统文件与缓存清理 (System Cache Cleanup)
用于解决系统级修改无法动态刷新（如系统壁纸缓存）的问题。
```bash
# 1. 清理系统在用户目录下生成的默认壁纸缓存（需要先执行 adb root 获取系统保护目录读写权限）
adb shell rm /data/system/users/0/wallpaper*

# 2. 重启开发板以使配置生效
adb shell reboot
```
