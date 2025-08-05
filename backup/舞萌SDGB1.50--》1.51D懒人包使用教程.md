下载SDGB **：由于有SB急眼天天发qq邮件给我， 所以现在不出示下载链接,需要的可以等人发**
下载需要付款？
如果123限制下载额度用这个油猴插件绕开https://greasyfork.org/zh-CN/scripts/520017-%E6%94%B9-123-%E4%BA%91%E7%9B%98%E4%BC%9A%E5%91%98%E9%9D%92%E6%98%A5%E7%89%88 


下载后请存放到D盘
 
 按大键盘上8进行投币
)1.如何启动游戏？

双击点击启动乌蒙dx.exe即可

2.提示odd xxxxx 找不到sc指令？？？ 
你的系统环境变量出了问题 去控制中心 高级设置 环境变量 Path里面看看 %systemroot%是否完整

3.咋是灰网啊我去
如果你进入游戏的时候 显示net坏 那么就是没有绿网
如下路径C:\Windows\System32\drivers\etc
找到 hosts文件 记事本打开 把里面东西全删了 改成下面这些
127.0.0.1 id.twitch.tv #S302
129.28.248.89 wq.sys-all.cn
81.71.193.236 ai.sys-all.cn
42.193.74.107 wi.sys-all.cn
81.70.119.195 at.sys-all.cn
然后保存 再打开你的start.bat

4：我用simna没反应 start.bat 打不开怎么办？
请使用start.bat
可能有这些原因 你的windows10时区不是中国 你没有以管理员运行start.bat 你的包被偷工减料了
网络问题无解 版本更新 slim.ver 缺失........反正你按照我这个顺序逐一排查就对了


5.摄像头如何配置
在SDGB文件夹/package /Sinmai-Assist  里有一个
config.yml
双击  用VS CODE打开  然后往下滑 你就可以看到配置参数

6.如何开启MOD（作弊面板）并且扫码登录？

同样是上一个的操作 然后下滑找到modsetting 然后把showpanel后面的false改为true
然后你找到dummylogin  把他后面也改成true
还有autoplay fastplay什么的 也是这样子开 面板才会显示

7.扫码登录 我没有摄像头怎么登录啊

1.打开微信舞萌dx公众号 2.获得玩家二维码 3.在那个界面长按二维码并且扫描 4.获得字符串
2.复制获得的字符串到你已经打开并且在扫描二维码页面的舞萌 6.看到悬浮窗Dummylogin 那里 在第一个大框Token下面填写你复制的字符串 然后点击Token Login 就会发现登录了 7.玩游戏
方案2：上机玩一把之后 上传成绩 然后去你的 userdataout文件夹（自己找找在哪里）获得userId
以后就可以用这个UserID直接在刚刚那个悬浮窗下面登录 但是前提是30min前刷新过二维码(不然会关你15分钟小黑屋）


8.如何更新?
解压1.50 X更新包压缩包 你会看见例如A71XX的文件夹 打开看一下里面有没有套娃 如果没有  就把文件夹丢到SDGB2025\Package\Sinmai_Data\StreamingAssets 打开游戏就可以发现更新了 (积累更新包必须一起放入)

9.如何开启自动游玩 如何解锁全部收藏品/歌曲/搭档？？

在VScode中把cheat栏列autoplay调为true
启动游戏之后的左上角面板那里开 AP FC ......最好打开disable mode update

![Image](https://github.com/user-attachments/assets/7b4860d6-6bc3-4e21-be2a-a48dab131254)

把这个地方的false  看自己想要啥 改成true就行(图里的是假的别试了)

10. 1.50如何更新1.51
其实谈不上更新 只需要替换一个ICF1文件  
如下
首先https://www.123912.com/s/2LjLVv-Tutwh 下载后 文件名应该是 ICF1
其次 打开D:\SDGB2025\Package\amfs
然后 如果里面有ICF把下载的ICF1替换进去
最后 启动游戏 发现已经更新到1.51


11.odd.sys服务无法启用 如下

![挖槽怎么启动不了 退钱！](https://github.com/user-attachments/assets/aebf1508-617e-402f-ad31-39904db7c65b)
 不要慌张 下载NO ODD.SYS SEGATOOLS解决 
下载:https://www.123912.com/s/2LjLVv-TUtwh
解压后 直接全选文件夹里的文件 复制到D:\SDGB2025\Package并全部替换
随后 点击 启动.bat 后即可启动游戏

12.已更新1.51E
需要放置A012更新包
而且还要ICF文件（放置方法和第十条一样 替换源文件）
但是现在不会显示 得等华丽服务器更新(误

13.Failed to initialize Melon Loader......怎么办?
确保没有中文路径 并且游戏不是在中文文件夹里

14.摄像头黑屏无法扫码？
(1)没有正确绑定摄像头ID 请绑定正确的ID #下面填入你的摄像头ID
    chimeCameraId: 0
    leftQrCameraId: 0
    rightQrCameraId: 0
    photoCameraId: 0
(2) 把摄像头清晰度设置成640x480 在启动游戏
(3)在Aquamai.tom中调整相关配置
(4)更改屏幕分辨率
(5)笔记本用户尝试外接摄像头？

15.标题服务器怎么坏了 怎么传不上分了
因为你狗号坠机了 或者填写错误了 或者你用了上面的无odd包
解决方法： 打开Package里的segatools.ini
找到

<img width="199" height="115" alt="Image" src="https://github.com/user-attachments/assets/b1a8c562-0f5d-4ee0-9ca8-53589c0393ee" />
看到ID了吗 那个就是你的狗号 你需要去找一个正确的狗号 并且填上去 就可以解决这个问题


**EX>>** https://github.com/clansty/MaiChartManager  
很好的模组和铺面管理器 同时也是音乐播放器~

![Image](https://github.com/user-attachments/assets/424e634d-8122-4ea4-8d37-a49aa314c034)
**吊图一大堆**






