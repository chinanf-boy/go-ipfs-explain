
# 在Windows上构建

![](https://ipfs.io/ipfs/QmccXW7JSZMVXidSc7tHsU6aktuaiV923q4yBGHUsdymYo/build.gif)

## 安装Go

`go-ipfs`基于Golang构建,因此所有构建方法都依赖于它. \
<https://golang.org/doc/install>\
该`GOPATH`环境变量也必须设置. \
<https://golang.org/doc/code.html#GOPATH>

## 选择您要继续的方式

`go-ipfs`利用`make`自动化构建和运行测试,但可以在没有它的情况下构建`git`和`go`. \
无论您选择哪种方法,如果遇到问题,请参阅[故障排除](#troubleshooting)部分. 

**运用`make`: **\
MSYS2和Cygwin提供了我们需要构建的Unix工具`go-ipfs`. 您可以使用其中任何一个,但如果您还没有安装,我们建议使用MSYS2. \
[MSYS2→](#msys2)\
[Cygwin的→](#cygwin)  

**手动使用构建工具: **\
本节假设您的工作版本为`go`和`git`已经设置好了如果您的环境限制安装其他软件,或者您正在将IPFS集成到您自己的构建系统中,那么您可能希望以这种方式构建. \
[最小→](#minimal)  

## MSYS2

1.  安装msys2 (<http://www.msys2.org>) 
2.  在正常情况下运行以下内容`cmd`提示 (不是MSYS2提示,我们只需要MSYS2的工具) . \
    下面是对该块的解释. 


    SET PATH=%PATH%;\msys64\usr\bin
    pacman --noconfirm -S  git make unzip
    go get -u github.com/ipfs/go-ipfs
    cd %GOPATH%\src\github.com\ipfs\go-ipfs
    make install
    %GOPATH%\bin\ipfs.exe version --all

如果没有错误,则最终命令应输出类似于"`ipfs version 0.4.14-dev-XXXXXXX`"其中"XXXXXXX"应匹配当前的短哈希值`go-ipfs`回购. 您可以通过此命令检索所述哈希: `git rev-parse --short HEAD`. \
如果`ipfs.exe`执行并且版本字符串匹配,然后构建成功. 

|                                        命令 | 说明                                                                                         |
| ----------------------------------------: | :----------------------------------------------------------------------------------------- |
|         `SET PATH=%PATH%;\msys64\usr\bin` | 将msys2的工具添加到我们的工具中[`PATH`](https://ss64.com/nt/path.html);默认为:  (\\ msys64 \\ usr \\ bin)  |
|   `pacman --noconfirm -S  git make unzip` | 安装`go-ipfs`构建依赖项                                                                           |
|       `go get -u github.com/ipfs/go-ipfs` | 获取/更新`go-ipfs`资源                                                                           |
| `cd %GOPATH%\src\github.com\ipfs\go-ipfs` | 改成`go-ipfs`源目录                                                                             |
|                            `make install` | 构建并安装到`%GOPATH%\bin\ipfs.exe`                                                              |
|     `%GOPATH%\bin\ipfs.exe version --all` | 测试构建的二进制文件                                                                                 |

要在更改源后再次构建,请运行: 

    SET PATH=%PATH%;\msys64\usr\bin
    cd %GOPATH%\src\github.com\ipfs\go-ipfs
    make install

**小费: **避免设置`PATH`每次  (`SET PATH=%PATH%;\msys64\usr\bin`) ,你可以永久锁定它`setx`在设置一次之后: 

    SETX PATH %PATH%

## Cygwin的

1.  安装Cygwin (<https://www.cygwin.com>) 
2.  在安装过程中,选择以下包.  (如果已安装Cygwin,请再次运行安装文件以安装其他软件包. ) 全新安装应该类似于[这个参考图片](https://ipfs.io/ipfs/QmaYFSQa4iHDafcebiKjm1WwuKhosoXr45HPpfaeMbCRpb/cygwin%20-%20install.png). 
    -   开发包
        -   `git`
        -   `make`
    -   存档包
        -   `unzip`
    -   网络包
        -   `curl`  
3.  在正常情况下运行以下内容`cmd`提示 (不是Cygwin提示,我们只需要Cygwin的工具) \
    下面是对该块的解释. 


    SET PATH=%PATH%;\cygwin64\bin
    mkdir %GOPATH%\src\github.com\ipfs
    cd %GOPATH%\src\github.com\ipfs
    git clone https://github.com/ipfs/go-ipfs.git
    cd %GOPATH%\src\github.com\ipfs\go-ipfs
    make install
    %GOPATH%\bin\ipfs.exe version --all

如果没有错误,则最终命令应输出类似于"`ipfs version 0.4.14-dev-XXXXXXX`"其中"XXXXXXX"应匹配当前的短哈希值`go-ipfs`回购. 您可以通过此命令检索所述哈希: `git rev-parse --short HEAD`. \
如果`ipfs.exe`执行并且版本字符串匹配,然后构建成功. 

|                                                                                                                             命令 | 说明                                                                                     |
| -----------------------------------------------------------------------------------------------------------------------------: | :------------------------------------------------------------------------------------- |
|                                                                                                `SET PATH=%PATH%;\cygwin64\bin` | 将Cygwin的工具添加到我们的工具中[`PATH`](https://ss64.com/nt/path.html);默认为:  (\\ cygwin64 \\ bin)  |
| `mkdir %GOPATH%\src\github.com\ipfs`<br/>`cd %GOPATH%\src\github.com\ipfs`<br/>`git clone https://github.com/ipfs/go-ipfs.git` | 获取/更新`go-ipfs`资源                                                                       |
|                                                                                      `cd %GOPATH%\src\github.com\ipfs\go-ipfs` | 改成`go-ipfs`源目录                                                                         |
|                                                                                                                 `make install` | 构建并安装到`%GOPATH%\bin\ipfs.exe`                                                          |
|                                                                                          `%GOPATH%\bin\ipfs.exe version --all` | 测试构建的二进制文件                                                                             |

要在更改源后再次构建,请运行: 

    SET PATH=%PATH%;\cygwin64\bin
    cd %GOPATH%\src\github.com\ipfs\go-ipfs
    make install

**小费: **避免设置`PATH`每次  (`SET PATH=%PATH%;\cygwin64\bin`) ,你可以永久锁定它`setx`在设置一次之后: 

    SETX PATH %PATH%

## 最小

虽然有可能建立`go-ipfs`同`go`单独,我们将使用`git`和`gx`用于实际的源管理. \
你可以使用任何版本的`git`你希望,但我们建议使用Windows版本<https://git-scm.com>. `git`必须在你的[`PATH`](https://ss64.com/nt/path.html)对于`go get`识别和使用它. 

### `gx`

您可以安装预建的二进制文件[`gx`](https://dist.ipfs.io/#gx)&[`gx-go`](https://dist.ipfs.io/#gx-go)如果它们适用于您的平台. 或者,您可以从源代码构建它们并将它们安装到`%GOPATH%\bin`通过运行以下内容: 

    go get -u github.com/whyrusleeping/gx
    go get -u github.com/whyrusleeping/gx-go

### `go-ipfs`

    SET PATH=%PATH%;%GOPATH%\bin
    go get -u -d github.com/ipfs/go-ipfs
    cd %GOPATH%/src/github.com/ipfs/go-ipfs
    gx --verbose install --global
    cd cmd\ipfs

我们需要`git`提交哈希将包含在我们的构建中,以便在极少数情况下发现错误,我们稍后会有一个参考点来跟踪它. 我们会问`git`为它并将其存储在变量中. 根据您是使用交互式命令行还是编写批处理文件,下一个命令的语法会有所不同. 使用适合您的那个. 

-   互动: `FOR /F %V IN ('git rev-parse --short HEAD') do set SHA=%V`  
-   解释: `FOR /F %%V IN ('git rev-parse --short HEAD') do set SHA=%%V`  

最后,我们将构建并测试`ipfs`本身. 

    go install -ldflags="-X "github.com/ipfs/go-ipfs/repo/config".CurrentCommit=%SHA%"
    %GOPATH%\bin\ipfs.exe version --all

您可以检查ipfs输出版本是否匹配`go version`和`git rev-parse --short HEAD`. \
如果`ipfs.exe`执行并且一切都匹配,然后构建成功. 

## 故障排除

-   **Git auth**如果您在使用Git时遇到身份验证问题,您可能需要查看<https://help.github.com/articles/caching-your-github-password-in-git/>并使用建议的解决方案: \
    `git config --global credential.helper wincred`

-   **还要别的吗**\
    请搜索[https://discuss.ipfs.io](https://discuss.ipfs.io/search?q=windows%20category%3A13)对于您可能遇到的任何其他问题. 如果您找不到任何现有的解决方案,请随时发布问题寻求帮助. 

如果你遇到了一个bug`go-ipfs`本身 (与建筑无关) 请使用[问题跟踪器](https://github.com/ipfs/go-ipfs/issues)举报. 
