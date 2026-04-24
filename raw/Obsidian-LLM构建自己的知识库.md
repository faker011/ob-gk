---
title: "Obsidian-LLM构建自己的知识库"
source: "https://codemx.cn/2026/04/07/obsidian-wiki/index.html"
author:
  - "[[墨香]]"
published: 2026-04-07
created: 2026-04-24
description: "​	前几天Karpathy分享了他最新的工作流：使用 LLM 构建个人知识库（Personal Knowledge Base），这条推文一发布，引发大量关注和点赞，两天后，他把这套方法论写成了一份 gist 发到 GitHub（llm-wiki） 上，开源给所有人。 ​	我最近也看到很多介绍这个构建知识库的帖子，但是很少有如何实战构建自己的知识库的操作步骤，所以开始也是很迷茫，到底该如何构建自己的"
tags:
  - "clippings"
---
前几天Karpathy分享了他最新的工作流： **使用 LLM 构建个人知识库（Personal Knowledge Base）** ，这条推文一发布，引发大量关注和点赞，两天后，他把这套方法论写成了一份 gist 发到 GitHub（ [llm-wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) ） 上，开源给所有人。

我最近也看到很多介绍这个构建知识库的帖子，但是很少有如何实战构建自己的知识库的操作步骤，所以开始也是很迷茫，到底该如何构建自己的知识库，正好今天没事找到一篇介绍如何使用的，我本地也实战了一下，记录一下操作步骤。

知识收集、整理是非常耗费时间的，我做开发十多年也整理了很多知识，放到github，博客，公众号，但是没有一个非常好的的管理方式，正好这个方法能够解决我的问题，可能也会解决很多人管理知识的问题。

下面我介绍下我的操作步骤。

## 准备工具

- Obsidian – [https://obsidian.md/](https://obsidian.md/) ：下载安装，这个是一个读取显示md文件的软件，具有很强大的功能，由于我也是刚开接触，因此很多还不熟悉，因此还在摸索阶段。
- obsidian web clipper – [https://obsidian.md/clipper：这是一款浏览器插件，用来快速收藏你需要放到知识库的网页。](https://obsidian.md/clipper%EF%BC%9A%E8%BF%99%E6%98%AF%E4%B8%80%E6%AC%BE%E6%B5%8F%E8%A7%88%E5%99%A8%E6%8F%92%E4%BB%B6%EF%BC%8C%E7%94%A8%E6%9D%A5%E5%BF%AB%E9%80%9F%E6%94%B6%E8%97%8F%E4%BD%A0%E9%9C%80%E8%A6%81%E6%94%BE%E5%88%B0%E7%9F%A5%E8%AF%86%E5%BA%93%E7%9A%84%E7%BD%91%E9%A1%B5%E3%80%82)

先将如上两个软件安装。

## 创建项目

安装完成后，在你的电脑本地新建一个项目文件夹，例如：obsidian，然后在下面新建raw文件夹和wiki文件夹，如果你已经有了知识库，可以拷贝过来放到raw目录下，直接放置就行不用整理。

然后打开Obsidian，点击菜单中的File->Open Vault，然后选择打开本地仓库，选择你创建的这个文件夹（obsidian）即可，选择后，Obsidian会扫描里面的内容并构建索引，然后点击左侧菜单中的查看关系图谱可以看到如下图：

有图可以放大缩小，点击可以跳转，不过这个不是今天的重点。

## 收藏知识点

先用Obsidian打开你的项目

然后在浏览器中查看到需要收藏的网页时，点击上面安装的obsidian web clipper插件，会弹出如下弹窗：

![68d1d735-d525-44a4-815f-cd6bd0208910](https://codemx.cn/images/AI/LLMWIKI/Clipper.png)

可以修改tags，以及最下面的 `Clippings` ，这个是保存文件夹，我们改为raw，这样就会直接保存到你这个查看的内容到raw的文件夹下，方便快速收藏。

## 开始编译

### 准备工作

Obsidian的skill：

- [kepano/obsidian-skills: Agent skills for Obsidian. Teach your agent to use Markdown, Bases, JSON Canvas, and use the CLI.](https://github.com/kepano/obsidian-skills)（ [https://github.com/kepano/obsidian-skills），如果是使用claude-code，则安装里面的直接安装即可，如果是使用codex，需要手动下载复制到.codex/skill文件夹中。](https://github.com/kepano/obsidian-skills%EF%BC%89%EF%BC%8C%E5%A6%82%E6%9E%9C%E6%98%AF%E4%BD%BF%E7%94%A8claude-code%EF%BC%8C%E5%88%99%E5%AE%89%E8%A3%85%E9%87%8C%E9%9D%A2%E7%9A%84%E7%9B%B4%E6%8E%A5%E5%AE%89%E8%A3%85%E5%8D%B3%E5%8F%AF%EF%BC%8C%E5%A6%82%E6%9E%9C%E6%98%AF%E4%BD%BF%E7%94%A8codex%EF%BC%8C%E9%9C%80%E8%A6%81%E6%89%8B%E5%8A%A8%E4%B8%8B%E8%BD%BD%E5%A4%8D%E5%88%B6%E5%88%B0.codex/skill%E6%96%87%E4%BB%B6%E5%A4%B9%E4%B8%AD%E3%80%82)

编译是需要skill的，我在网上找了几个：

- [lewislulu/llm-wiki-skill: Karpathy-style LLM knowledge base Agent Skill for OpenClaw/Codex. Experimental — will iterate over time.](https://github.com/lewislulu/llm-wiki-skill)([https://github.com/lewislulu/llm-wiki-skill](https://github.com/lewislulu/llm-wiki-skill))
- [skills/skills/karpathy-kb at main · pedronauck/skills](https://github.com/pedronauck/skills/tree/main/skills/karpathy-kb) ([https://github.com/pedronauck/skills/tree/main/skills/karpathy-kb](https://github.com/pedronauck/skills/tree/main/skills/karpathy-kb))
- [Astro-Han/karpathy-llm-wiki: One skill to build your own Karpathy-style LLM wiki.](https://github.com/Astro-Han/karpathy-llm-wiki)([https://github.com/Astro-Han/karpathy-llm-wiki](https://github.com/Astro-Han/karpathy-llm-wiki))
- [SamurAIGPT/llm-wiki-agent: A personal knowledge base that builds and maintains itself. Drop in sources — Claude (or Codex/Gemini) reads them, extracts knowledge, and maintains a persistent interlinked wiki. Works with Claude Code, Codex, OpenCode, Gemini CLI. No API key needed.](https://github.com/SamurAIGPT/llm-wiki-agent)([https://github.com/SamurAIGPT/llm-wiki-agent](https://github.com/SamurAIGPT/llm-wiki-agent))
- [sdyckjq-lab/llm-wiki-skill: 基于 Karpathy llm-wiki 方法论的个人知识库构建 Skill，支持多平台！](https://github.com/sdyckjq-lab/llm-wiki-skill)

还需要 `Karpathy` 开源的 [llm-wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) ([https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)，这个可以好好读一下，毕竟是大神写的。](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f\)%EF%BC%8C%E8%BF%99%E4%B8%AA%E5%8F%AF%E4%BB%A5%E5%A5%BD%E5%A5%BD%E8%AF%BB%E4%B8%80%E4%B8%8B%EF%BC%8C%E6%AF%95%E7%AB%9F%E6%98%AF%E5%A4%A7%E7%A5%9E%E5%86%99%E7%9A%84%E3%80%82)

这里我使用的是codex + `lewislulu/llm-wiki-skill` （这是个skill、模板、脚本），也可以参考这个自己写一个。

### 全量编译

执行codex，然后输入：

```
Learn this skill（https://github.com/lewislulu/llm-wiki-skill） and, based on the content at
https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f#file-llm-wiki-md, construct a complete wiki under the wiki folder by reading all the details in the raw folder. Make it a well-structured and clean wiki. Ensure that log.md and index.md are preserved.
```

中文：

```
学习该 skill（https://github.com/lewislulu/llm-wiki-skill），并基于https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f#file-llm-wiki-md 的内容，通过读取 raw目录中的所有细节，在 wiki 目录下构建一个完整的 wiki。将其整理为结构清晰、规范良好的知识库。确保保留 log.md 和 index.md。
```

编译开始：

![start](https://codemx.cn/images/AI/LLMWIKI/start1.png)

编译结束：

编译产物：

可以看到已经编译完成了。

然后就可以使用Obsidian查看了，也可以使用AI进行搜索，例如：

### 增量编译

```
Please ingest the latest materials I placed in the raw folder into my wiki.
```

中文：

```
请ingest我最新放入raw里的资料到我的wiki
```

执行上面命令即可。

## 最后

这样一个自己的知识库就构建好了，那么核心就是你要去收集你要的知识，然后直接放到raw下面即可，不用整理。如果需要同步，可以使用github进行保存，也可以使用其他方式。

文章作者: [墨香](http://www.codemx.cn/)

版权声明: 本博客所有文章除特别声明外，均采用 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 许可协议。转载请注明来自 [墨香博客](http://www.codemx.cn/) ！