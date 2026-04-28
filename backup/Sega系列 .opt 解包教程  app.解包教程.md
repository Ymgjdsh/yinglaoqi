保证小白看得懂（误）

**1.首先 获得.opt文件\.app文件**

### 2.下载 [unsegaREBORN](https://github.com/Elpisdev/unsegaREBORN)

在release 中 下载Mac edition or Windows edition （一个几mb的exe程序）

<img width="1245" height="467" alt="Image" src="https://github.com/user-attachments/assets/6ebe5e52-6054-487c-8d12-ffc360fd62f8" />
 或者通过此链接下载 https://drive.google.com/file/d/10wL7XTgE8voCDXBIZ45qsZjrzHCwESSv/view?usp=drive_link

### 3. 下载7-zip 以及 安装 NTFS 或者 EXFAT文件 插件

下载7-zip：不赘述
其次下载对应插件 这里以解包出EXfat为例 
 ExFat7z 是 7-Zip 这款流行压缩软件的小型插件。您可以使用 Exfat7z 和 7-Zip 来打开 ExFat **磁盘映像。
要将插件安装到 7-Zip 安装文件夹中，您需要创建一个名为“Formats”的子文件夹。之后，将 ExFat.64.dll 或 ExFat.32.dll（取决于您的 7-Zip 版本）复制到该子文件夹中 然后重启7-zip 此时可以直接双击打开或者解压EXfat文件

<img width="305" height="33" alt="Image" src="https://github.com/user-attachments/assets/dd992be7-4d9b-421e-a627-915573e4f9f0" />

### 3.获得更新包

将Exfat提取后 新建文件夹 将文件放入 并将文件夹名称改为 _A0xx_  随后 你可以使用此更新包进行游戏更新
注意 若缺少DataConfig文件 则无法正常显示版本号





预防补档内容：
SEGA系街机游戏/OPT解包的不完全指南
博主： Lemonno 发布时间：2025 年 08 月 19 日 577 次浏览 暂无评论 2746字数 分类： 默认分类
首页正文  分享到：  
本文章仅仅用于技术交流与探讨，请尊重版权，如内容侵犯到您的权益，请及时与我联系

首先感谢Azalea的这篇BlogMaimai 街机音游逆向！里面的教程大多有效，但部分步骤现在已经有了更好的解决方案，又因为我在这条路上踩了太多坑，所以才有了这篇文章

需要准备的工具
你需要解密的app原包文件（废话
fsdecrypt.exe
calculate_iv.py
RStudioPortable.exe
fsdecrypt.exe以及calculate_iv.py文件可前往SEGA Decryption Guide获取

出发咯~
以下内容已过时，虽然能用但不是最方便的解法，往下翻翻有新方法
前期步骤与SEGA Decryption Guide内的Readme文件一致，在此仅作大致说明
首先你需要一个包含了AES key的Bin文件，嗯？没有那种东西？在这里或许能找到你想要的

如果你不知道应该下载哪一个Bin文件的话，或许可以从app文件的名称找到线索

随后用16进制编辑器打开你的Bin文件（这里用Sublime Text演示）
可以从这里用16进制打开
可以从这里用16进制打开

随后换行写入EB 52 90 4E 54 46 53 20 20 20 20 00 10 01 00 00（如果你也使用Sublime Text的话，记得将大写字母转换为小写，并且使用英文输入法添加空格）并保存

在当前目录下打开cmd或者powershell窗口并执行下列指令

fsdecrypt .bin 0x200000 <path/to/app> <out.vhd>
其中 <PCB CODE>.bin应改为修改好的bin文件的文件名，<path/to/app>应改为app文件完整路径<out.vhd>应改为你想要的输出的文件的名字。

请注意应该去掉前后的‘<>‘再执行 运行完毕后，你的目录下应该会出现类似于out.vhd的文件。

随后转移到calculate_iv.py生成key 1
在这一步之前，请确保你的系统中有python环境。为了避免异常情况，你可以将该py文件删减至以下内容

import os
import glob

def byte_xor(ba1, ba2):
    return bytes([_a ^ _b for _a, _b in zip(ba1, ba2)])

print("You must decrypt the opt first using fstools and the OPT.bin\nPlace everything in the same directory\nONLY HAVE ONE VHD IN THE DIRECTORY AT A TIME")
cwd = os.getcwd()

with open(str(cwd) + "/exfat.bin", "rb") as f:
    exfat_HEADER = f.read(-1)
    print("exFAT Header = " + str(exfat_HEADER.hex()))

placeholder = glob.glob("*.vhd")
vhd = str(placeholder[0])
with open(str(cwd) + "/" + vhd, "rb") as f:
    key1 = f.read(16)
    print("key1 =" + str(key1.hex()))

​
随后运行（请保证py文件和vhd文件处于同一目录下）

python calculate_iv.py
​
然后你应该会看见key1的内容，将他复制下来，并打开Bin文件，替换掉你刚才写入的内容，并再次运行fsdecrypt的指令

至此，你将得到一个解密过后的VHD文件

试试更快速的方法？
你也可以使用unsega.exe来进行快速解密

unsega的使用方法很简单，将app文件拖动到unsega.exe图标上就能完成整个解密过程。

随后再进行下面的流程即可

注意注意~
至此，你可以切换至RStudio进行后续操作，你也同样可以使用Azalea Blog内的内容提取文件，但同样你也可以使用本Blog的教程在Windows环境下完成操作。
打开RStudio，点击左上角驱动器，选择打开镜像，并找到你的vhd文件打开

如果你的app文件是大版本更新的数据包，那么右侧应该为internal_0
如果你的app文件是大版本更新的数据包，那么右侧应该为internal_0

但如果你和我一样，打开后发现是internal_1.vhd的话，则需要你去找到当前版本的大版本app文件进行同样的解包操作。 比如，你当前操作的游戏版本为1.41，那么你就需要找到1.40的app文件，解密后得到internal_0.vhd文件，随后再在RStudio里面打开internal_1.vhd，并选择internal_0.vhd文件打开，你就能得到完整的文件了。

至于游戏的脱壳操作，还请移步至Maimai 街机音游逆向！进行更深入的研究。
opt文件我还没有实际操作过，等有机会再更新吧
> [!NOTE]
> 教程部分来源自 https://fragrance.moe/intro.html 
                              https://manalogues.com/posts/2024/02/26
                              https://blog.chongxi.us/2025/08/27/toolsForMaimai/

https://lemonno.xyz/archives/18.html

持续更新中，侵权请联系我删除



</html>关于舞萌科技的杂谈以及原理分析

Chongxi
admin
  2025-08-27 08:00 创建  2025-12-18 15:15:49 更新  [TECH]

本文中提到的舞萌DX 均为华立科技在中国大陆的代理版本

本文原为：杂谈 mai 科技相关知识以及第三方工具使用指南，现拆分为多篇文章以区分层次

本文仅作为 maimai 深层次的相关研究，仅供学习参考交流使用，主要目的是向广大舞萌玩家科普基本常识，教各位如何保护自己的 Net 账号，并演示你的账号是如何被挂哥毁掉的。本文不支持任何开挂作弊行为。

在此感谢每一位在 GitHub 等平台公开科技的各路神仙

1. 基本概念
1.1 SGWCMAID
在登录舞萌DX机台时，需要通过「舞萌 | 中二」公众号获取二维码。长按二维码解析后的字符串即为 SGWCMAID。

严重警告

绝对不要在任何公开场合泄露您的 SGWCMAID

请仅向您信任的人员或服务提供 SGWCMAID。

如果他人获取了您的 SGWCMAID，则意味着对方拥有您的舞萌账号操作权限，可在有效登录时效期内登入您的账号。

1.2 登录时效
SGWCMAID 的页面底部会显示二维码的有效期提示。过期后，二维码无法再用于机台登录，需生成新的二维码。

二维码有效期：约 10 分钟

账号登录时效：约 30 分钟 (2025/08/27 测定)

当距离上一次二维码获取已超过约 30 分钟时，账号会进入「冻结」状态，任何方式均无法登录

该状态会在生成新的二维码后解除

这是对账号的一道保护机制，防止攻击者滥用

1.3 User ID
User ID 并不是好友代码，而是舞萌国身份证 账号标识，与 SGWCMAID 关联

通过 SGWCMAID 可以获取对应的 User ID

拥有 User ID 的同时，也意味着拥有操作该账号的权限，可用于登录或对你账号进行 G 键开挂

舞萌 DX 的 User ID 为顺序计数，开头固定
所以 User ID 可被用作遍历攻击，这就说明了挂哥是如何给你的账号开挂的，他们通过遍历 User ID 来登入你的账号，如果你的账号恰好在登录时效内且处于未登录状态，那么你就倒霉了，所以说，登录时效是华立最后的底裤，如果没了，任何人的账号都可以随时被登录
1.4 小黑屋
舞萌服务器规定的登录会话超时为 15分钟
登录时必须使用生成时的时间戳，登出也必须使用对应的时间戳
如果没有正常登出（如因服务器丢包、高延迟或异常宕机），账号就会进入我们所说的小黑屋，只能等会话超时自动过期 / 用科技解除
这是服务器防止会话滥用的一种保护机制
但是由于舞萌服务器延迟较高，实际小黑屋持续时间可能会大于 15 分钟
此部分相关原理说明
2. 科技
舞萌的科技多种多样，严格意义上，HDD,Bot, 查分器 , 开挂等都算科技，因为他们都或多或少直接使用非正规渠道获取了服务器信息 / 程序本体，只是影响好坏的问题

我们先着重讲外挂，这是每个 maimai 玩家都该担忧的问题

2.1 外挂
目前我们所熟知的外挂有以下作用：

传分 往账号中写入指定的乐曲成绩
下埋 批量写入 (指定难度 / 版本等) 成绩
发票 向您的账号中发放「补偿」的 2/3/4/5/6 倍进度票
解歌 解锁被锁定的乐曲 (比如紫谱难度)
解图 解锁地图 (如月面区域)
跑图 顾名思义
签到 签到集章卡
解锁收藏品 包括但不限于 姓名框 / 称号 / 头像 / 搭档 / 背景板 / 功能票
修改舞里程 DX2025 更新的舞里程商店，可用里程购买功能票等道具
你的号是怎么被开挂的
如何保护自己的账号

不在不信任的公开场合发送您的二维码 / SGWCMAID
不在非出勤时间随意获取二维码
发 b50 尽可能隐藏掉昵称等不必要信息
2.2 HDD/app
舞萌 DX 机台运行的游戏程序本体，app 是官方机台运行的游戏程序，HDD 一般用于在手台等非官方机台上运行，可能还会带有部分 mod 功能，比如 Auto Play

此部分带来的法律风险由用户自己承担

2.3 opt
服务器向机台下发的更新会以.opt 形式呈现，其中包含此次下发的更新内容，例如乐曲数据等信息

下发时间 opt 下发并通知机台下载此更新的时间
发布时间 机台应用本次更新的时间

机台即使下载好了 opt 也不会立刻更新，需要满足发布时间才会更新

关于国服 2025 部分杂谈
2.4 第三方服务器
目前根据笔者已知有以下第三方服务器：

转发服务器：作中转用途，作为中间人代理以加速华立服务器的加载速度
纯粹的私服
2.5 第三方查分器 /bot
主要用途是帮助玩家了解自己的 Best50 等游玩成绩，目前主流查分器有落雪查分器与水鱼查分器 ,bot 的话太多难以统计，主要也是此用途

2.6 手台
玩家第三方自制、高度模拟官方机台的机器

3. 备注
关于第三方查分器使用已迁移到新的文章分篇，后续会补

关于挂哥扫号实例请看本博客下的此文章: mai 纪事：9 月大规模科技扫号和国服万花筒事件

标题: 关于舞萌科技的杂谈以及原理分析
作者: Chongxi
创建于 : 2025-08-27 08:00:00
更新于 : 2025-12-18 15:15:49
链接: https://blog.chongxi.us/2025/08/27/toolsForMaimai/
版权声明: 本文章采用 CC BY-NC-SA 4.0 进行许可。
聊聊 Android 上五花八门的浏览器