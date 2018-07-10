
## / ws和/ wss  -  websockets

如果您希望浏览器连接到例如`/dns4/example.com/tcp/443/wss/ipfs/QmFoo`

-   [ ] 与之匹配的SSL证书`/dns4`要么`/dns6`名称
-   [ ] go-ipfs听`/ip4/127.0.0.1/tcp/8081/ws`
    -   8081就是一个例子
    -   请注意它`/ws`在这里,不是`/wss`-  go-ipfs目前无法执行SSL,请参阅下一点
-   [ ] nginx的
    -   使用SSL证书配置
    -   听443号港口
    -   转发到127.0.0.1:8081
