# copypath

右键复制文件/文件夹绝对路径的 Nautilus 脚本。
单文件、零配置，已在 Ubuntu 22.04（GNOME 42 / Nautilus 42 / X11）实测。

## 用法

文件管理器里**右键文件/文件夹 → Scripts(脚本) → Copy Path**。
多选文件则逐行复制多个路径。

## 安装 / 卸载

```bash
sudo apt install xclip # 依赖
./copypath install     # 在 ~/.local/share/nautilus/scripts/ 建硬链接
nautilus -q            # 重启文件管理器，右键出现"脚本 → Copy Path"
./copypath uninstall   # 删硬链接即完全卸载
```
