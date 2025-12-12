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

