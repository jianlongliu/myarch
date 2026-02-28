![screenshot](/screenshots/Screenshot.png)
![screenshot](/screenshots/Screenshot-X.png)
![screenshot](/screenshots/Screenshot_from_2026-02-19_12-16-08.png)

## 1. 准备
### 1.1 USB烧录工具
Ventoy    
https://www.ventoy.net/cn/index.html

rufus    
https://rufus.ie

### 1.2 Arch半自动部署工具 [可选]
`archinstall`
> tips: 最小化安装，后续有图形界面需求单独安装    
    
### 1.3 Arch 国内源
`sudo reflector --country 'China' --latest 10 --sort rate --save /etc/pacman.d/mirrorlist`

    
## 2. Wayland compositor
### 2.1 niri
https://github.com/YaLTeR/niri    
`sudo pacman -S niri`

### 2.2 dank material shell
https://danklinux.com/    
`curl -fsSL https://install.danklinux.com | sh`

## 3. Display Manager

![img](https://github.com/Nomadcxx/sysc-greet/raw/master/assets/showcase.gif)

### greetd    
https://github.com/kennylevinsen/greetd    

#### sysc-greet    
https://github.com/Nomadcxx/sysc-greet    
`paru -S sysc-greet`

## 4. Shell
### zsh
`sudo pacman -S zsh`    

#### oh-my-zsh
https://ohmyz.sh    
`sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`    

### `eza`    
`sudo pacman -S eza`    
https://github.com/eza-community/eza
> `ls`的rust更现代化实现

### `bat`    
`sudo pacman -S bat`    
https://github.com/sharkdp/bat
> `cat`的现代化实现

## 5. IME

### fcitx5
`sudo pacman -S fcitx5 fcitx5-rime`

#### 万象输入法
https://github.com/amzxyz/rime_wanxiang

#### fcitx5 输入法皮肤
https://github.com/catppuccin/fcitx5

## 6. 安全和隐私
### 6.1 firewalld
```zsh
# arch
sudo pacman -S firewalld
```
⚠️ 配置clash代理，把虚拟网卡加入firewalld白名单避免和防火墙冲突    
`sudo firewall-cmd --permanent --zone=trusted --add-interface=FlClash`

### 6.2 Secure Boot (安全引导) 自定义签名
https://jianl.dev/posts/sbctl/

## 7. App
### 7.1 Zen Browser
![zen](/screenshots/Screenshot-zen.png)
`paru -S zen-browser`
https://zen-browser.app/

### 7.2 yazi
https://github.com/sxyazi/yazi    
`paru -S yazi`    

### 7.3 neovim
https://neovim.io/
https://github.com/neovim/neovim    
`sudo pacman -S neovim`

#### lazyvim
https://www.lazyvim.org/    
`git clone https://github.com/LazyVim/starter ~/.config/nvim`

## 8. 多媒体播放
![mpv_with_modernz](/screenshots/Screenshot_MPV_with_Modernz.png)
### MPV
https://mpv.io    
`paru -S mpv`     

#### Modernz 
https://github.com/Samillion/ModernZ

## 9. 远程协助

### 9.1 wayvnc
`sudo pacman -S wayvnc`

### 9.2 向日葵
`paru -S sunloginclient`    
https://jianl.dev/posts/sunloginclient/

## 10. Q&A
#### 解决微信不能使用fcitx5 中文输入

```sh
# 微信flatpak
`sudo flatpak override --env=GTK_IM_MODULE=fcitx --env=QT_IM_MODULE=fcitx --env=XMODIFIERS=@im=fcitx com.tencent.WeChat`

# 微信Linux
`Exec=env GTK_IM_MODULE=fcitx QT_IM_MODULE=fcitx QT_IM_MODULE=fcitx XMODIFIERS=@im=fcitx /usr/bin/wechat %U`
```
//progressing

## 11. Colorschemes
### Rose Pine
https://rosepinetheme.com/

### Catppuccin
https://catppuccin.com/
