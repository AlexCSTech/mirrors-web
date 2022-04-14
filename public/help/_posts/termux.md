---
category: help
layout: help
mirrorid: termux
---

Termux 镜像使用帮助
===================

Termux 是什么
-------------

> Termux is a terminal emulator and Linux environment bringing powerful terminal access to Android.

Termux 是运行在 Android 上的 terminal。不需要root，运行于内部存储（不在SD卡上）。

自带了一个包管理器，可以安装许多现代化的开发和系统维护工具。比如：

 * neovim
 * tmux
 * zsh
 * clang
 * gcc
 * weechat
 * irssi
 * ...

如何使用 Termux 镜像
------------------

### 图形界面（TUI）替换

在较新版的 Termux 中，官方提供了图形界面（TUI）来半自动替换镜像，推荐使用该种方式以规避其他风险。
在 Termux 中执行如下命令

```bash
termux-change-repo
```

在图形界面引导下，使用自带方向键可上下移动。   
第一步使用空格选择需要更换的仓库，之后在第二步选择 TUNA/BFSU 镜像源。确认无误后回车，镜像源会自动完成更换。

### 命令行替换

如果您在使用termux v0.118及以上版本，使用如下命令行替换官方源为 TUNA 镜像源

``` bash
sed -i 's@^\(deb.*stable main\)$@#\1\ndeb https://{{ site.hostname }}/termux/termux-packages-24 stable main@' $PREFIX/etc/apt/sources.list
apt update && apt upgrade
```

如果您在使用termux v0.117及以下版本，则需要使用如下命令

```bash
sed -i 's@^\(deb.*stable main\)$@#\1\ndeb https://mirrors.tuna.tsinghua.edu.cn/termux/termux-packages-24 stable main@' $PREFIX/etc/apt/sources.list
sed -i 's@^\(deb.*games stable\)$@#\1\ndeb https://mirrors.tuna.tsinghua.edu.cn/termux/game-packages-24 games stable@' $PREFIX/etc/apt/sources.list.d/game.list
sed -i 's@^\(deb.*science stable\)$@#\1\ndeb https://mirrors.tuna.tsinghua.edu.cn/termux/science-packages-24 science stable@' $PREFIX/etc/apt/sources.list.d/science.list
apt update && apt upgrade
```


### 手动修改

编辑 `$PREFIX/etc/apt/sources.list` 修改为如下内容

```
# The termux repository mirror from TUNA:
deb https://{{ site.hostname }}/termux/termux-packages-24 stable main
```

（仅v0.117及以下）编辑 `$PREFIX/etc/apt/sources.list.d/game.list` 修改为如下内容

```
# The termux repository mirror from TUNA:
deb https://{{ site.hostname }}/termux/termux-packages-24 games main
```

（仅v0.117及以下）编辑 `$PREFIX/etc/apt/sources.list.d/science.list` 修改为如下内容

```
# The termux repository mirror from TUNA:
deb https://{{ site.hostname }}/termux/termux-packages-24 science main
```

请使用内置或安装在 Termux 里的文本编辑器，例如 `vi` / `vim` / `nano` 等，**不要使用 RE 管理器等其他具有 ROOT 权限的外部 APP** 来修改 Termux 的文件

### 社区源

镜像站还提供了如下社区维护的源，如需使用请自行添加：

- https://{{ site.hostname }}/termux/x11-packages
- https://{{ site.hostname }}/termux/unstable-packages
- https://{{ site.hostname }}/termux/termux-root-packages-24

### 警告

镜像仅适用于 Android 7.0 (API 24) 及以上版本，旧版本系统使用本镜像可能导致程序错误。