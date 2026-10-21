# copypath

右键复制文件/文件夹绝对路径的 Nautilus 脚本。
单文件、零配置，已在 Ubuntu 22.04（GNOME 42 / Nautilus 42 / X11）实测。

## 用法

文件管理器里**右键文件/文件夹 → 脚本 → Copy Path**，绝对路径进入剪贴板；
多选文件则逐行复制多个路径。

## 安装 / 卸载

```bash
./copypath install     # 在 ~/.local/share/nautilus/scripts/ 建硬链接
nautilus -q            # 重启文件管理器，右键出现"脚本 → Copy Path"
./copypath uninstall   # 删硬链接即完全卸载
```

## 迁移

把 `copypath` 这一个文件拷到新机器（Ubuntu/GNOME/X11），重跑 `./copypath install`。

## 依赖

- `xclip`：`sudo apt install xclip`

## 影响面（隔离性）

- 安装的全部影响 = `~/.local/share/nautilus/scripts/Copy Path` **一个硬链接**
  （Nautilus 的脚本扫描不认符号链接，故用硬链接；与源文件同 inode，改源文件即生效）
- 不修改 `~/.bashrc` 等任何其他文件；运行时不落盘任何内容
- 卸载删硬链接即净；直接删目录不卸载只会在 scripts 目录残留一份无害文件副本

## 已知边界（均为 Nautilus 42 / GNOME 上游设计，非本工具问题）

- **空白处右键没有"脚本"入口**：Nautilus 42 源码中 Scripts 子菜单只挂在"选中文件"的右键菜单里（`update_selection_menu`），空白菜单（`update_background_menu`）无此逻辑。替代：Ctrl+L 显示完整路径。
- **桌面右键没有"脚本"入口**：桌面菜单由 GNOME 桌面图标扩展（DING）提供，不支持 Nautilus 脚本。
- 脚本内容变化后若用会改 inode 的编辑方式重写过源文件，硬链接会断开，重跑一次 `./copypath install` 即可。
