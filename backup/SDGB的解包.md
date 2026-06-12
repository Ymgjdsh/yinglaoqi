#  maimai HDD：从解包到运行完整指南

文章中的资源大多转载自[此网页](https://pavilions12.github.io/2026/06/12/%E5%88%9D%E6%AC%A1%E6%8E%A2%E7%B4%A2maimai%20HDD/ )所有资源非本人制作
---

## 目录

- [方案一：全手动解包修补（适合进阶用户）](#方案一全手动解包修补适合进阶用户)
- [方案二：使用覆盖包快速启动（推荐新手/遇到问题的用户）](#方案二使用覆盖包快速启动推荐新手遇到问题的用户)
- [通用故障排除](#通用故障排除)
- [附录：ODD Driver 安全性说明](#附录odd-driver-安全性说明)

---
> [!WARNING]
> !注意 所有方案只适用于Windows系统  如果需要使用 请确认系统环境




## 方案一：全手动解包修补（适合进阶用户）

### 一、解包阶段

#### 1. 获取原始 `.APP` 镜像文件

下载 SEGA 街机数据发布版本 `.APP` 源文件，本文以 **SDGB 1.55** 版本为例：  
[SDGB_1.55.01_20260302122354_0.app(暂时不提供 可以自行搜索)](https://www.bilibili.com/video/BV1GJ411x7h7/?spm_id_from=333.337.search-card.all.click)

#### 2. 使用 `fsdecrypt` 解包

下载 [`fsdecrypt`](https://gitea.tendokyu.moe/beerpsi/fsdecrypt/releases) 并执行：

```bash
fsdecrypt.exe SDGB_1.55.01_20260302122354_0.app
```
或者直接把.app文件拖到fsdecrypt.exe用它打开

生成 `.vhd` 文件（如 `SDGB_1.55.01_20260302122354_0_3.vhd`）。

#### 3. 从 `.vhd` 提取 `Package` 目录

- 双击 `.vhd` 文件挂载为虚拟磁盘  
- 将根目录下的 **`Package`** 文件夹拖出到本地（如 `D:\mai2\Package`）

---

### 二、修补阶段(手动看这里 萌新直接往下翻看方案二)

> 以下所有操作均在 **`Package\`** 目录中进行。

1. **整合 `segatools`**  
   下载 [`segatools`](https://gitea.tendokyu.moe/TeamTofuShop/segatools/releases) → 解压 `mai2.zip` → 全部文件复制到 `Package\`

2. **部署 `MelonLoader`**  
   从 [`MelonLoader`](https://github.com/LavaGang/MelonLoader/releases/latest) 获取稳定版 → 解压到 `Package\` [^1]

3. **添加 `AquaMai.toml`**  
   下载 [`AquaMai.toml`](https://pavilions12.github.io/2026/06/12/%E5%88%9D%E6%AC%A1%E6%8E%A2%E7%B4%A2maimai%20HDD/AquaMai.toml) 放到 `Package\` [^1]

4. **创建 `Mods` 目录**  
   在 `Package\` 下新建 `Mods` 文件夹 [^1]

5. **安装 `AquaMai.dll`**  
   从 [AquaMai 下载页](https://portal.mumur.net/mai2/aquamai) 获取 **版本 ≤ 1.5.19** 的 `AquaMai.dll` → 放入 `Package\Mods\` [^1]

6. **创建运行时目录**  
   新建三个空文件夹：`option`、`appdata`、`amfs`

7. **放置 ICF 文件**  
   将游戏 ICF 文件重命名为 `ICF1` → 放入 `Package\amfs\`

8. **替换配置文件**  
   下载 [`segatools.ini` 示例](https://pavilions12.github.io/2026/06/12/%E5%88%9D%E6%AC%A1%E6%8E%A2%E7%B4%A2maimai%20HDD/segatools.ini) 和 [`launch.bat` 示例](https://pavilions12.github.io/2026/06/12/%E5%88%9D%E6%AC%A1%E6%8E%A2%E7%B4%A2maimai%20HDD/launch.bat) → 覆盖 `Package\` 中的同名文件

9. **脱壳 `amdaemon.exe`**  
   使用 [`XenonUnpack.exe`](https://pavilions12.github.io/2026/06/12/%E5%88%9D%E6%AC%A1%E6%8E%A2%E7%B4%A2maimai%20HDD/XenonUnpack.exe) 对 `Package\amdaemon.exe` 脱壳

10. **部署输入驱动**  
    将 [`odd.sys`](https://pavilions12.github.io/2026/06/12/%E5%88%9D%E6%AC%A1%E6%8E%A2%E7%B4%A2maimai%20HDD/odd.sys) 和 [`odd-loader.bat`](https://pavilions12.github.io/2026/06/12/%E5%88%9D%E6%AC%A1%E6%8E%A2%E7%B4%A2maimai%20HDD/odd-loader.bat) 复制到 `Package\`

---

### 三、运行（方案一）

1. **以管理员身份**运行 `odd-loader.bat`（保持窗口打开）  
2. 运行 `launch.bat`

---

## 方案二：使用覆盖包快速启动（推荐新手/遇到问题的用户）

> 很多启动失败（`amPlatformGetPlatformInformation` 错误、`amdaemon.exe` 闪退）是因为手动修补时的版本不匹配。社区预制的**覆盖包**可直接覆盖工作文件。

### 步骤

1. **下载覆盖包**（SDGB 1.55 版本）  
   [SDGB1.55coverage.zip 下载链接](https://github.com/Ymgjdsh/yinglaoqi/releases)

   > ⚠️ 该链接为我的  GitHub 仓库 Releases

2. **准备 `Package` 目录**（按方案一解包得到干净的 `Package`）

3. **覆盖文件**  
   解压覆盖包，全选所有内容**复制**到 `Package` 目录，覆盖同名文件。

4. **运行**  
   - 以管理员身份运行 `odd-loader.bat`  
   - 运行 `launch.bat` 或 `start.bat`

### 覆盖包的特点 

- 包含正确版本的 `amdaemon.exe`（已脱壳）、`mai2hook.dll`、`AquaMai.dll` 及配置文件  
- 避免了 `AquaMai.dll` 版本过高导致崩溃的问题  
- 直接修复 `amPlatformGetPlatformInformation` 错误

---

## 通用故障排除

### 1. `amPlatformGetPlatformInformation(). ErrCode 0  闪现命令行窗口后无法启动`

- **原因**：amdaemon 未能通过 hook 获取模拟的平台信息  
- **解决**：  
  - 以管理员身份运行 `odd-loader.bat`  
  - 开启测试模式：  
    ```cmd
    bcdedit /set testsigning on
    bcdedit /set nointegritychecks on
    ```  
    重启电脑  
  - 使用方案二覆盖包  
  - 临时关闭杀毒软件

### 2. Game processes have terminated

- **原因**：缺少 `option`、`appdata`、`amfs` 目录或 `odd.sys` 未正确加载  
- **解决**：检查目录结构，重新以管理员运行 `odd-loader.bat`

### 3. 黑屏

- **原因**：缺少 `option\` 文件夹或 `ICF1` 放置错误  
- **解决**：确认 `option` 存在，`amfs\ICF1` 正确

### 4. 卡第三启动屏

- **原因**：机台模式设置问题  
- **解决**：测试键（数字 7）进入测试模式 → 游戏设置 → 将“设定群组内的标准机”改为 **标准设定机**，或将“店内招募设置”改为 **OFF**

### 5. 灰网（标题服务器坏NET坏等）

- **可能原因**：`AquaMai.toml` 中 `[GameSystem.RemoveEncryption]` 未禁用  
- **解决**：添加一行 `Disabled = true`
其他方法请看Blog里另一篇[文章](https://ymgjdsh.github.io/yinglaoqi//post/wu-meng-SDGB1.51%20I%20-lan-ren-bao-shi-yong-jiao-cheng-%EF%BC%88-po-zhen.html)里的网络配置教程

### 6. 无声音

- **原因**：缺少 `mai2.ini` 或未设置声道  
- **解决**：在 `Package\` 根目录创建 `mai2.ini`：  
  ```ini
  [Sound]
  Sound8Ch=0
  ```

---

## 附录：ODD Driver 安全性说明

`odd.sys` 是 maimai HDD 破解所需的内核驱动，用于模拟 SEGA 街机硬件。  
典型安全安装脚本（如 `odd-loader.bat`）内容如下：

```batch
@echo off
sc stop odd >nul 2>nul
sc delete odd >nul 2>nul
copy /y odd.sys %SystemRoot%\System32\drivers\
sc create odd binPath= "%SystemRoot%\System32\drivers\odd.sys" type= kernel
sc start odd
pause
sc stop odd
sc delete odd
```

该脚本仅执行驱动安装与卸载，无下载、加密、后门等恶意行为。  
- **风险**：任何未签名内核驱动都有潜在系统不稳定风险，但运行该游戏必需。  
- **建议**：从可信社区（GitHub segatools 项目、大型模拟论坛）获取，并开启测试模式。  
- **验证**：上传 `odd.sys` 到 [VirusTotal](https://www.virustotal.com) 扫描，少量引擎报“HackTool”属正常误报。

---

## 脚注

[^1]: `MelonLoader` 和 `AquaMai` 也可以通过 [`MuNET-OSS/MaiChartManager`](https://github.com/MuNET-OSS/MaiChartManager/releases/latest) 一键安装，选择“让我们说中文！”自动生成配置。
```
本文章旨在讨厌https://blog.xiaoxinww.icu/的评论后才可查看 

