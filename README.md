![screenshot](/screenshots/Screenshot.png)
![screenshot](/screenshots/Screenshot-X.png)

# myarch — 自用桌面 Arch Linux 方案

> `ai-agent-generated` 分支：实际 dotfiles + 包清单
> `main` 分支：从零安装文档

## 1. HW Spec

| 组件 | 型号 |
|---|---|
| 机型 | ThinkPad X1 Carbon Gen 9 |
| CPU | Intel Core i7-1185G7 (8) @ 4.80GHz |
| 内存 | 32GB DDR4 |
| 存储 | 2TB NVMe |

## 2. Software Stack

| 层 | 选型 | 说明 |
|---|---|---|
| WM | [niri](https://github.com/YaLTeR/niri) 26 | scrollable-tiling Wayland compositor |
| 面板 | [DMS](https://danklinux.com) | DankMaterialShell，matugen 主题引擎 |
| Shell | ZSH + [Oh My Zsh](https://ohmyz.sh) + [Starship](https://starship.rs) | Catppuccin Mocha 配色提示符 |
| 终端 | [Ghostty](https://ghostty.org) | GPU 加速，SFMono Nerd Font |
| 输入法 | Fcitx5 + Rime（[万象](https://github.com/amzxyz/rime_wanxiang)） | 中英文输入 |
| 播放器 | [mpv](https://mpv.io) + [ModernZ](https://github.com/Samillion/ModernZ) | 自定义 OSC |
| 音乐 | [MPD](https://github.com/MusicPlayerDaemon/MPD) + [rmpc](https://github.com/mierak/rmpc) | TUI 客户端 |
| 浏览器 | [Zen Browser](https://zen-browser.app/) | Firefox 内核，Wayland 原生 |
| 文件管理 | [yazi](https://github.com/sxyazi/yazi) | Rust 终端文件管理器 |

## 3. 配置目录结构

```
.config/
├── niri/                          # niri WM
│   ├── config.kdl                 #   主配置 + includes
│   └── user.kdl                   #   自定义：modeline 1600p、模糊、微信启动
├── mpv/                           # 视频播放器
│   ├── mpv.conf                   #   hwdec=gpu-next, wayland
│   ├── scripts/
│   │   ├── modernz.lua            #   ModernZ OSC 界面
│   │   └── thumbfast.lua          #   缩略图预览
│   └── script-opts/modernz.conf   #   ModernZ 配色布局
├── mpd/mpd.conf                   # 音乐播放守护
├── rmpc/
│   ├── config.ron                 #   rmpc MPD TUI 客户端配置
│   └── theme.ron                  #   rmpc 主题/布局/配色
├── ghostty/config                 # 终端（SFMono Nerd Font）
├── environment.d/
│   ├── 80-zen-wayland.conf        #   MOZ_ENABLE_WAYLAND=1
│   ├── 90-dms.conf                #   ELECTRON_OZONE_PLATFORM_HINT, TERMINAL
│   └── fcitx5.conf                #   GTK/QT IM module
├── fastfetch/config.jsonc         # 系统信息展示
├── starship.toml                  # Shell 提示符
├── fcitx5/
│   ├── config                     #   输入法热键
│   └── profile                    #   keyboard-us + rime
├── yazi/
│   ├── yazi.toml                  #   文件管理器 openers
│   └── package.toml               #   gvfs 插件
├── autostart/fcitx-5.desktop      # fcitx5 自启动
├── mimeapps.list                  # MIME 文件关联
├── xdg-terminals.list             # 默认终端 = ghostty
└── systemd/user/                  # 用户级 systemd 服务
    ├── wl-clip-persist.service    #   Wayland 剪贴板持久化
    ├── wl-gammarelay.service      #   屏幕色温/亮度 daemon
    ├── mpd.socket.d/bind.conf     #   MPD 绑定 127.0.0.1:6600
    └── app-@autostart.service.d/override.conf  # autostart 延后到 DMS 启动

.zshrc                             # 别名、starship、oh-my-zsh 插件
.bashrc                            # 备用 bash 配置
.local/bin/
  └── gammarelay                   # gamma/亮度/色温控制脚本
pkglist-official.txt               # 官方包清单（154 个）
pkglist-aur.txt                    # AUR 包清单（26 个）
```

## 4. 包管理

```bash
# 官方包
sudo pacman -S --needed - < pkglist-official.txt

# AUR 包
yay -S --needed - < pkglist-aur.txt
```

## 5. 部署

```bash
git clone --branch ai-agent-generated https://github.com/jianlongliu/myarch.git
cd myarch

# 方式一：stow（推荐）
sudo pacman -S stow
stow -t ~ .

# 方式二：裸 git
# git --git-dir=$HOME/myarch --work-tree=$HOME checkout ai-agent-generated
```

## 6. Screenshots

![mpv_with_modernz](/screenshots/Screenshot_MPV_with_Modernz.png)
![rmpc](</screenshots/Screenshot from 2026-03-23 19-02-49.png>)

## 7. Branches

- `main` — 从零安装文档
- `ai-agent-generated` — 本分支，实际配置文件 + 包清单
