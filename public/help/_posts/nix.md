---
category: help
layout: help
mirrorid: nix
---

## Nix 镜像使用帮助

[Nix](https://nixos.org/nix) 是一个支持 Linux 和 macOS 的独特的“函数式包管理器”，具有原子更新、依赖隔离、构建尽可能可复现等特点。

[Nixpkgs](https://nixos.org/nixpkgs) 是 Nix 包管理器对应的软件发行版，使用 Nix 函数式语言编写，除软件包外提供用于软件定制、构建、开发环境配置的工具。

[NixOS](https://nixos.org) 是一个基于 Nix 和 Nixpkgs 的 GNU/Linux 发行版。在 Nixpkgs 中的软件之上 NixOS 使用 Nix 语言提供了声明式的系统配置，实现系统完整可复现、版本快速切换等功能。

### Nix

细节内容，请参见 Nix 文档中的 [Installing a Binary Distribution](https://nixos.org/nix/manual/#ch-installing-binary) 一节。

- 单用户安装

    ```console
    $ sh <(curl https://{{ site.hostname }}/nix/latest/install)
    ```
- 多用户安装：

    ```console
    $ sh <(curl https://{{ site.hostname }}/nix/latest/install) --daemon
    ```

如果需要，可以在[文件列表中手动挑选需要的版本](https://{{ site.hostname }}/nix)。

### NixOS

NixOS 的安装镜像和 OVF 虚拟机镜像可以在镜像站首页“下载链接”处或 <https://{{ site.hostname }}/nixos-images/> 下载。

### Nixpkgs binary cache

Binary cache 的镜像位于 <https://{{ site.hostname }}/nix-channels/store>，与 channel 同步更新。

目前 nix-darwin 的 binary cache 并不工作，请使用官方源。

以优先选择镜像，备选源站为例，选择以下配置之一：

- 单独安装的 Nix：编辑配置文件添加或修改如下项（通常系统配置在 `/etc/nix/nix.conf`，用户配置在 `~/.config/nix/nix.conf`）：

    ```plain
    substituters = https://{{ site.hostname }}/nix-channels/store https://cache.nixos.org/
    ```

- NixOS 21.11 及之前的版本在 `configuration.nix` 中使用如下配置（https://cache.nixos.org 会被自动添加）

    ```nix
    nix.binaryCaches = [ "https://{{ site.hostname }}/nix-channels/store" ];
    ```

- NixOS 22.05 及之后的版本在 `configuration.nix` 中使用如下配置（https://cache.nixos.org 会被自动添加）：

    ```nix
    nix.settings.substituters = [ "https://{{ site.hostname }}/nix-channels/store" ];
    ```

### Nixpkgs channel

Channel 的镜像位于 <https://{{ site.hostname }}/nix-channels/> 目录下，使用方式与 <https://nixos.org/channels/> 相同。

单独安装的 Nix 替换 `nixpkgs-unstable` 命令如下：

```console
$ nix-channel --add https://{{ site.hostname }}/nix-channels/nixpkgs-unstable nixpkgs
$ nix-channel --update
```

替换 NixOS channel 命令如下（以 root 执行，将 `19.09` 替换为系统版本）：

```console
# nix-channel --add https://{{ site.hostname }}/nix-channels/nixos-19.09 nixos
# nix-channel --update
```
