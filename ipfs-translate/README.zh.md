
# go-ipfs

![banner](https://ipfs.io/ipfs/QmVk7srrwahXLNmcDYvyUEJptyoxpndnRa57YJ11L4jV26/ipfs.go.png)

[![](https://img.shields.io/badge/made%20by-Protocol%20Labs-blue.svg?style=flat-square)](http://ipn.io)
[![](https://img.shields.io/badge/project-IPFS-blue.svg?style=flat-square)](http://ipfs.io/)
[![](https://img.shields.io/badge/freenode-%23ipfs-blue.svg?style=flat-square)](http://webchat.freenode.net/?channels=%23ipfs)
[![standard-readme compliant](https://img.shields.io/badge/standard--readme-OK-green.svg?style=flat-square)](https://github.com/RichardLitt/standard-readme)
[![GoDoc](https://godoc.org/github.com/ipfs/go-ipfs?status.svg)](https://godoc.org/github.com/ipfs/go-ipfs)
[![Build Status](https://travis-ci.org/ipfs/go-ipfs.svg?branch=master)](https://travis-ci.org/ipfs/go-ipfs)

[![Throughput Graph](https://graphs.waffle.io/ipfs/go-ipfs/throughput.svg)](https://waffle.io/ipfs/go-ipfs/metrics/throughput)

> Go中的IPFS实现

## 校对🀄️

- ⏰ 2018 7.10 开始

进度: `1/36`

- [ ] [README.md](./README.zh.md)
- [x] [contribute.zh.md](./contribute.zh.md)

IPFS是一个全局的,版本化的对等文件系统. 它结合了Git,BitTorrent,Kademlia,SFS和Web的好点子. 它就像一个bittorrent swarm,交换git对象. IPFS提供了一个像HTTP Web一样简单的接口,但内置了永久性. 您还可以将世界挂载到/ ipfs. 有关详情,请参阅: 

https\://github.com/ipfs/ipfs[. ](https://github.com/ipfs/ipfs)请提出有关IPFS的所有问题

设计*在里面*ipfs repo问题[. ](https://github.com/ipfs/ipfs/issues)请提出有关Go IPFS的所有问题*履行*在[这个回购](https://github.com/ipfs/go-ipfs/issues). 

## 目录

-   [安全问题](#security-issues)
-   [安装](#install)
    -   [系统要求](#system-requirements)
    -   [安装预建包](#install-prebuilt-packages)
    -   [来自Linux包管理器](#from-linux-package-managers)
    -   [从源代码构建](#build-from-source)
        -   [安装Go](#install-go)
        -   [下载并编译IPFS](#download-and-compile-ipfs)
        -   [故障排除](#troubleshooting)
    -   [发展依赖](#development-dependencies)
    -   [更新](#updating)
-   [用法](#usage)
-   [入门](#getting-started)
    -   [有些事要尝试](#some-things-to-try)
    -   [Docker用法](#docker-usage)
    -   [故障排除](#troubleshooting-1)
-   [特约](#contributing)
    -   [想破解IPFS?](#want-to-hack-on-ipfs)
    -   [想看看我们的代码?](#want-to-read-our-code)
-   [执照](#license)

## 安全问题

IPFS协议及其实现仍处于重大发展阶段. 这意味着我们的协议可能存在问题,或者我们的实现可能存在错误. 而且 - 虽然IPFS还没有生产就绪 - 许多人已经在他们的机器上运行节点. 因此,我们非常重视安全漏洞. 如果您发现安全问题,请立即引起我们的注意!

如果您发现可能影响实时部署的漏洞 (例如,通过公开远程执行漏洞利用) ,请将您的报告私下发送至security@ipfs.io. 请不要提交公共问题. security@ipfs.io的GPG密钥是[4B9665FB 92636D17 7C7A86D3 50AAE8A9 59B13AF3](https://pgp.mit.edu/pks/lookup?op=get&search=0x50AAE8A959B13AF3). 

如果问题是无法立即利用的协议弱点或尚未部署的问题,请公开讨论. 

## 安装

IPFS的规范下载说明在: <http://ipfs.io/docs/install/>. 它是**强烈建议**如果您对IPFS开发不感兴趣,请遵循这些说明. 

### 系统要求

IPFS可以在大多数Linux,macOS和Windows系统上运行. 我们建议在具有至少2 GB RAM的机器上运行它 (只有一个CPU内核可以正常运行) ,但只需1 GB的内存即可正常运行. 在内存较少的系统上,它可能不完全稳定. 

### 安装预建包

我们在我们的网站上托管预建的二进制文件[发行页面](https://ipfs.io/ipns/dist.ipfs.io#go-ipfs). 

从那里: 

-   单击页面右侧的蓝色"Download go-ipfs". 
-   打开/提取存档. 
-   移动`ipfs`到你的路上 (`install.sh`能为你做到这一点) . 

### 来自Linux包管理器

-   [Arch Linux](#arch-linux)
-   [尼克斯](#nix)
-   [快照](#snap)

#### Arch Linux

在Arch Linux中,go-ipfs可用作[去-IPF问题](https://www.archlinux.org/packages/community/x86_64/go-ipfs/)包. 

    $ sudo pacman -S go-ipfs

go-ipfs的开发版本也在AUR下[去-IPF问题,混帐](https://aur.archlinux.org/packages/go-ipfs-git/). 您可以使用自己喜欢的AUR Helper安装它,也可以从AUR手动安装. 

### 尼克斯

对于Linux和MacOSX,您可以使用纯功能包管理器[尼克斯](https://nixos.org/nix/): 

    $ nix-env -i ipfs

您也可以使用它的属性名称来安装Package`ipfs`. 

#### 快照

随着快照,在任何一个[支持的Linux发行版](https://snapcraft.io/docs/core/install): 

    $ sudo snap install ipfs

### 从源代码构建

#### 安装Go

ipfs的构建过程需要Go 1.10或更高版本. 如果你没有它: [下载Go 1.10+](https://golang.org/dl/). 

您需要将Go的bin目录添加到您的`$PATH`环境变量,例如,通过将这些行添加到您的`/etc/profile` (用于系统范围的安装) 或`$HOME/.profile`: 

    export PATH=$PATH:/usr/local/go/bin
    export PATH=$PATH:$GOPATH/bin

 (如果遇到麻烦,请参阅[去安装说明](https://golang.org/doc/install)) . 

#### 下载并编译IPFS

    $ go get -u -d github.com/ipfs/go-ipfs

    $ cd $GOPATH/src/github.com/ipfs/go-ipfs
    $ make install

如果你是在FreeBSD而不是`make install`使用`gmake install`. 

#### 建立在不太常见的系统上

如果您的操作系统没有得到官方支持,但您仍然想尝试构建ipfs (在大多数情况下它应该可以正常工作) ,您可以执行以下操作而不是`make install`: 

    $ make install_unsupported

注意: 如果,此过程可能会中断[gx](https://github.com/whyrusleeping/gx) (用于依赖关系管理) 或其任何依赖关系`go get`将始终为每个依赖项选择最新的代码,通常会导致API不匹配. 

#### 故障排除

-   分离[说明可用于在Windows上构建](docs/windows.md). 
-   也,[OpenBSD的说明](docs/openbsd.md). 
-   `git`是必需的`go get`获取所有依赖项. 
-   包管理器通常包含过时的`golang`包. 确保这件事`go version`报告至少1.10. 请参阅上文,了解如何安装go. 
-   如果您对开发感兴趣,请同时安装开发依赖项. 
-   *警告: 旧版本的OSX FUSE (适用于Mac OS X) 在安装时可能会导致内核崩溃!*我们强烈建议您使用[最新版本的OSX FUSE](http://osxfuse.github.io/).  (看到<https://github.com/ipfs/go-ipfs/issues/177>) 
-   有关设置FUSE的更多详细信息 (以便可以安装文件系统) ,请参阅docs文件夹. 
-   Shell命令完成可用于`misc/completion/ipfs-completion.bash`. 读[文档/ command-completion.md](docs/command-completion.md)学习如何安装它. 
-   见[init示例](https://github.com/ipfs/website/tree/master/static/docs/examples/init)有关如何将IPFS连接到systemd或您的发行版使用的任何init系统. 

### 发展依赖

如果更改协议缓冲区,则需要安装[protoc编译器](https://github.com/google/protobuf). 

### 更新

#### 使用ipfs-update进行更新

IPFS有一个可以通过访问的更新工具`ipfs update`. 该工具未与IPFS一起安装,以保持该逻辑独立于主代码库. 安装`ipfs update`,[在这里下载](https://ipfs.io/ipns/dist.ipfs.io/#ipfs-update). 

#### 使用IPFS下载IPFS构建

列出go-ipfs的可用版本: 

    $ ipfs cat /ipns/dist.ipfs.io/go-ipfs/versions

然后,从上一个命令 ($ VERSION) 查看版本的可用构建: 

    $ ipfs ls /ipns/dist.ipfs.io/go-ipfs/$VERSION

要下载版本的给定版本: 

    $ ipfs get /ipns/dist.ipfs.io/go-ipfs/$VERSION/go-ipfs_$VERSION_darwin-386.tar.gz # darwin 32-bit build
    $ ipfs get /ipns/dist.ipfs.io/go-ipfs/$VERSION/go-ipfs_$VERSION_darwin-amd64.tar.gz # darwin 64-bit build
    $ ipfs get /ipns/dist.ipfs.io/go-ipfs/$VERSION/go-ipfs_$VERSION_freebsd-amd64.tar.gz # freebsd 64-bit build
    $ ipfs get /ipns/dist.ipfs.io/go-ipfs/$VERSION/go-ipfs_$VERSION_linux-386.tar.gz # linux 32-bit build
    $ ipfs get /ipns/dist.ipfs.io/go-ipfs/$VERSION/go-ipfs_$VERSION_linux-amd64.tar.gz # linux 64-bit build
    $ ipfs get /ipns/dist.ipfs.io/go-ipfs/$VERSION/go-ipfs_$VERSION_linux-arm.tar.gz # linux arm build
    $ ipfs get /ipns/dist.ipfs.io/go-ipfs/$VERSION/go-ipfs_$VERSION_windows-amd64.zip # windows 64-bit build

## 用法

      ipfs - Global p2p merkle-dag filesystem.

      ipfs [<flags>] <command> [<arg>] ...

    SUBCOMMANDS
      BASIC COMMANDS
        init          Initialize ipfs local configuration
        add <path>    Add a file to ipfs
        cat <ref>     Show ipfs object data
        get <ref>     Download ipfs objects
        ls <ref>      List links from an object
        refs <ref>    List hashes of links from an object

      DATA STRUCTURE COMMANDS
        block         Interact with raw blocks in the datastore
        object        Interact with raw dag nodes
        files         Interact with objects as if they were a unix filesystem

      ADVANCED COMMANDS
        daemon        Start a long-running daemon process
        mount         Mount an ipfs read-only mountpoint
        resolve       Resolve any type of name
        name          Publish or resolve IPNS names
        dns           Resolve DNS links
        pin           Pin objects to local storage
        repo          Manipulate an IPFS repository

      NETWORK COMMANDS
        id            Show info about ipfs peers
        bootstrap     Add or remove bootstrap peers
        swarm         Manage connections to the p2p network
        dht           Query the DHT for values or peers
        ping          Measure the latency of a connection
        diag          Print diagnostics

      TOOL COMMANDS
        config        Manage configuration
        version       Show ipfs version information
        update        Download and apply go-ipfs updates
        commands      List all available commands

      Use 'ipfs <command> --help' to learn more about each command.

      ipfs uses a repository in the local file system. By default, the repo is located
      at ~/.ipfs. To change the repo location, set the $IPFS_PATH environment variable:

        export IPFS_PATH=/path/to/ipfsrepo

## 入门

也可以看看: <http://ipfs.io/docs/getting-started/>

要开始使用IPFS,必须首先在系统上初始化IPFS的配置文件,这样做完成`ipfs init`. 看到`ipfs init --help`有关可选参数的信息. 初始化完成后,即可使用`ipfs mount`,`ipfs add`以及任何其他要探索的命令!

### 有些事要尝试

本地'ipfs工作'的基本证明: 

    echo "hello world" > hello
    ipfs add hello
    # This should output a hash string that looks something like:
    # QmT78zSuBmuS4z925WZfrqQ1qHaJ56DQaTfyMUF7F8ff5o
    ipfs cat <that hash>

### Docker用法

IPFS泊坞窗图像托管在[hub.docker.com/r/ipfs/go-ipfs](https://hub.docker.com/r/ipfs/go-ipfs/). 要使文件在容器内可见,您需要使用安装主机目录`-v`docker的选项. 选择要用于从IPFS导入/导出文件的目录. 您还应该选择一个目录来存储在重新启动容器时将保留的IPFS文件. 

    export ipfs_staging=</absolute/path/to/somewhere/>
    export ipfs_data=</absolute/path/to/somewhere_else/>

启动运行ipfs的容器并公开端口4001,5001和8080: 

    docker run -d --name ipfs_host -v $ipfs_staging:/export -v $ipfs_data:/data/ipfs -p 4001:4001 -p 127.0.0.1:8080:8080 -p 127.0.0.1:5001:5001 ipfs/go-ipfs:latest

观看ipfs日志: 

    docker logs -f ipfs_host

等待ipfs启动. 当你看到ipfs正在运行: 

    Gateway (readonly) server
    listening on /ip4/0.0.0.0/tcp/8080

你现在可以停止观看日志了. 

运行ipfs命令: 

    docker exec ipfs_host ipfs <args...>

例如: 连接到同行

    docker exec ipfs_host ipfs swarm peers

添加文件: 

    cp -r <something> $ipfs_staging
    docker exec ipfs_host ipfs add -r /export/<something>

停止正在运行的容器: 

    docker stop ipfs_host

### 故障排除

如果之前已经安装过IPFS,并且遇到了使新版本工作的问题,请尝试删除 (或在其他地方备份) IPFS配置目录 (默认为〜/ .ipfs) 并重新运行`ipfs init`. 这会将配置文件重新初始化为其默认值,并清除任何错误条目的本地数据存储区. 

请将一般问题和帮助请求发送给我们[论坛](https://discuss.ipfs.io)或我们的IRC频道 (freenode #ipfs) . 

如果您认为自己发现了错误,请查看[问题清单](https://github.com/ipfs/go-ipfs/issues)并且,如果您没有在那里看到您的问题,请在IRC (freenode #ipfs) 上与我们联系或提交您自己的问题!

## 特约

我们❤️所有[我们的贡献者](docs/AUTHORS);没有你,这个项目就不会是这样!如果您想提供帮助,请参阅[Contribute.md](contribute.md). 

该存储库属于IPFS[行为守则](https://github.com/ipfs/community/blob/master/code-of-conduct.md). 

### 想破解IPFS?

[![](https://cdn.rawgit.com/jbenet/contribute-ipfs-gif/master/img/contribute.gif)](https://github.com/ipfs/community/blob/master/contributing.md)

### 想看看我们的代码?

有些地方可以帮助你入门.  (WIP) 

主文件: [CMD / IPF问题/ main.go](https://github.com/ipfs/go-ipfs/blob/master/cmd/ipfs/main.go) <br>CLI命令: [芯/命令/](https://github.com/ipfs/go-ipfs/tree/master/core/commands) <br>Bitswap (数据交易引擎) : [交换/比特交换/](https://github.com/ipfs/go-ipfs/tree/master/exchange/bitswap)

DHT: <https://github.com/libp2p/go-libp2p-kad-dht> <br>PubSub的: <https://github.com/libp2p/go-floodsub> <br>libp2p: <https://github.com/libp2p/go-libp2p>

## 执照

MIT
