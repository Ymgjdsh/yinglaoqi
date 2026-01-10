**OpenWrt插件——应用过滤（OpenAppFilter）自定义特征库之法**

**原文发表于二〇二五年八月廿七，修订于二〇二六年元月初八｜DIY**

昔者，吾尝试诸OpenWrt网络管控插件，终独留「应用过滤」（OpenAppFilter）一器。此插件虽有VIP之制，供丰沛特征库，然吾所需者，仅限数站而已。故研习自添特征之法。若有亟需者，可购VIP以助开发者，资费三十有九，不亦廉乎？

**一、特征库文件**

先于此处下载无偿特征库：  
网址：https://www.openappfilter.com/#/feature  
解压后得三文件，中有二.bin文件为特征库。视其升级说明，可知二者之异。  
续解.bin文件，见feature.cfg与app_icons二目，其义自明。

**二、特征码格式**

特征库文件存诸APP特征码，乃未加密之文册，常为.cfg格式，可以文书编辑。  
特征库说明载于：https://github.com/destan19/OpenAppFilter/wiki/self%E2%80%90define-feature-file

特征码用以界定各APP之协议特征，如端口、域名、七层内容字典等，其式如下：  
`$id $name:[$proto;$sport;$dport;$host url;$request;$dict]`

- `$id`：APP独有编号，不可重复。  
- `$name`：APP之名，如“抖音”。  
- `$proto`：传输层协议，tcp或udp。  
- `$sport`：源端口，1-65535，空则匹所有，通常不设。  
- `$dport`：目的端口，1-65535，空则匹所有。  
- `$host`：HTTP/HTTPS请求之域名，如www.baidu.com。  
- `$dict`：七层内容字典，格式如`xx:aa|yy:bb`。其中xx、yy为位置（首位为0），aa、bb为十六进制内容。例：`00:a0|02:08|03:0a`，即第0位为0xa0，第2位为0x08，第3位为0x0a。若位置为负，则自末位起计，然通常勿用负数。

**三、自定义特征库**

开启feature.cfg，可见其内容如：

```
#class video 3 视频
3001 抖音:[tcp;;;-dy-;;,tcp;;;-dy.;;,...]
3006 斗鱼:[tcp;;;douyu;;,...]
……
```

可于同类中复制一APP特征，追加于该类之末。盖appid低三位为类内编号，高位为类id。如3001，其3为视频类，001即抖音编号。  
复制后首须改appid，务使组内唯一，宜取组内最大编号加一。例如今最大为3012，则新appid可设为3013。  
今欲增一网页游戏站poki.com，可添特征码如下：

```
2117 宝玩:[tcp;;;*.poki-cdn.com;;,tcp;;;poki.com;;,tcp;;;t.poki.io;;]
```

多网址以逗号相隔，其系为“或”。添毕，须更新文件首行之版本号。

另须取网站标徽之图，格式50×50 PNG。若难寻，可以他图暂代。图存于app_icons目录，名依appid而定。宜先察该目录内最大编号，以免重复。

**四、以浏览器析域名**

于PC端，用Chrome开发者工具甚便：

1. 启网站前，按F12，择Network标签。  
2. 勾选Preserve log，以保跳转后记录不失。  
3. 点击“🛑”止录钮或“⨯”清旧记。  
4. 于地址栏输入https://poki.com并回车。  
5. 观Network中Name/Domain列，可见如poki.com、*.poki.io等域名，即可循规添入feature.cfg。

**五、以Wireshark捕无域名之应用**

若应用无显著域名而具独特流量特征（如手游、加密协议），可以Wireshark捕包，取`$dict`所需字节特征。  
其法有二：

1. 以笔记本为热点，手机连之，直用Wireshark捕包分析。  
2. 于路由器上以tcpdump捕包，存为.pcap文件，后用Wireshark析之。

吾所编X86固件已含tcpdump插件，可直接捕包，得文件于`/tmp/tcpdump/cap/`。亦可于OpenWrt命令行安装tcpdump：

```
opkg update
opkg install tcpdump
```

安装后以终端指令捕包。详见：OpenWrt抓包

以Wireshark开启.pcap文件后，可设过滤条件，如专析IP为192.168.1.101之设备：

```
ip.addr == 192.168.1.101 && (http.host || tls.handshake.extensions_server_name)
```

于HTTPS握手包中，展Transport Layer Security → Extension: server_name，右键择Apply as Column，则主界面增Server Name一列，域名一览无遗。  
择该应用TCP/UDP会话，察数据包内容，如：

```
0000   a0 45 13 10 00 1c 00 00 00 03 01 0a 00 00 00 01
0010   4f 12 09 45 01 5d ...
```

对应`$dict`规则可为：`00:a0|01:45|02:13|03:10`

规匹之议：

- 位置宜靠前（前数十字节）。  
- 宜用固定字段（如协议标志）。  
- 避用IP、端口、会话ID等易变之数。  
- 可较数包，得固定字节序列。  
- 于加密通信（如HTTPS），可自Client Hello/SNI取字节。  
- 于WebSocket，可察握手包中独特字段。

吾于Wireshark捕包分析亦非熟手，不过临事而学耳。

**六、封.bin文件**

feature3.0_cn_20250316.bin虽解压即可自定特征，然如何重封为.bin？初以为直压后改后缀即可，实则不然。  
先析其构：

重命名为tag.gz后缀解压之
而后将修改后的feature文件替换到解压文件夹 
而后像我这样选中所有文件 并且用7zip将其压缩为tar文件
<img width="653" height="171" alt="Image" src="https://github.com/user-attachments/assets/8cab8ff4-70e9-4403-b504-bb02c44af589" />

而后 再用7zip对tar文件压缩 压缩选项选择gzip即可压缩成.tar.gz
然后改名成.bin后缀 即可导入插件

乃知此.bin实为gzip压缩文件。目录构如下：

```
feature/
├── feature.cfg
└── app_icons/
    ├── ...
```

进入feature目录，而后封包：

```
tar -cf feature.tar feature.cfg app_icons   # 先作tar包
gzip -c feature.tar > feature3.0_cn_20250822.bin   # 压为.bin格式
```

遂得新特征库文件feature3.0_cn_20250822.bin。可径于插件管理页面上传。

**七、吾之特征库分享**

吾所制特征库，添有宝玩游戏及数网盘。  
百度网盘：https://pan.baidu.com/s/1qcsD1XVwoLjC4J3vAwBh2A?pwd=hm8g  取码：hm8g

**八、OpenWrt X86固件**

吾所编X86固件，含应用过滤及网络管控插件，亦备诸科学上网工具：  
百度网盘：https://pan.baidu.com/s/1BTbtZJQvvUXtfwCAknNJdQ?pwd=xg1r  取码：xg1r

**九、应用过滤之疑难**

1. 所滤网址，或致他站不可访。如蔽数国内视频站，Google遂不能搜。其因未明，吾亦未得解方。（然时而复常）  
2. 此插件或碍Docker。若启应用过滤，容器或报500错。宜先启容器，后开插件。  
3. 若同启科学上网插件，则应用过滤中之站亦为代理之站，过滤遂无效。例如设外网皆走代理，则过滤库中所有外站仍可访。此吾未将外邦社媒、视频站添入特征库之故也。

**OpenWrt**


附加内容:
**拦截蛋仔派对**
终端运行
tcpdump -i br-lan host 10.0.0.183 -s 0 -w /tmp/eggparty.pcap
50s后 Ctr;+c
保存抓取数据
strings /tmp/eggparty.pcap | grep -E '\.(com|cn|net|org)' | grep -iE '(netease|egg|game|party)' | sort | uniq | head -20
分析数据 即可获得域名


**微信视频号特征码（来自吾爱破解，不确定有没有用）**
3127 微信视频号:[tcp;;;wxapp.tc.qq.com;/251/20302/stodownload;,tcp;;;video.qq.com;/251/20302/stodownload;,tcp;;;;;1a0:2f|1a1:73|1a4:64,tcp;;;;;1a1:2f|1a2:73|1a5:64,tcp;;;;;1a2:2f|1a3:73|1a6:64,tcp;;;;;1a3:2f|1a4:73|1a7:64,tcp;;;;;1a4:2f|1a5:73|1a8:64]