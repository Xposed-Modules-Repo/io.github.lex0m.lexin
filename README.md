<div align="center">

# 乐信 · lexin

**微信界面美化 + 本地功能增强** · Xposed / LSPosed 模块

![version](https://img.shields.io/badge/version-1.6.2-4A6CF7?style=flat-square)
![platform](https://img.shields.io/badge/Android-12%20~%2016-3DDC84?style=flat-square&logo=android&logoColor=white)
![wechat](https://img.shields.io/badge/微信-8.0.72%20~%208.0.80-07C160?style=flat-square&logo=wechat&logoColor=white)
![size](https://img.shields.io/badge/APK-670%20KB-8A8F9A?style=flat-square)
![license](https://img.shields.io/badge/license-MIT-blue?style=flat-square)

包名 `io.github.lex0m.lexin` · 作者 lex · 纯 Java · 无 Gradle

[下载 APK](lexin-1.6.2.apk) · [功能一览](#功能一览) · [安装](#安装) · [兼容性](#兼容性) · [设计取舍](#设计取舍)

</div>

---

## 这是什么

一个跑在微信进程里的 LSPosed 模块，做两件事：

- **界面**：把微信换成你自己的样子 —— 全屏背景、卡片化列表、悬浮底栏、毛玻璃。
- **本地功能**：防撤回、朋友圈保留、去广告、自动原图、步数修改、一键转发……
  全部**在设备上完成**，不上传、不伪造、不改一条上行报文。

一个 670 KB 的 APK，没有 Gradle 工程、没有第三方依赖、没有后台服务。

---

## 功能一览

### 界面

| 功能 | 说明 |
| --- | --- |
| 全屏背景 | 任意图片，透明度可调，五种缩放（填充 / 适应 / 拉伸 / 居中 / 自定义裁剪） |
| 列表卡片化 | 左右内缩、圆角、上下间隔、卡片高度全可调 |
| 聊天条独立成卡 | 单独配图、裁剪、透明度、模糊 |
| 悬浮底栏 | 主页 TabBar 与聊天输入栏改成悬浮圆角卡片 |
| 毛玻璃 | Android 12+ 的 GPU 模糊（低版本自动降级为纯色） |
| 顶部跟随 | 状态栏、聊天标题栏跟随背景或微信深浅模式 |
| 每日一言 | 面板首屏一句诗，每次打开换一句 |

### 聊天

| 功能 | 说明 |
| --- | --- |
| 消息防撤回 | 对方撤回的消息原样留在列表，气泡压暗 + 正下方贴方向标签（不压住原文，切后台回来不跑位） |
| 朋友圈保留 | 对方删掉的评论与动态，本机留一份副本 |
| 去广告 | 开屏、小程序开屏位、朋友圈信息流 |
| 自动查看原图 | 浏览图片时自动切原图，点都不用点 |
| 放宽本地限制 | 表情包数量、消息多选、状态字数上限 |
| 骰子 / 猜拳自选 | 长按表情面板可指定点数或出拳，也可以保持随机 |

### 转发与导出

| 功能 | 说明 |
| --- | --- |
| 长按菜单加项 | 不改微信任何判定，只在长按菜单里多一格「转发（乐信）」 |
| 官方转发 | 普通消息直接触发微信自己的转发，走官方链路 |
| 受限消息导出 | 语音、图片等不能转发的消息，导出到「下载/乐信导出」 |
| 语音转 MP3 | 微信的 SILK 语音解码后转 MP3（解码在模块进程做，微信进程零 native） |
| 朋友圈转发 | 文字 / 图片 / 视频，支持一键全选 |

### 工具

| 功能 | 说明 |
| --- | --- |
| 运动步数 | 三种模式：直接增加 / 每小时自动增加 / 倍率放大，都受上限约束，不会把数字钉死 |
| 解除扫码限制 | 相册选图、长按图片识别二维码按「相机」场景处理 |
| 自动语音转文字 | 收到语音自动调微信官方的转文字（不接第三方识别） |
| 批量分类标签 | 给多个好友批量打标签，走微信官方 netscene，服务端与你手动打标签完全一致 |
| 隐蔽入口 | 面板入口藏在「关怀模式」页，常规界面零痕迹 |

---

## 安装

1. 装 [`lexin-1.4.0.apk`](lexin-1.4.0.apk)
2. LSPosed 里勾选「乐信」，**作用域只勾微信**
3. 强行停止微信，重新打开

> 需要 root + LSPosed（或兼容框架）。没 root 走 [LSPatch](https://github.com/JingMatrix/LSPatch)，
> 步骤与注意项见 [免 root 使用指南](https://github.com/lex0m/lexin/blob/main/%E5%85%8Droot%E4%BD%BF%E7%94%A8%E6%8C%87%E5%8D%97.md)。

## 打开面板

1. **桌面「乐信」图标**，或 **LSPosed → 模块 → 乐信 → 右下角 ▶**
   → 直接打开模块自己的设置页（全部开关一屏）；同时会给微信发一条通知，切回微信就能看到悬浮面板
2. 微信里：**我 → 设置 → 更多 → 关怀模式 → 长按「开启」**（隐藏入口）

> 步数、批量标签这类操作必须在微信进程里做，所以它们只在悬浮面板里。

---

## 兼容性

### Android

| 版本 | 状态 |
| --- | --- |
| Android 15 / 16 | 实测主力环境（edge-to-edge、强制深色、16 KB 页对齐都已处理） |
| Android 12 ~ 14 | 支持 |
| Android 9 ~ 11 | 理论可用（minSdk 28）；音频转码库只带 arm64，32 位机型只能用到无 native 的功能 |

### 微信

| 版本 | 状态 |
| --- | --- |
| **8.0.78** | 全部适配，本机实测 9/9 |
| 8.0.79 / 8.0.77 | 全部适配（8.0.79 的撤回标签与开屏广告锚点在 1.3.9 修正） |
| 8.0.76 / 8.0.74 | 全部适配；骰子结果改写降级（选择框仍在） |
| 8.0.72 | 防撤回 / 表情 / 原图 / 扫码 / 入口 全通 |

表里没有的版本照样能用：模块会自己在设备上扫微信 dex，按「类名 + 方法内字符串 +
方法签名」三层特征找落点，结果缓存到本机，下次启动零成本。找不到的功能安静跳过，
不崩、也不影响微信本身。

给新版本补一张表（可选，让首次启动直接命中）：

```sh
python3 tools/gen-anchors.py . 8.0.80=/path/weixin8080.apk   # 约 25 秒/版本，直接解析 dex
sh build.sh
```

---

## 设计取舍

这几条决定了代码为什么长这样：

- **不改微信的判定，只借它的链路。** 转发用微信自己的转发、标签用微信自己的 netscene、
  语音发送用微信自己的发送入口。不伪造消息 xml，不改上行报文。
- **每个功能独立失败。** 一个功能挂不上就静默跳过、面板里标「未适配」，绝不连累其它功能，
  也不把异常抛给宿主。
- **降级要干净。** 锚点四级回退：版本表 → 邻近版本 → 本机学习缓存 → 运行时 dex 扫描，
  每级都做指纹校验 —— 宁可少一个功能，也不挂错类。
- **微信进程不加载任何 native 库。** 解码、转码这类活放在模块自己的进程里，微信侧只递字节。
- **发布版零日志。** `Log.d` 编进空实现；要排查时在面板里显式打开诊断日志，重启微信才生效。
- **不在微信目录里留新文件。** 配置写进微信自己的 `shared_prefs`，键名统一 `ap_+hashCode`。

---

## 构建

不用 Gradle，JDK 21 + aapt2 + R8 + apksigner：

```sh
sh build.sh                      # 正式包 → dist/lexin-<版本>.apk
sh build.sh --debug              # 诊断包（日志开关打开）
sh tools/build-audio.sh --test   # 重编音频库并自测
```

版本号唯一来源是 `AndroidManifest.xml`；`build.sh` 会自己探测 Termux 工具链，
打完自动跑 `tools/verify_apk.py`（组件是否被 R8 裁掉、`.so` 是否 STORED、
`resources.arsc` 是否未压缩、`xposed_init`、JNI 符号、buildId 指纹），任何一项不过就失败。

---

## 更新日志

### v1.6.2（2026-11-16）— 全盘复审：自检复活 + 背景图通道 + 构建可复现

这一版没有新功能，专修**「装上了、面板也说好了，但就是不工作」**。复审 62 条，修 21 条。

**两个阻断**
- **自检机制自己就是坏的**：`SelfCheck` 用 `getDeclaredMethod("pulse")` 找方法，但 R8 把
  `pulse` 改名成了 `le` ⇒ 发布包里必然抛 `NoSuchMethodException`。真机证据：
  `hook 活性 armed=1 / hits=0`，37 分钟一次没涨（自检 15 秒一次）。改成按**签名**找。
- **「重新自动适配」从来不扫**：`forget()` 先把待扫槽位清空，紧接着 `schedule()` 看到空表
  直接返回 —— 一次扫描都不发生，toast 却说"已开始"。

**高危**
- 长按菜单点击回调挑方法不校验返回类型就 `setResult(null)` ⇒ 挑中 `->boolean` 的重载会
  拆箱 null，**崩微信**
- 两处 `getOutline` 缺 try/catch：框架在渲染线程调，首次布局前 0×0 会抛异常漏进微信绘制
- 卡片高度守卫是**空 if 块**：`WRAP_CONTENT` 被改成绝对像素，多行消息被截断
- **背景图三处全走 `content://`**，而微信 targetSdk 34 且没有 `QUERY_ALL_PACKAGES`，
  解析不到 authority ⇒ 面板选图必失败、背景画不出来。改成读写都走微信自己 `files/` 的点号文件
- 老背景图迁移失败也照删 ⇒ 用户的图直接消失
- 主题包 `FileReader` 泄漏（最终 "Too many open files"）；`image()` 复用同一个 Drawable 实例（错图）

**构建可复现**
以前每次构建用随机锚点密钥 ⇒ 同源码连编三次三个哈希，`VERSIONS.md` 记的哈希永远对不上。
改成 `sha256(私盐 + 源码指纹)` 确定性派生。**源码不变 ⇒ 包完全一致**（已实测连跑两次相同）。

### v1.6.0 / v1.6.1（2026-11-16）— 判据三态 + 死类根因

- **「面板全绿、功能全哑」的根因**：微信 8.0.80 用 Tinker 热修，真正执行的类是补丁 dex 里那份；
  用框架给的 `XC_LoadPackage.classLoader` 解析出来的是 base.apk 的**死类** —— 存在、能挂、
  永远不触发。现在在 `Application.onCreate` / `Activity.onResume` 采纳运行时 ClassLoader 并重挂
- `Features.app` 从 v1.2 起一直是 null（`Application.attach` 时刻 `getApplicationContext()` 还没赋值）
  ⇒ 配置永远读不到、状态永远推不出去、全量扫描从没跑过。改用 `param.thisObject`
- 面板判据从「一个布尔」改成三态：`未适配` / `已挂载未命中` / `已命中 N 次`，
  快照带头部（版本 / 微信版本 / pid / 时间戳），超过 10 分钟标灰
- 防撤回落到 `DbGuard`：直接从 WCDB 的 `update()` 里摘掉 `type`/`content`/`isSend` 三个字段
  （`status=2` 实测是发送状态，按它拦会把消息发不出去）
- 隐蔽收敛：`Bridge`/`Settings`/`MediaSaver` 从挂 `Activity.onResume` 改成生命周期回调（零 hook）；
  `AntiRecall` 兜底不再挂 framework 的公共适配器入口

### v1.4.0（2026-10-28）— 两轮兼容性优化

**功能兼容**
- 桌面图标 / LSPosed ▶ 直接进设置页；「界面美化」页补返回出口
  （之前进去出不来，看起来像"模块只有界面美化"）
- 设置页补齐到与微信面板同一套：转发增强、语音·底栏·标签、诊断日志、面板入口
- **设置页的开关真的生效了**：原来模块进程写自己的 `svc.xml`、微信进程写微信的 prefs，
  两边各读自己那份 ⇒ 设置页改的开关微信读不到。现在改动会经 provider 同步进微信进程（按时间戳水位合并）
- 外观页选的背景图现在生效（之前存在模块目录、微信读自己的目录）
- 转发增强的触摸热路径：先判抬手再查父级文字

**设备 / 系统兼容**
- targetSdk 35 在 Android 15 强制 edge-to-edge ⇒ 底部补系统栏高度，三键导航不再挡内容
- 深色模式 force dark 会反转浅色界面 ⇒ 设置页 / 外观页 / 微信面板三处全关
- 微信 targetSdk 34 且无 `MANAGE_EXTERNAL_STORAGE` ⇒ Android 11+ 写不了 `/sdcard/Download`
  （语音/媒体导出会静默失败）。导出改成三层兜底 + MediaStore
- 微信的 `:xweb_*` / `:sandboxed_process` 沙箱进程不再装全套 hook；面板广播、状态推送、dex 扫描只在主进程
- 版本号改由构建脚本从 `AndroidManifest.xml` 生成
- `BgProvider` 的写操作校验调用方

**未修**（需要真机回归）：朋友圈广告在构造阶段拦截的方式、锚点空结果缓存、
转发增强的栈学习范围、32 位机型缺音频库。

### v1.3.x

- **1.3.9** 修微信 8.0.79 两个锚点错种子（`chat_binder` / `ad_open`）
- **1.3.3** 安卓 17 兼容（运行时字符串特征扫描）、频闪 / 拖影修复
- **1.3.1** 主页仿 TG 悬浮底栏、修复聊天标题栏黑边、朋友圈一键全部转发
- **1.3.0** 自动语音转文字、悬浮聊天底栏、批量分类标签

### v1.2.x

- **1.2.3** 朋友圈视频转发、自绘勾选 UI
- **1.2.2** 长按菜单收敛为一条路径 + 朋友圈转发
- **1.2.1** 语音转 MP3（SILK 解码 + LAME 编码，真机逐字节验证）

---

## 致谢

实现思路参考了不少开源项目，代码是 Java 独立写的，没有直接复制：

- [MDWechat](https://github.com/Blankeer/MDWechat) —— 按视图树定位页面层级、ActionBar 背景接管、九宫格气泡解析
- [WeKit](https://github.com/ujhhgtg/WeKit) —— 朋友圈广告拦截与扫码限制解除的做法、微信日志 tag 作特征定位
- [XposedWechatHelper](https://github.com/wuxiaosu/XposedWechatHelper) —— 传感器层改步数的思路
- [WechatSpellbook](https://github.com/Gh0u1L5/WechatSpellbook) · [WechatMagician](https://github.com/Gh0u1L5/WechatMagician) —— 早期防撤回 / 功能注入的参考
- [DJB-Developer/wechat-android-history-versions](https://github.com/DJB-Developer/wechat-android-history-versions) —— 微信官方历史版本直链（生成多版本适配表用）
- [LSPosed](https://github.com/LSPosed/LSPosed) —— 运行框架

哪位作者觉得引用不当，说一声我就改。

## 免责声明

仅供个人学习与技术研究使用。
**禁止在国内网络平台传播、售卖或代装**（网盘、论坛、公众号、应用市场、短视频平台、群文件分享等一律禁止）。
使用本模块产生的一切后果由使用者自行承担。

<div align="center">

交流群 **186737276**

</div>
