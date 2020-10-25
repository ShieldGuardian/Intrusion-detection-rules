ICMP（Internet ControlMessages Protocol，网间控制报文协议）是TCP/IP协议族的子协议，是一种面向无连接的协议.
经常使用的ping命令就是基于ICMP协议，windows系统下ping默认传输的是： abcdefghijklmnopqrstuvwabcdefghi，共32bytes.
linux系统下，ping默认传输的是48bytes，前8bytes随时间变化，后面的固定不变，内容为!”#$%&’()+,-./01234567.
ping的包大小，也就是data大小是可以修改的，改变操作系统默认填充的Data，替换成我们自己的数据,这就是ICMP隐蔽隧道的原理.

windows系统下ping默认传输的是：abcdefghijklmnopqrstuvwabcdefghi，16进制内容为：6162636465666768696a6b6c6d6e6f70717273747576776162636465666768694
inux系统下ping默认传输的内容，去掉开头可变的8bytes后是：!”#$%&’()+,-./01234567，16进制内容为：101112131415161718191a1b1c1d1e1f202122232425262728292a2b2c2d2e2f3031323334353637
对于正常的ping命令产生的数据，有以下特点：
每秒发送的数据包个数比较少，通常每秒最多只会发送两个数据包；
请求数据包与对应的响应数据包内容一样；
数据包中payload的大小固定，windows下为32bytes，linux下为48bytes；
数据包中payload的内容固定，windows下为abcdefghijklmnopqrstuvwabcdefghi，linux下为!”#$%&’()+,-./01234567，如果指定ping发送的长度，则为不断重复的固定字符串；
type类型只有2种，0和8。0为请求数据，8为响应数据。
对于ICMP隧道产生的数据，有以下特点：
每秒发送的数据包个数比较多，在同一时间会产生成百上千个 ICMP 数据包；
请求数据包与对应的响应数据包内容不一样；
数据包中 payload的大小可以是任意大小；
存在一些type为13/15/17的带payload的畸形数据包；
个别ICMP隧道工具产生的数据包内容前面会增加 ‘TUNL’ 标记以用于识别隧道。
因此，根据正常ping和ICMP隧道产生的数据包的特点，可以通过以下几点特征检测ICMP隧道:
检测同一来源数据包的数量。正常ping每秒只会发送2个数据包，而ICMP隧道可以每秒发送很多个；
检测数据包中 payload 的大小。正常ping产生的数据包payload的大小为固定，而ICMP隧道数据包大小可以任意；
检测响应数据包中 payload 跟请求数据包是否不一致。正常ping产生的数据包请求响应内容一致，而ICMP隧道请求响应数据包可以一致，也可以不一致；
检测数据包中 payload 的内容。正常ping产生的payload为固定字符串，ICMP隧道的payload可以为任意；
检测 ICMP 数据包的type是否为0和8。正常ping产生的带payload的数据包，type只有0和8，ICMP隧道的type可以为13/15/17。
