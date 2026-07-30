# myarch — 自用桌面 Arch Linux 方案

> `ai-agent` 分支：实际 dotfiles 配置
> `main` 分支：手动安装文档

## HW Spec

| 组件 | 型号 |
|---|---|
| 机型 | ThinkPad X1 Carbon Gen 9 |
| CPU | Intel Core i7-1185G7 (8) @ 4.80GHz |
| 内存 | 32GB DDR4 |
| 存储 | 2TB NVMe |

## Software Stack

| 层 | 选型 |
|---|---|
| OS | Arch Linux |
| WM | [niri](https://github.com/YaLTeR/niri) 26 (scrollable-tiling) |
| 面板 | [DMS](https://danklinux.com) (DankMaterialShell) |
| Shell | ZSH + Oh My Zsh + [Starship](https://starship.rs) |
| 终端 | [Ghostty](https://ghostty.org) |
| 输入法 | Fcitx5 + Rime（万象） |
| 播放器 | mpv + ModernZ / MPD + rmpc |
| 浏览器 | Zen Browser |
| 文件管理 | yazi |

## 目录结构

```
.config/
├── niri/                    # niri WM 配置
│   ├── config.kdl           #   主配置（include dms/*）
│   └── user.kdl             #   自定义覆盖
├── mpv/                     # 视频播放器
│   ├── mpv.conf
│   ├── scripts/
│   │   ├── modernz.lua      #   ModernZ OSC
│   │   └── thumbfast.lua    #   缩略图
│   └── script-opts/
│       └── modernz.conf
├── mpd/mpd.conf             # 音乐播放守护
├── ghostty/config           # 终端配置
├── environment.d/           # 环境变量
│   ├── 80-zen-wayland.conf  #   MOZ_ENABLE_WAYLAND
│   ├── 90-dms.conf          #   ELECTRON Ozone / TERMINAL
│   └── fcitx5.conf          #   GTK/QT IM module
├── fastfetch/config.jsonc   # 系统信息
├── starship.toml            # Shell 提示符
├── fcitx5/                  # 输入法
│   ├── config               #   热键
│   └── profile              #   输入法列表
├── autostart/fcitx-5.desktop
└── systemd/user/            # 用户级服务
    ├── wl-clip-persist.service
    ├── wl-gammarelay.service
    ├── mpd.socket.d/bind.conf
    └── app-@autostart.service.d/override.conf

.zshrc
.bashrc
pkglist-official.txt          # 官方包清单
pkglist-aur.txt               # AUR 包清单
```

## 恢复

```bash
# 1. 安装包
sudo pacman -S --needed - < pkglist-official.txt
yay -S --needed - < pkglist-aur.txt

# 2. 部署配置
git clone --branch ai-agent https://github.com/jianlongliu/myarch.git
cd myarch
stow -t ~ .
```
