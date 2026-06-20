# SDGB 舞萌 DX 懒人包完全技术指南

> [!WARNING]  
> **下载提醒**：此一般程度的垃圾教程并不直接提供 SDGB 懒人包下载链接，需要的朋友可以留意评论区（或发我 SDEZ 1.66）。  
> 如果你是自己拼的包，建议先阅读我的另一篇[文章](https://ymgjdsh.github.io/yinglaoqi/post/SDGB-de-jie-bao.html)，了解 Package 基本构造（不提供 .app 资源，这个东西其实不难找）。

---

##  目录

- [下载与存放](#download)
- [启动游戏](#start)
- [环境变量问题](#env)
- [灰网修复](#network)
- [卡更新/检查数据](#stuck)
- [摄像头配置](#camera)
- [MOD与作弊面板](#mod)
- [无摄像头扫码登录](#login)
- [游戏更新](#update)
- [自动游玩与全解锁](#autoplay)
- [ODD.SYS服务问题](#odd)
- [小数点版本更新](#dotupdate)
- [Melon Loader报错](#melon)
- [摄像头黑屏](#blackcamera)
- [狗号与标题服务器](#dog)
- [全屏与显示](#fullscreen)
- [MOD加载](#modload)
- [推荐工具](#tools)

---

<a id="download"></a>
## 📦 下载与存放

### 123 云盘问题
123下载需要付款？建议购买临时会员下载，目前123封锁了直链访问权，脚本失效了。

### 存放规则
下载后请存放到D盘，路径不可有中文。

---

<a id="start"></a>
## 1️⃣ 如何启动游戏？

双击点击启动乌蒙dx.exe即可。  
游戏内每个键都对应了不同的字母，比如Z,C,X等等，自己都按一遍就知道是哪个键了。

**如何投币？（aquamai）**  
按大键盘上`+`进行投币（也有可能是`8`），大键盘`9`为测试键。

**游戏启动没反应 / bat 打不开怎么办？**  
- 文件路径不能有中文  
- 请使用start.bat  
- 关闭杀毒软件  
- 游戏助手关一关  
- Win7及以下无法打开  
- 某些手台不支持（？）  
- 你的windows10时区不是中国  
- 你没有以管理员运行start.bat  
- 网络问题无解，版本更新，slim.ver缺失  

反正你按照我这个顺序逐一排查就对了。

---

<a id="env"></a>
## 2️⃣ 提示 odd xxxxx 找不到 sc 指令？？？

你的系统环境变量出了问题。去控制中心 → 高级设置 → 环境变量，Path里面看看 `%systemroot%` 是否完整。

---

<a id="network"></a>
## 3️⃣ 咋是灰网啊我去

如果你进入游戏的时候显示net坏，那么就是没有绿网。

**修复步骤**：  
如下路径 `C:\Windows\System32\drivers\etc` 找到 hosts文件，记事本打开，把里面东西全删了，改成下面这些：
```
129.28.248.89 wq.sys-all.cn
81.71.193.236 ai.sys-all.cn
42.193.74.107 wi.sys-all.cn
81.70.119.195 at.sys-all.cn
```
然后保存，再打开你的start.bat。关闭所有可能存在在你网络环境的vpn。

---

<a id="stuck"></a>
## 4️⃣ Net好，但是进去卡在更新或者检查数据100%？

<img width="721" height="493" alt="Image" src="https://github.com/user-attachments/assets/b4087441-ce8f-4f2c-8636-d0a0ca948d26" />

如上图，这是由于狗号所在机厅没有基准机导致的，问题不大。

**解决办法**：进入游戏的时候，按大键盘上的服务键（多为数字）进入测试菜单，然后选择游戏设置。

<img width="343" height="329" alt="Image" src="https://github.com/user-attachments/assets/71b67687-2927-4a62-a5b6-599333e71612" />

进去之后，把店内招募设置关闭。

<img width="571" height="561" alt="Image" src="https://github.com/user-attachments/assets/3051536b-f008-429d-8fa0-603daecea4b5" />

---

<a id="camera"></a>
## 5️⃣ 摄像头如何配置（笔记本似乎不能正常调用）

在SDGB文件夹 `/package/Sinmai-Assist` 里有一个 `config.yml`。  
**这里以大多数懒人包最常用的MOD为例，当然aquamai也差不多**。  
（什么？你没有Sinmai-Assist？请看第17条）

双击用VS CODE打开，然后往下滑你就可以看到配置参数。

**注意**：
1. 摄像头ID必须是纯数字，`D:\SDGB2026\Package\Sinmai-Assist\WebCameraList.txt` 查看你的ID
2. 扫码摄像头和玩家摄像头的ID不可以是一样的
3. 如果无法解决，尝试在config和Aquamai.toml中设置 `disableEncryption` 为 true，或者修改你的狗号（最好改成你所处地段机厅的狗号），再运行游戏尝试（下文有狗号修改教程）

---

<a id="mod"></a>
## 6️⃣ 如何开启 MOD（作弊cheat面板）并且扫码登录？

同样是上一个的操作，然后下滑找到modsetting，把showpanel后面的false改为true。然后找到dummylogin，把他后面也改成true。还有autoplay fastplay什么的，也是这样子开，面板才会显示。

---

<a id="login"></a>
## 7️⃣ 扫码登录，我没有摄像头怎么登录啊

**方案一（Token登录）**：
1. 打开微信舞萌dx公众号
2. 获得玩家二维码
3. 在那个界面长按二维码并且扫描
4. 获得字符串
5. 复制获得的字符串到你已经打开并且在扫描二维码页面的舞萌
6. 看到悬浮窗Dummylogin那里，在第一个大框Token下面填写你复制的字符串，然后点击Token Login，就会发现登录了
7. 玩游戏

**方案二（UserID登录）**：  
游戏玩一把之后，上传成绩，然后去你的userdataout文件夹（自己找找在哪里）获得userId。  
*Ps：可以从一些QQ BOT或者tgbot里获得userid，但同时你的账号信息有概率泄漏*。  
以后就可以用这个UserID直接在刚刚那个悬浮窗下面登录，但是前提是30min前刷新过二维码（不然会关你15分钟小黑屋）。

---

<a id="update"></a>
## 8️⃣ 如何更新？（有压缩包的情况，若只有opt文件请跳转到另一篇文章opt解包教程）

解压1.55 X更新包压缩包，你会看见例如“A071”的文件夹（不是就改成这样的格式比如A0xx），打开看一下里面有没有套娃，如果没有，就把文件夹丢到 `SDGB2026\Package\Sinmai_Data\StreamingAssets`，打开游戏就可以发现更新了（积累更新包必须一起放入）。

---

<a id="autoplay"></a>
## 9️⃣ 如何开启自动游玩 AUTOPLAY？如何解锁全部收藏品/歌曲/搭档？

**这里以大多数懒人包最常用的MOD为例，当然aquamai也差不多**。

在VScode中把cheat栏里autoplay调为true。启动游戏之后的左上角面板那里开AP、FC......最好打开disable mode update。

![Image](https://github.com/user-attachments/assets/7b4860d6-6bc3-4e21-be2a-a48dab131254)

把这个地方的false，看自己想要啥，改成true就行。

---

<a id="odd"></a>
## 🔟 odd.sys服务无法启用，如下

![挖槽！](https://github.com/user-attachments/assets/aebf1508-617e-402f-ad31-39904db7c65b)

不要慌张，下载NO ODD.SYS SEGATOOLS解决。  
下载：https://www.123912.com/s/2LjLVv-TUtwh   
解压后，直接全选文件夹里的文件，复制到 `D:\SDGB2026\Package` 并全部替换。  
随后，点击启动.bat后即可启动游戏。

或者，你的Windows系统环境出现问题。请在电脑高级设置中查看是否存在错误修改。

---

<a id="dotupdate"></a>
## 1️⃣1️⃣ 某些小数点版本更新

需要放置更新包，而且还要ICF文件（放置方法和第十条一样，替换源文件）。  
注意：防止更新包后需要等华立更新，否则灰网。

---

<a id="melon"></a>
## 1️⃣2️⃣ Failed to initialize Melon Loader......怎么办？

确保没有中文路径，并且游戏不是在中文文件夹里。

---

<a id="blackcamera"></a>
## 1️⃣3️⃣ 摄像头黑屏无法扫码？

1. 没有正确绑定摄像头ID，请绑定正确的ID。下面填入你的摄像头ID：
   ```
   chimeCameraId: 0
   leftQrCameraId: 0
   rightQrCameraId: 0
   photoCameraId: 0
   ```
2. 把摄像头清晰度设置成640x480再启动游戏
3. 在Aquamai.toml中调整相关配置
4. 更改屏幕分辨率
5. 笔记本用户一般无法正常调用摄像头，可以尝试外接摄像头？

---

<a id="dog"></a>
## 1️⃣4️⃣ 标题服务器怎么坏了，怎么传不上分了

因为你狗号坠机了，或者填写错误了，或者你用了上面的无odd包。

**解决方法**：打开Package里的segatools.ini，找到：

<img width="199" height="115" alt="Image" src="https://github.com/user-attachments/assets/b1a8c562-0f5d-4ee0-9ca8-53589c0393ee" />

看到ID了吗，那个就是你的狗号，你需要去找一个正确的狗号并且填上去，就可以解决这个问题（别看了狗号自己找汤小云要，我这个是假的，当然找人发你狗表也可以）。

最后（VPN）请关闭一切网络代理，否则无法连接国内服务器。

---

<a id="fullscreen"></a>
## 1️⃣5️⃣ 如何全屏

Alt+回车，然而触摸鼠标可能存在BUG。

---

<a id="modload"></a>
## 1️⃣6️⃣ 如何加载Sinmai-Assist.dll等Mod？

确保你已经创建了package下的Mods文件夹，将.dll后缀的文件拖入Mods文件夹即可。

---

<a id="tools"></a>
## ⭐ 推荐工具

#EX>>** https://github.com/clansty/MaiChartManager   
很好的模组和铺面管理器，同时也是音乐播放器~

![Image](https://github.com/user-attachments/assets/424e634d-8122-4ea4-8d37-a49aa314c034)

**吊图一大堆**

---

_bing引擎能搜到此文章（2026.6.20）_

_大家可以在评论区交流技术之类的~_

---

> *本教程手搓后经过AI处理。*