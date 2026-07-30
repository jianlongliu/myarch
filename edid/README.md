# EDID — eDP-1 面板配置

> ThinkPad X1 Carbon Gen 9
> 面板：CSOT T3 (CSO1411)

## 用途

原厂 EDID 不暴露 2560x1600@60Hz 模式，通过自定义 EDID 注入实现 1600p 省电模式。

配合 `niri/user.kdl` 中的 modeline 使用：

```
output "eDP-1" {
    modeline 348.50 2560 2752 3032 3504 1600 1603 1609 1658 "+hsync" "-vsync"
    scale 1.5
}
```

## 恢复

```bash
# 1. 复制 EDID 到 firmware
sudo cp CSO1411.bin /usr/lib/firmware/edid/

# 2. 复制内核 cmdline（覆盖）
sudo cp kernel-cmdline /etc/kernel/cmdline

# 3. mkinitcpio.conf 添加 FILES
#    编辑 /etc/mkinitcpio.conf，确保包含：
#    FILES=(/lib/firmware/edid/CSO1411.bin)

# 4. 重新生成 initramfs
sudo mkinitcpio -P

# 5. 重启
reboot
```
