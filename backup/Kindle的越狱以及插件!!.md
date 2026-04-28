越狱方法
[https://www.bilibili.com/video/BV1VZrLYyEfX/?spm_id_from=333.337.search-card.all.click&vd_source=51ac3392cf2fd955a04a1bc24fd998e0](url)
这个要求我们关注公众号获得插件
我们当然是拒绝啦
整个越狱不超过10min 不过没必要刷安卓了 太卡了
我整理了一些必要的插件
_下载地址[https://wwuv.lanzouw.com/iFFYN2tgnsfe_
2](url)
> [!NOTE]
> 注意，如果你的 Kindle 固件是 5.16.3 或更新版本，需要使用支持 HF（hard float）的插件。


目录
一、MobileRead Package Installer (MRPI) — 插件安装器（必须）
二、KUAL — 插件程序启动器（推荐）
三、Koreader — 第三方电子书阅读器
四、ScreenSavers Hack – 更换 Kindle 屏保
五、Fonts Hack – 更换 Kindle 字体
六、USBNetwork Hack – 无线管理 Kindle
七、File Browser – 便捷管理 Kindle 文件
八、Kindle Python – 让 Kindle 支持 Python 程序
九、Helper – 小工具集合
十、不过瘾？可自行获取更多增强插件
注意，本文会用到一些扩展名为 .xz 的压缩文件，由于有些解压缩软件会损坏解压的文件，因此对于解压缩软件，Windows 系统推荐使用 7-zip，macOS 推荐使用 Keka（或命令行工具 tar）。

如今后遇升级固件插件失效，请参考《Kindle 升级到新固件后如何恢复越狱和插件》这篇文章。

下载插件时推荐通过“官方页面”下载，以便获取插件的最新版本。如果某款插件安装失败，可以查看一下 Kindle 根目录的 ⁨extensions/MRInstaller⁩/⁨log⁩/mrinstaller.log 这个日志文件，可以为你提供解决问题的有效线索。

一、MobileRead Package Installer (MRPI) — 插件安装器
MobileRead Package Installer 是一款 KUAL 插件。因为现在 Kindle 固件不支持直接把插件文件以刷入 bin 的方式安装，所以需要通过 KUAL 的这个插件 MRPI 来安装。

下载 MRPI：官方页面 ｜ 百度网盘〈提取码 : 6666〉
下载 MRPI（支持 HF 版本）：官方页面 ｜ 百度网盘〈提取码 : 6666〉
官方指南：KUAL: Kindle Unified Application Launcher (v 2.6)
★ 安装步骤：

用 USB 数据线将 Kindle 连接到电脑上，直到出现 Kindle 磁盘；
解压缩下载到的 kual-mrinstaller-xxx.tar.xz 得到一个文件夹；
把文件夹内的 extensions 和 mrpackages 拷贝到 Kindle 的根目录。
注意，如果根目录已有 extensions 这个文件夹，可以只把解压得到的 extensions 文件夹中的内容拷贝到 Kindle 根目录原有的 extensions 文件夹内，以避免原文件夹内的其它文件被删除。

> [!TIP]
> 另外，值得一提的是，如果你需要安装多个插件（比如本文之后所介绍的那些插件），不必重复每一款插件的安装步骤，只需要将所有 bin 文件拷贝到 mrpackage 目录，然后通过 ;log mrpi 命令一次性安装它们。这样，每当需要重新安装插件时，可以节省大量时间。

特别提示：如果你在安装完 MRPI 后使用命令 ;log mrpi 安装其它插件时看到“MRPI is not installed”的提示，极有可能是因为某些解压缩软件（如 WinZip）解压 .xz 格式的 MRPI 插件压缩包时破坏了 MRPI 相关文件导致的。为避免此问题，如果你使用的是 Windows 系统，请使用 7-zip 解压，如果你使用的是 macOS 系统，请使用 Keka 解压（或命令行工具 tar 解压）。详见小伙伴“就爱茄子”的留言及相关讨论。

二、KUAL — 插件程序启动器
KUAL (即 Kindle Unified Application Launcher)，是一款插件启动器。安装 KUAL 之后，你可以下载或自己编写插件并通过 KUAL 启动。比如用来启动 Koreader 之类的插件程序、让电量显示百分比等。

以下是 KUAL 的两种安装方法，请根据自己的 Kindle 型号选择合适的安装步骤。

安装方式一：
KO 1/2/3、KPW 4/5、Kindle 8/10 按照以下步骤安装 KUAL：

下载 coplate 版本 KUAL：官方页面 ｜ 百度网盘〈提取码 : 6666〉
用 USB 数据线将 Kindle 连接到电脑上，直到出现 Kindle 磁盘；
先按照第一部分提供的方法安装 MobileRead Package Installer (MRPI)；
然后解压缩下载到的 KUAL-xxxxxxx-20xxxxxx.tar.xz 得到一个文件夹；
在文件夹中找到 Update_KUALBooklet_xxxxxxx_install.bin 文件，拷贝到 Kindle 根目录下的 mrpackages 文件夹，然后在 Kindle 搜索框中输入 ;log mrpi 点击回车；
这时会调用 MRPI 安装 KUAL，安装完成并等待 Kindle 重启完毕后即可使用 KUAL。
安装方式二：
Kindle 7、KPW 1/2/3、KV 按照以下步骤安装 KUAL：

下载 KUAL：官方页面 ｜ 百度网盘〈提取码 : 4kb1〉
官方指南：KUAL: Kindle Unified Application Launcher (v 2.6)
★ 固件版本大于 5.8.x 的安装步骤：

用 USB 数据线将 Kindle 连接到电脑上，直到出现 Kindle 磁盘；
先按照第一部分提供的方法安装 MobileRead Package Installer (MRPI)；
然后解压缩下载到的 KUAL-v2.x.xx-xxxxxxxx-20xxxxxx.tar.xz 得到一个文件夹；
在文件夹中找到 Update_KUALBooklet_v2.x.xx_install.bin 文件，拷贝到 Kindle 根目录下的 mrpackages 文件夹，然后在 Kindle 搜索框中输入 ;log mrpi 点击回车；
这时会调用 mrpi 安装 KUAL，安装完成并等待 Kindle 重启完毕后即可使用 KUAL。
★ 固件版本小于 5.8.x 的安装步骤：

用 USB 数据线将 Kindle 连接到电脑上，直到出现 Kindle 磁盘；
解压缩下载到的 KUAL-v2.x.xx-xxxxxxxx-20xxxxxx.tar.xz 得到一个文件夹；
在文件夹中找到 KUAL-KDK-2.0.azw2 拷贝到 Kindle 的 documents 文件夹中；
弹出 Kindle 磁盘并进入 Kindle 界面，即可看到 KUAL（如下图所示）。
成功安装 KUAL 后，我的图书馆中会出现一个名为 KUAL 的个人文档图标，正常情况下，点开此图标应显示菜单。

 

▲ KPW4 成功安装 KUAL 后显示的图标，以及打开后显示的菜单

三、Koreader — 第三方电子书阅读器
Koreader 这款软件采用图像分割再重排的方式处理 PDF 文档（包括扫描和非扫描页面），这样不仅支持文字版 PDF 重排和数学公式的重排，还能对扫描版 PDF 和 DJVU 文档进行重新排版。重新排版后的文档，文字放大后可以适应屏幕自动换行，免去不断地左右拖动页面阅读。

下载 Koreader：官方页面 ｜ 百度网盘〈提取码 : 8ehi〉
下载 Koreader（支持 HF 版本）：官方页面｜ 官方链接
官方指南：在Kindle上安装和运行KOReader
注意，Koreader 提供了三种版本，对应不同的 Kindle 设备型号，请按需选择：

Legacy：K2、DX、K3（及其它差异化版本）
Kindle：K4、K5、KPW1
PW2：KPW2 后的所有版本（如 Kindle 7/8/10、KPW 2/3/4/5、KO 1/2/3、KV）
★ 安装步骤：

首先确保安装了 MRPI 和 KUAL；
用 USB 数据线将 Kindle 连接到电脑上，直到出现 Kindle 磁盘；
解压缩下载到的 Koreader 压缩包，可得到 extensions 和 koreader 两个文件夹；
先把文件夹 extensions 中的内容拷贝到 Kindle 根目录下的 extensions 文件夹中；
然后把文件夹内的 koreader 文件夹拷贝到 kindle 根目录下；
通过 KUAL 菜单中启动 Koreader 并用它的文件浏览器打开并阅读电子书。
* 提示1：汉化 Koreader 菜单可下载 menu.json，替换根目录的 \extensions\koreader\menu.json。
* 提示2：Koreader 的使用方法请参考《Koreader —— Kindle 的 PDF 文档重排插件》这篇文章。

另外，作为可选步骤，你还可以安装 KPVBooklet，其用途是在 Kindle 中直接显示原生系统不支持的 EPUB 等格式，并将其打开方式自动关联到 Koreader（还可通过 KUAL 菜单关联更多格式）。注意，由于 KPVBooklet 已很久未更新，可能不兼容新版本固件中（即 2017-10-27 之后发布的固件）。

下载 KPVBooklet：官方页面 ｜ 百度网盘〈提取码 : ts46〉
★ 安装步骤：

解压缩下载到的 kpvbooklet 压缩包，得到一个文件夹；
把文件夹内的 update_kpvbooklet_xxx_install.bin 拷贝到 Kindle 里 mrpackages 文件夹中；
弹出 Kindle 磁盘，进入 Kindle 界面，打开 KUAL，依次点击菜单【Helper → Install MR Packages】（或在搜索栏输入 ;log mrpi 并回车）；
耐心等待 kpvbooklet 安装，直到安装完成后 Kindle 重启完毕。
如果因升级到最新版本固件或未知原因导致此插件不能使用的，重新操作以上安装步骤即可恢复。

四、ScreenSavers Hack – 更换 Kindle 屏保
* 提示：此插件与 Kindle 原生的封面屏保功能有冲突，如仍想使用该功能不建议安装。

除非开启“广告”或开启封面屏保功能，Kindle 的默认屏保总是一成不变的。你可以通过安装这款插件实现自定义屏保，让 Kindle 在息屏休眠时，显示你精心挑选的图片。

下载 linkss：官方页面 ｜ 百度网盘〈提取码 : b2vk〉
官方指南：Kindle Touch/PaperWhite ScreenSavers Hack
★ 安装步骤：

首先确保关闭了广告特惠，并且安装了 MRPI 和 KUAL；
用 USB 数据线将 Kindle 连接到电脑上，直到出现 Kindle 磁盘；
解压缩下载到的 kindle-linkss-0.25.N-rxxx.tar.xz，得到一个文件夹；
把文件夹内的 Update_linkss_0.25.N_install_pw2_kt2_kv_pw3.bin 拷贝到 Kindle 里 mrpackages 文件夹中（如果是 KPW1 或 Touch 请选择另外那个 bin 文件）；
弹出 Kindle 磁盘，进入 Kindle 界面，打开 KUAL，依次点击菜单【Helper → Install MR Packages】（或在搜索栏输入 ;log mrpi 并回车）；
耐心等待 linkss 安装，直到安装完成后 Kindle 重启完毕；
再次用 USB 数据线将 Kindle 连接到电脑上，直到出现 Kindle 磁盘；
在 Kindle 根目录下会出现一个名为 linkss 的文件夹，把你想要设为屏保的图片放到该文件夹下的 screensavers 文件夹中即可。需要注意的是，屏保图片应按照如 bg_ss00.png、bg_ss01.png … bg_ss19.png … 这样的序列方式命名。屏保图片的规格请参照下面所列参数。
★ 屏保规格：

为达到更好的视觉效果，建议屏保图片按照下面不同设备相对应的图片尺寸制作：

Kindle 2/3/4/5/7/8/10：PNG 格式，宽高 600*800 像素
KPW 1/2：PNG 格式，宽高 758*1024 像素
KO1、KV、KPW 3/4：PNG 格式，宽高 1072*1448 像素
KO 2/3：PNG 格式，宽高 1680*1264 像素
KPW5：PNG 格式，宽高 1236*1648 像素
你可以参考《制作 Kindle 屏保图片三步走：打开、调整和保存》这篇文章制作屏保图片。也可以前往“Kindle 屏保图册”下载 Kindle 伴侣为你制作好的屏保图片。

如果制作的 png 图片无法正常使用，请尝试将屏保图片处理成 8 位深度的灰度图。需要注意的是，请不要把一个 jpg 图片通过更改后缀名的方式更改成 png，这样得到的仍然是无法使用的 jpg 图片。

如果因升级到最新版本固件或未知原因导致此插件不能使用的，请备份一自定义屏保图片，然后重新操作上面的第 1~7 步骤，重启后重新把屏保图片拷贝到 screensavers 文件夹中即可恢复。另外，在测试时发现安装 usbnet 这款插件后会影响到 linkss 屏保插件，同样重复第 1~7 步骤即可恢复。

* Kindle 原生壁纸路径：/usr/share/blanket/screensaver/

五、Fonts Hack – 更换 Kindle 字体
* 提示：Kindle 已原生支持自定义字体（详情），无需安装此插件。

Kindle 自带了四种简体中文字体，两款繁体/正体中文字体，如果感觉这些字体不能满足你的阅读需要或审美情趣，就可以使用这款插件为 Kindle 增加你喜欢的字体。

*注意，文件名中带有设备名，不同的 Kindle 设备请使用相应的 bin 文件。

下载 Python：官方页面 ｜ 百度网盘〈提取码 : w875〉
下载 linkfonts：官方页面 ｜ 百度网盘〈提取码 : wmcz〉
官方指南：Kindle Touch/PaperWhite 5.3.x – 5.4.x Fonts Hack
注意，目前的使用自定义字体只能用替换当前字体的方法。

★ 安装步骤：

第一部分：安装 Kindle Python 和 linkfonts

首先确保安装了 MRPI 和 KUAL；
用 USB 数据线将 Kindle 连接到电脑上，直到出现 Kindle 磁盘；
解压缩下载到的 kindle-python-0.xx.N-rxxxxx.tar.xz 和 kindle-linkfonts-0.xx.N-rxxxxx.tar.xz，得到两个文件夹；
分别将两个文件夹内的 Update_python_0.xx.N_install_pw2_and_up.bin 和 Update_linkfonts_0.xx.N_install_pw2_and_up.bin 拷贝到 Kindle 根目录中的 mrpackages 文件夹中；
弹出 Kindle 磁盘，进入 Kindle 界面，打开 KUAL，依次点击菜单【Helper → Install MR Packages】（或在搜索栏输入 ;log mrpi 并回车）；
耐心等待 Kindle Python 安装，直到安装完成后 Kindle 重启完毕；
第二部分：拷贝字体 & 修改配置文件

重新用 USB 数据线将 Kindle 连接到电脑上，直到出现 Kindle 磁盘；
在 Kindle 根目录下可以找到名为 linkfonts 的文件夹，把 .ttf 格式的字体文件拷贝到该文件夹下的 fonts 文件夹中；
然后进入 etc 文件夹中，将文件 fc-override.tpl 复制一份到 conf.d 文件夹中，重命名为 100-override-chinese.conf（可使用任意文件名，只要开头是数字即可），注意必须将扩展名 .tpl 要更改为 .conf（如果系统隐藏了扩展名，请先通过 Windows 的资源管理器或 macOS 的访达设置显示文件的后缀名）；
使用文本编辑器（不要用记事本，推荐使用 Sublime Text 等专门的代码编辑器）打开重命名后的文件，将其中的 %TO_OVERRIDE% 替换成 STSong、STKai、STHeiti、STYuan 中的一个（分别对应系统字体中的 宋体、楷体、黑体、圆体）；把 %TO_USE% 改成要使用的字体的字体名称 (注意，要用字体的字体族名，而不是 .ttf 文件的文件名，连带 % 也替换掉)，修改完毕后保存文件。
弹出 Kindle 磁盘，进入 Kindle 界面，打开 KUAL，依次点击菜单【Fonts → Fonts Hack Behavior → Update fontconfig cache】，待刷新配置并重启 Kindle 完毕后，即可成功替换字体。
以上步骤操作完成并确认安装成功之后，可以查看《Kindle 中文字体推荐：更换一下字形口味》这篇文章，看看有没有自己心仪的字体。

如果因升级到最新版本固件或未知原因导致此插件不能使用的，重新操作第一部分步骤恢复。

* 如何找到 .ttf 文件的字体族名？如果是 Windows 系统，请安装“字体试衣间”之类的字体管理软件获取字体的字体族名；如果是 Mac 系统，双击打开字体文件，窗口标题显示的即是字体的字体族名。

六、USBNetwork Hack – 无线管理 Kindle
USBNetwork 可以让我们通过 WiFi 直接连接到 Kindle 并对其进行传送文件、管理等操作，就像管理 FTP 一样，这样就可避免为了管理文件反复在 Kindle 上插拔 USB 数据线。

具体安装及使用方法可参考《USBNetwork Hack 安装教程：无线管理 Kindle 文件》这篇文章。

七、File Browser – 便捷管理 Kindle 文件
这款插件能在 Kindle 中启动一个 WEB 服务器，方便你在任意设备中（如手机、平板或电脑）通过任意网页浏览器浏览、上传、下载和管理 Kindle 设备中的文件。具体安装及使用方法可参考《File Browser：便捷地管理 Kindle 中的文件》这篇文章。

八、Kindle Python – 让 Kindle 支持 Python 程序
如果你要安装的插件含有 Python 脚本，则需要 Kindle 具备解释 Python 程序的功能，

下载 Python：官方页面 ｜ 百度网盘〈提取码 : w875〉
★ 安装步骤：

首先确保安装了 MRPI 和 KUAL；
用 USB 数据线将 Kindle 连接到电脑上，直到出现 Kindle 磁盘；
解压缩下载到的 kindle-python-0.xx.N-rxxxxx.tar.xz，得到一个文件夹；
将文件夹内的 Update_python_0.xx.N_install_pw2_and_up.bin（如果你想使用 Python 2.x）或 Update_python3_0.xx.N_install_pw2_and_up.bin（如果你想使用 Python 3.x）拷贝到 Kindle 根目录中的 mrpackages 文件夹中；
弹出 Kindle 磁盘，进入 Kindle 界面，打开 KUAL，依次点击菜单【Helper → Install MR Packages】（或在搜索栏输入 ;log mrpi 并回车）；
耐心等待 Kindle Python 安装，直到安装完成后 Kindle 重启完毕。
注意，安装完成后出现 Success 字样然后重启才算安装成功。如果出现任何带 Fail 字样的提示就表示安装失败，一般是存储空间太小的原因，请检查 Kindle 空间是否留足了 200 MB 的空间。

九、Helper – 小工具集合
Helper 是一个小工具集合，里面有两个比较有用的小工具，分别是“PREVENT ScreenSaver”和“ALLOW ScreenSaver”，前者的作用是禁止 Kindle 休眠（禁用屏保），后者是恢复 Kindle 休眠（启用屏保）。

下载 kual-helper：官方页面 ｜ 百度网盘〈提取码 : b86h〉
首先确保安装了插件 KUAL。解压缩 kual-helper-0.5.N-xxx.tar.xz ，在路径 kual-helper-0.5.N/extensions 下找到 helper 文件夹，将其拷贝到 Kindle 中的 extensions 文件夹中即可。

然后进入 KUAL，点击【Helper+】进入小工具集合，点击【PREVENT ScreenSaver】即可禁止 Kindle 休眠，点击【ALLOW ScreenSaver】即可恢复 Kindle 休眠。
https://bookfere.com/post/311.html（ 转载地 ） 

![神奇的Kindle](https://github.com/user-attachments/assets/ff4ab614-6a76-4510-963e-5d6cb96cfe0f)