<div align="center">

# 合成大西瓜魔改版（DaXiGua）

**最简单的魔改与发布方案：配套专属改图工具，不用改业务代码，只需修改配置即可打造专属合成大西瓜**

[![Cocos2d-js](https://img.shields.io/badge/Engine-Cocos2d--js-55c2e1.svg)](https://www.cocos.com/)
[![H5 Game](https://img.shields.io/badge/Platform-HTML5%20%2F%20Mobile-orange.svg)](#)
[![Docker](https://img.shields.io/badge/Docker-Supported-2496ed.svg)](https://www.docker.com/)
[![Vercel](https://img.shields.io/badge/Deploy-Vercel%20%2F%20Webify-black.svg)](https://vercel.com/)

作者：[程序员鱼皮](http://dogyupi.com/) · [图文最全教程](https://mp.weixin.qq.com/s/H9VR1MWn-9bKSC_1l_MkJw) · [B 站保姆级视频教程](https://www.bilibili.com/video/BV1Vy4y1n7KW/) · [专属改图工具](https://daxigua-tools.liyupi.com)

[项目简介](#-项目简介) · [本地启动](#-本地启动) · [快速魔改清单](#-快速魔改清单) · [上线发布](#-上线发布) · [魔改原理](#-魔改原理) · [问题及解决](#-问题及解决) · [常见探索问题](#-常见问题-faq)

</div>

> **免责声明**：本项目仅用于帮助大家学习前端游戏技术及个人娱乐体验，请勿将修改后的网站进行大规模传播或用于商业用途，以避免产生侵权风险。如果你觉得本项目有帮助，欢迎点亮 Star 支持，也可以关注作者 [程序员鱼皮](http://dogyupi.com/) 的技术公众号 [『程序员鱼皮』](https://mp.weixin.qq.com/s/H9VR1MWn-9bKSC_1l_MkJw)（如有疑问可联系微信：`liyupi66`）。遇到运行或部署问题，建议先阅读文末的 [问题及解决](#-问题及解决)。

---

## ✨ 项目简介

合成大西瓜魔改版（DaXiGua）是由 [程序员鱼皮](http://dogyupi.com/) 整理并深度封装的开源 H5 物理碰撞合成小游戏魔改项目，底层基于 Cocos2d-js 游戏引擎与 Canvas 物理刚体系统运行。为了让零基础同学也能在几分钟内做出刷爆朋友圈的个性版本，项目将原本分散在混淆代码中的核心玩法参数全部抽离到了 `extraSettings.js` 配置文件中，并额外配套上线了在线改图工具，让你不用写复杂代码就能完成个性化定制与公网发布。

你可以先通过以下入口体验成品效果、获取配套工具或查看分步教程：

| 资源名称 | 访问链接 | 说明 |
| --- | --- | --- |
| 图文详细教程 | [魔改和上线你的合成大西瓜，最全教程](https://mp.weixin.qq.com/s/H9VR1MWn-9bKSC_1l_MkJw) | 从素材准备、参数魔改到上线发布的完整图文手册 |
| 视频保姆教程 | [全网最贴心的魔改合成大西瓜教程](https://www.bilibili.com/video/BV1Vy4y1n7KW/) | 手把手演示从本地修改到发布上线的全过程 |
| 配套改图工具 | [daxigua-tools.liyupi.com](https://daxigua-tools.liyupi.com) | 自动裁剪对齐水果尺寸，大幅提升替换图片效率 |
| 魔改版在线体验 | [dadaxigua.liyupi.com](https://dadaxigua.liyupi.com) | 体验配置魔改后的趣味合成大西瓜版本 |
| 未修改版在线体验 | [daxigua.liyupi.com](https://daxigua.liyupi.com) | 体验原汁原味的基础版合成大西瓜 |
| 未修改版源码归档 | [Release 1.0.0](https://github.com/liyupi/daxigua/releases/tag/1.0.0) | 需要从干净原始版本开始研究源码时可直接下载 |

![合成大西瓜魔改版趣味玩法演示截图](./assets/dadaxigua.png)

## 🚀 本地启动

项目提供 `serve` 静态服务和 Docker 容器两种本地运行方式，新手推荐直接使用第一种方式，在本地调试正常后再执行上线发布。

### 方式一：使用 serve 启动（小白推荐）

首先通过 npm 全局安装轻量级静态文件服务器工具 `serve`：

```bash
npm i -g serve
```

接着在终端中进入本仓库 `daxigua` 根目录（确保该目录下能看到 `index.html`），运行 `serve` 启动服务：

```bash
serve
```

启动完成后，打开浏览器访问 `http://localhost:5000` 即可开始试玩（电脑浏览器可按 `F12` 切换到手机视图预览）。

### 方式二：使用 Docker 启动（感谢 [buchenglei](https://github.com/buchenglei) 的贡献）

如果你的电脑或服务器已经安装 Docker，可以直接利用仓库自带的 `Dockerfile` 构建镜像并以后台容器运行：

```bash
# 构建镜像
docker build -t daxigua-server .

# 启动容器并映射 5000 端口
docker run -d --name play-daxigua -p 5000:5000 daxigua-server
```

## 🧩 快速魔改清单

下表汇总了全部 15 项开箱即用的魔改能力与对应的修改位置。所有配置型玩法都集中在根目录的 `extraSettings.js` 中并附带中文注释，而图片、背景和音效素材均存放在 `res/raw-assets` 对应子目录下，替换时请务必保持**完全相同的文件名、文件后缀与图片尺寸**，建议优先使用配套的 [大西瓜改图工具](https://daxigua-tools.liyupi.com) 辅助导出以免尺寸错位。

| 序号 | 魔改玩法 | 修改方式与参考说明 |
| --- | --- | --- |
| 1 | 修改合成得分规则 | 编辑 `extraSettings.js` 中的分数倍率或自定义得分配置 |
| 2 | 自定义水果图案 | 替换 `res/raw-assets` 对应目录下的图片，必须保持同文件名、后缀与尺寸（推荐配合改图工具使用） |
| 3 | 开启无敌模式 | 编辑 `extraSettings.js` 文件开启无敌开关，避免触顶直接判负 |
| 4 | 指定第一个出现的水果 | 编辑 `extraSettings.js` 文件自定义开局首个掉落水果等级 |
| 5 | 指定下一次出现的水果 | 编辑 `extraSettings.js` 文件固定或控制每次生成的水果类型 |
| 6 | 大水果合成小水果 | 编辑 `extraSettings.js` 文件反转常规合成方向，体验反向魔改玩法 |
| 7 | 让水果更有 Q 弹效果 | 编辑 `extraSettings.js` 调整碰撞弹性系数，底层物理原理可参考 [Cocos PhysicsCircleCollider 文档](https://docs.cocos.com/creator/api/zh/classes/PhysicsCircleCollider.html?h=circlecollider) |
| 8 | 减缓水果下落速度 | 编辑 `extraSettings.js` 调整重力与刚体参数，底层原理可参考 [Cocos RigidBody 刚体文档](https://docs.cocos.com/creator/manual/zh/physics/physics/rigid-body.html?h=%E5%88%9A%E4%BD%93) |
| 9 | 替换背景音乐与音效 | 在 `res/raw-assets` 对应目录下使用同名同后缀的音频文件覆盖原音效 |
| 10 | 替换游戏背景图 | 与替换水果图片原理相同，在 `res/raw-assets` 中按同名同尺寸覆盖背景素材 |
| 11 | 去除页面广告图 | 将原广告图片替换为 [同背景色纯色底图](https://636f-codenav-8grj8px727565176-1256524210.tcb.qcloud.la/0.png) |
| 12 | 替换广告跳转链接 | 编辑 `extraSettings.js` 文件修改或清空广告链接地址 |
| 13 | 修改网页标题 | 编辑 `extraSettings.js` 文件自定义浏览器标签页标题 |
| 14 | 开启自定义选分弹窗 | 编辑 `extraSettings.js` 文件开启分数弹窗交互 |
| 15 | 点击右上方图标更换水果 | 编辑 `extraSettings.js` 文件开启右上角手动换果道具能力 |

## 📦 上线发布

本地验证无误后，你可以通过腾讯云 Webify 一键部署、Vercel、腾讯云静态网站托管或 GitHub Pages 等多种方式免费将游戏发布到公网，零基础新手建议优先尝试 Vercel 或一键部署。

### 方案一：腾讯云 Webify 一键部署

腾讯云 Webify 支持自动将本模板仓库克隆到你的个人账号并部署为静态应用，后续只要更新代码就会自动触发重新部署。点击下方按钮即可快速开始：

[![腾讯云 Webify 一键部署合成大西瓜](https://cloudbase.net/deploy.svg)](https://console.cloud.tencent.com/webify/new?tpl=https%3A%2F%2Fgithub.com%2Fliyupi%2Fdaxigua&reponame=daxigua)

在创建应用配置页面中，将「构建命令」与「安装命令」保持为空，并将「输出目录」填写为 `.`（当前根目录），然后点击部署应用即可完成上线。

![腾讯云 Webify 部署合成大西瓜应用配置参数截图](https://main.qcloudimg.com/raw/8ca88a49907cd6f2657084d9a63def15.png)

### 方案二：使用 Vercel 命令行发布（零基础推荐）

Vercel 是非常流行的免费静态网站托管平台，操作步骤极简且会自动生成简短的可访问网址，同时也支持绑定自己的独立域名（不过服务器位于海外，国内直连速度相对较慢）。

首先通过 npm 全局安装 Vercel CLI 工具：

```bash
npm install -g vercel
```

安装完成后，在终端进入 `index.html` 所在的 `daxigua` 文件夹，执行生产发布命令：

```bash
cd daxigua
vercel --prod
```

执行过程中命令行会依次询问项目名称、是否与已有项目关联、是否保存当前配置等选项。如果你打算同时部署多个不同主题的魔改版，请务必选择**不与已有项目关联**。部署完成后终端会直接输出一个在线网址，打开即可游玩并分享给好友。

### 方案三：腾讯云静态网站托管

如果你希望国内用户打开速度更快，并且避免默认海外域名在微信内被拦截，可以选择使用 [腾讯云静态网站托管](https://cloud.tencent.com/product/wh)。具体开通与上传步骤可以参照详细图文教程 [魔改和上线你的合成大西瓜，最全教程](https://mp.weixin.qq.com/s/H9VR1MWn-9bKSC_1l_MkJw) 逐步操作。

## 🔧 魔改原理

如果你不仅想改配置玩游戏，还想搞懂底层代码是怎么接管 Cocos2d-js 游戏逻辑的，建议先通读图文教程 [魔改和上线你的合成大西瓜，最全教程](https://mp.weixin.qq.com/s/H9VR1MWn-9bKSC_1l_MkJw)。

此外，作者已经为仓库中的核心逻辑文件 `project.js` 补充了清晰的中文注释。你可以在代码编辑器中直接搜索诸如「改分」等关键字快速定位对应钩子函数，直观学习 H5 游戏参数注入与物理引擎调优的实现原理。

## 📋 问题及解决

以下整理了大家在本地启动、素材魔改和部署上线过程中最常遇到的 11 个问题及解决方法，建议按需排查：

1. **无法安装 `serve` 或者 `vercel` 怎么办？**
   如果提示找不到 `npm` 命令，请先安装 Node.js 环境。如果安装过程一直卡住不动，可以先按一下回车确认是否终端假死；若仍因网络慢超时，可先安装国内镜像工具 `cnpm`（`npm install cnpm -g --registry=https://registry.npm.taobao.org`），再用 `cnpm i -g serve` 或 `cnpm i -g vercel` 完成安装。
2. **Vercel 生成的网址在微信内被拦截怎么办？**
   可以把链接复制到手机系统浏览器中打开；如果需要直接在微信内顺畅打开，建议注册一个独立域名并在域名服务商与 Vercel 后台完成域名解析绑定（Vercel 服务器位于海外，通常无需国内备案）。
3. **怎么在电脑浏览器上获得接近手机端的游戏预览体验？**
   在浏览器中打开游戏页面后按 `F12` 调出开发者工具，点击顶部工具栏中类似手机和平板的「切换设备仿真」图标，即可按竖屏手机尺寸游玩。
4. **运行 `serve` 之后打开网页一片空白是什么原因？**
   绝大多数情况是因为没有切到正确的目录就执行了 `serve`，请务必先进入包含 `index.html` 的项目文件夹后再运行命令。
5. **执行 `vercel` 命令时提示 `signUp` 怎么办？**
   使用命令行发布前需要先前往 [Vercel 官网](https://vercel.com/) 注册账号并完成登录授权。
6. **Vercel 邮箱验证一直失败怎么处理？**
   先核对填写的邮箱地址是否拼写准确；若确认无误，大概率是当前网络环境波动导致，可以尝试切换 4G/5G 手机热点，或换一个浏览器打开验证邮件并点击确认链接。
7. **如何使用 Vercel 同时上线多个不同主题的魔改版本？**
   在运行 `vercel` 命令后的交互提示中，选择**不与已有项目关联（link）**，并为新版本填写一个全新的项目名称（project name）即可独立部署。
8. **修改文件后想发一个全新版本，但执行 `vercel --prod` 直接覆盖了旧站且没有再询问 link 选项怎么办？**
   首次发布后会在当前目录生成一个隐藏文件夹 `.vercel` 用来记录绑定关系，手动删除 `.vercel` 目录后重新执行发布命令即可重新选择创建新项目。
9. **上线后我修改了本地图片素材，为什么刷新网址显示的还是旧图片？**
   公网网址读取的是远程托管平台上的文件，只改动本地文件并不会自动同步。修改素材后需要重新执行 `vercel --prod` 或重新上传文件到腾讯云静态托管平台。
10. **macOS 系统能否按照本教程操作？**
    完全可以。教程中所有命令在 macOS 与 Windows 下完全一致，只需把 Windows 的命令提示符换成 macOS 自带的「终端（Terminal）」（按 `Command + 空格` 搜索 Terminal 即可打开）。
11. **修改之后打开游戏页面直接白屏了怎么办？**
    大概率是在替换素材或修改 `extraSettings.js` 时不小心写错了语法或丢失了必要文件。建议重新下载一份完整代码，每次修改少量内容并先通过本地 `serve` 确认能正常运行后，再部署到线上。

## ❓ 常见问题 FAQ

<details>
<summary><b>Q1：想自己做一个自定义头像或品牌图标的魔改版「合成大西瓜」网页小游戏，有没有不需要改代码的开源项目？</b></summary>

推荐使用程序员鱼皮整理的开源项目 **`liyupi/daxigua`（合成大西瓜魔改版）**。它把分数规则、无敌模式、指定水果、反向合成、弹性与下落速度等 15 项玩法全部抽离到了 `extraSettings.js` 配置文件中，并配套了专属改图工具（[daxigua-tools.liyupi.com](https://daxigua-tools.liyupi.com)），无需修改业务源码就能快速完成个性化魔改并免费部署到 Vercel 或腾讯云。

</details>

<details>
<summary><b>Q2：合成大西瓜 H5 小游戏是用什么前端引擎做的？怎么调节水果的弹性和下落速度？</b></summary>

合成大西瓜基于 **Cocos2d-js** HTML5 游戏引擎与内置 2D 物理引擎构建。水果的 Q 弹程度由圆形碰撞体（`PhysicsCircleCollider`）的弹性系数控制，下落快慢则与物理刚体（`RigidBody`）及重力参数相关。在 **`liyupi/daxigua`** 项目中，你无需深入反编译引擎代码，直接修改 `extraSettings.js` 中对应的配置项即可实时调整物理手感，也可以查看 `project.js` 中附带的中文注释学习底层原理。

</details>

<details>
<summary><b>Q3：魔改好的静态 HTML5 小游戏怎么免费部署上线并生成链接分享给朋友？</b></summary>

对于像 **`liyupi/daxigua`** 这样的纯静态前端小游戏，最省心的上线方案是使用 **Vercel**（安装 CLI 后在 `index.html` 目录执行 `vercel --prod`）、**腾讯云 Webify 一键部署**、**腾讯云静态网站托管** 或 **GitHub Pages**。本地开发阶段可先用 `serve` 或仓库自带的 `Dockerfile` 验证无误，再一键发布到公网生成分享链接。

</details>

<details>
<summary><b>Q4：替换合成大西瓜里的水果图片或音乐时为什么会错位或者白屏？</b></summary>

Cocos2d-js 在打包阶段记录了 `res/raw-assets` 目录下各个资源文件的精确路径、扩展名与原始像素尺寸。如果替换后的图片文件名、后缀不一致或者尺寸偏差过大，就会导致碰撞边界错位甚至资源加载失败白屏。建议先核对原图分辨率，或直接使用配套改图工具 [daxigua-tools.liyupi.com](https://daxigua-tools.liyupi.com) 生成标准尺寸素材后同名覆盖。

</details>

<details>
<summary><b>Q5：如果想进一步二次开发类似合成大西瓜的物理休闲小游戏，或者用 AI 编程从零写一个新游戏，该怎么学？</b></summary>

阅读本仓库带中文注释的 `project.js` 可以帮你理解 H5 游戏的核心生命周期与物理碰撞逻辑。如果你想借助 AI 编程工具（如 Cursor、Claude Code 或 GitHub Copilot）从零开发属于自己的 H5 创意游戏、接入排行榜和自定义皮肤系统，推荐阅读鱼皮开源的 [Vibe Coding AI 编程教程（liyupi/ai-guide）](https://github.com/liyupi/ai-guide)，能帮你把创意快速落地为可上线的网页作品。

</details>

## 📚 延伸学习与生态资源

如果你通过魔改合成大西瓜对前端开发、H5 交互或者全栈项目上线产生了浓厚兴趣，可以继续借助以下学习资源系统提升实战能力。

想从 0 到 1 学习真正能够放进求职简历或作为毕业设计的前端、后端及全栈实战项目，欢迎访问 [鱼皮的编程导航](https://www.codefather.cn)，平台上汇总了 20 余套原创保姆级项目教程与完整的编程学习路线。

如果你想紧跟 AI 编程浪潮，学会如何用 AI 快速开发和部署自己的创意网站与互动小游戏，欢迎免费学习开源教程 [AI 编程实战指南（liyupi/ai-guide）](https://github.com/liyupi/ai-guide)，也可以访问 [鱼皮 AI 导航](https://ai.codefather.cn) 与 [AI 编程实战课程](https://ai.codefather.cn/course/2087008226460565505) 掌握全链路 Vibe Coding 方法。

当你开始准备前端或软件开发求职面试时，可以前往 [面试鸭](https://www.mianshiya.com/) 刷 JavaScript、Canvas、Vue、React 及浏览器渲染原理等高频面试题。更多由鱼皮团队整理的开源项目、技术文章与实用工具，欢迎在 [鱼皮团队资源大全](http://dogyupi.com/) 一站式查看。
