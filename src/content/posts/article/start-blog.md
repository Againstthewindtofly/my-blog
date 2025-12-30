---
title: 技术分享|在2025年搭建个人博客
description: 赶在2025的尾巴，终于搭建起了个人博客
published: 2025-12-30
tags: [技术分享, 博客, Astro, Firefly]
category: 技术分享
draft: true
---

之前就有想过搭建一个个人博客，但后面由于种种原因没有施行。选择使用笔记来记录，其实就是太懒了...因为我希望能够完全拥有对笔记所有权利，所以选择了本地优先的[思源笔记](https://b3log.org/siyuan/)。这导致想要分享笔记时就会非常麻烦。

## 技术选型
我对博客的要求很简单，第一，尽量免费，第二，我拥有数据的所有权。明确了需求，剩下的就很简单了，直接问Gemini：如果我要在2025年搭建个人博客，你推荐我用什么实现？

Gemini 给了我一些推荐，主要是分为传统带后台类的 CMS 内容管理系统，如：[WordPress](https://wordpress.org/)，[Halo](https://halo.run/)；和 Markdown + 静态导出 组合的，比如：[Astro](https://astro.build/)，[Hexo](https://hexo.io/)；还有用 Notion 类作为内容管理的，比如：[NotionNext](https://github.com/tangly1024/NotionNext)

让我来选的话，我只会在 Astro 和 Hexo 中选。Halo 类的需要服务器搭建，不能随时写；Notion 类的数据不在自己手里，不考虑。还有一点，我觉得 Markdown 这种标记语言记录的方式天生就更适合 AI。

Astro 和 Hexo 的选择很难，但在 AI 眼里很简单，无脑选择支持 [Tailwind CSS](https://tailwindcss.com/) 的 Astro。为了更好的跟上 AI 浪潮，我选择听 AI 的。（话说 AI 是真喜欢 Tailwind 呀）

| 需求场景 | 推荐方案 | 理由 |
| :--- | :--- | :--- |
| **纯技术人，追求极致性能和定制** | **[Astro](https://astro.build/)** | 2025 年的最佳平衡点，性能王。 |
| **懒人，只想在手机上写笔记就发博客** | **[NotionNext](https://github.com/tangly1024/NotionNext)** | 牺牲一点性能和控制权，换取极致的写作便利。 |
| **想要像 WordPress 一样有后台管理界面** | **[Halo](https://halo.run/)** | 适合不想折腾代码、喜欢图形化后台的用户（需自备服务器）。 |
| **老牌稳定，习惯传统的 Markdown 流程** | **[Hexo](https://hexo.io/)** | 经典但略显疲态，如果你已经习惯了它的生态，依然可用。 |

## 搭建流程

明确了搭建用的技术，接下来就是选择一个自己喜欢的主题。这里可以看 [Astro 的主题商店](https://astro.build/themes/)，有很多免费的可供选择。我选择的是 [**Firefly**](https://github.com/CuteLeaf/Firefly)，清新好看。

### 安装

根据 [Firefly 官方文档](https://docs-firefly.cuteleaf.cn/guide/get-started/)，安装步骤如下：

1. **环境准备**：确保你的系统安装了 Node.js (>= 20)、pnpm (>= 9) 和 Git。
2. **获取代码**：首先在 GitHub 上 [**Fork**](https://github.com/CuteLeaf/Firefly/fork) 该项目，或者点击 [**Use this template**](https://github.com/CuteLeaf/Firefly/generate) 使用模板创建到你自己的仓库。然后将其克隆到本地：
   ```bash
   git clone https://github.com/your-github-name/Firefly.git
   cd Firefly
   ```
3. **安装依赖**：
   ```bash
   pnpm install
   ```
4. **本地开发**：运行 `pnpm dev` 启动开发服务器，在浏览器访问 `http://localhost:4321` 查看。
5. **打包网站**：运行 `pnpm build` 将网站打包成静态文件，生成到 `dist` 目录。

### 配置

Firefly 的配置非常直观，大部分个性化设置都集中在 `src/config/` 目录下。你可以通过编辑这些文件来自定义你的博客：

- **`siteConfig.ts`**：站点基础设置，包括网站标题、语言（如 `zh_CN`）、主题色以及是否开启某些特性。
- **`profileConfig.ts`**：个人资料设置，你可以在这里配置头像、昵称、个人简介以及社交媒体链接。
- **`navConfig.ts`**：导航栏菜单项的配置。
- **`commentConfig.ts`**：评论系统配置，支持 [Waline](https://waline.js.org/)、[Giscus](https://giscus.app/)、[Twikoo](https://twikoo.js.org/) 等多种主流方案。
- **`footerConfig.ts`** & **`FooterConfig.html`**：用于自定义页脚文本或注入自定义 HTML 内容。
- **`announcementConfig.ts`**：配置站点顶部的公告栏。

更多高级配置（如代码高亮、樱花特效等）也可以在对应的配置文件中找到。详细的配置说明可以参考 [Firefly 官方配置文档](https://docs-firefly.cuteleaf.cn/guide/configuration/)。

### 部署

一开始我尝试用 GitHub Pages 部署但遇到了问题，懒得研究了，直接换成 [Vercel](https://vercel.com/)，其部署流程非常顺滑：

1. **代码托管**：将你的代码推送到 GitHub 等 Git 平台。
2. **导入项目**：登录 Vercel，点击 "Add New Project" 并导入你的仓库。
3. **自动识别**：Vercel 会自动检测到这是 Astro 项目并预设好构建配置。
4. **完成发布**：点击 "Deploy" 即可完成部署。

未来我也许会尝试部署到 [EdgeOne Pages](https://edgeone.ai/products/pages) 以优化国内访问速度。但是我测试 Vercel 绑定自定义域名后在国内的访问表现也相当不错。

## 尾声
到这里，我的博客就上线了，感谢你的浏览~