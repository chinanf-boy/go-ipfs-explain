# go-ipfs@0.4.16-rc3 [![explain](http://llever.com/explain.svg)](https://github.com/chinanf-boy/Source-Explain)

「 ipfs 协议 主实现 软件 , go语言 」

[github source tag](https://github.com/ipfs/go-ipfs/releases/tag/v0.4.16-rc3)

[中文](./readme.md) | ~~[english](./readme.en.md)~~

欢迎 `Issue` 和 `Pull` ❤️, 最好 `Pull` 👏

---

## 生活

[help me live , live need money 💰](https://github.com/chinanf-boy/live-need-money)

---

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [ipfs/ipfs](#ipfsipfs)
- [ipfs/go-ipfs/readme.md](#ipfsgo-ipfsreadmemd)
  - [想看看我们的代码？](#%E6%83%B3%E7%9C%8B%E7%9C%8B%E6%88%91%E4%BB%AC%E7%9A%84%E4%BB%A3%E7%A0%81)
  - [Main](#main)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

---

协议的实现是复杂的, 我们从`go-ipfs`的`readme.md`中找到了开始的文件

## ipfs/ipfs

如果你对`ipfs/ipfs`的协议说明感兴趣,~~[可以看看>中文🇨🇳<][ipfs-zh]~~~

[ipfs-zh]: https://github.com/chinanf-boy/ipfs-zh

## ipfs/go-ipfs/readme.md

如果你对`ipfs/go-ipfs`的 **readme** 感兴趣,[可以看看>中文🇨🇳<][go-ipfs-zh]

[go-ipfs-zh]: https://github.com/chinanf-boy/go-ipfs-zh

### 想看看我们的代码？

有些地方可以帮助你入门。（WIP）

Main 文件: [cmd/ipfs/main.go](https://github.com/ipfs/go-ipfs/blob/master/cmd/ipfs/main.go) <br>
CLI 命令行: [core/commands/](https://github.com/ipfs/go-ipfs/tree/master/core/commands) <br>
Bitswap (the data trading engine) 改造的bit协议: [exchange/bitswap/](https://github.com/ipfs/go-ipfs/tree/master/exchange/bitswap)

DHT: https://github.com/libp2p/go-libp2p-kad-dht <br>
PubSub: https://github.com/libp2p/go-floodsub <br>
libp2p: https://github.com/libp2p/go-libp2p

### Main

用过`go-ipfs`都知道, 它的重点在于命令行的启动与使用

而`cmd`命令行,`/ipfs`协议,`/main.go`主文件的路径也就不为奇


