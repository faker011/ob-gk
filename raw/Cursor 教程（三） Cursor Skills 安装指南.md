---
title: "Cursor 教程（三）| Cursor Skills 安装指南"
source: "https://blog.csdn.net/qq_20236937/article/details/158284199"
author:
  - "[[qq_20236937]]"
published: 2026-02-22
created: 2026-04-24
description: "文章浏览阅读7.2k次，点赞31次，收藏72次。Cursor 教程（三）| Cursor Skills 安装指南_cursor skills"
tags:
  - "clippings"
---
## 第一章：认识 Cursor Skills

### 1.1 什么是 Cursor Skills

Cursor Skills 是一种标准化的指令文件格式,用于为 AI 代理提供专业能力和领域知识。通过 Skills,你可以:

- 📦 **封装可复用的工作流程** - 将重复性任务标准化
- 🎯 **提供专业领域知识** - 教会 AI 特定技术栈的最佳实践
- 🔄 **跨项目共享** - 在多个项目中复用相同的技能
- 🤝 **团队协作** - 统一团队的开发规范和流程

### 1.2 Skills vs Rules 的区别

| 特性 | Skills (技能) | Rules (规则) |
| --- | --- | --- |
| **用途** | 任务执行指南 | 项目约定和规范 |
| **触发方式** | AI 根据上下文自动选择 | 始终应用或手动应用 |
| **适用场景** | “如何执行某个任务” | “项目的通用约定” |
| **示例** | “如何编写单元测试” | “使用 TypeScript 严格模式” |

---

## 第二章：核心概念与术语

### 2.1 SKILL.md 文件

这是技能的核心文件,**文件名必须是 `SKILL.md`** (全大写),包含:

- YAML 前置元数据(name, description 等)
- 技能的详细指令和使用说明

### 2.2 技能目录

Skills 可以存储在以下位置:

| 路径 | 作用域 | 说明 |
| --- | --- | --- |
| `.cursor/skills/` | 项目级 | Cursor IDE 标准路径 |
| `.claude/skills/` | 项目级 | Claude Code 标准路径(openskills 默认) |
| `.agent/skills/` | 项目级 | 通用多代理路径(使用 --universal 标志) |
| `~/.cursor/skills/` | 全局用户级 | 所有项目可用 |
| `~/.claude/skills/` | 全局用户级 | Claude Code 全局路径(openskills --global) |

**重要说明**:

- `openskills` 默认安装到 `.claude/skills/` (项目级) 或 `~/.claude/skills/` (全局)
- 使用 `--universal` 标志会安装到 `.agent/skills/` 目录
- Cursor 会自动识别这些目录中的技能

### 2.3 AGENTS.md 文件

由 `openskills` 工具自动生成的索引文件,列出所有可用技能及其描述,帮助 AI 快速了解可用能力。

---

## 第三章：技能目录结构详解

### 3.1 什么是"项目根目录"?

**项目根目录** 就是你用 Cursor 打开的项目 文件夹 ,通常包含 `package.json` 、 `README.md` 等文件。

**实际例子**:

假设你有一个项目叫 `my-website`,完整路径是:

- Windows: `D:\projects\my-website`
- Mac/Linux: `/Users/yourname/projects/my-website`

当你在 Cursor 中打开这个项目时,`my-website` 就是 **项目根目录** 。

**项目根目录通常包含**:

```
my-website/              ← 这就是项目根目录
├── package.json         ← 项目配置文件
├── README.md            ← 项目说明
├── src/                 ← 源代码文件夹
├── node_modules/        ← 依赖包
└── .git/                ← Git 版本控制
123456
```

### 3.2 技能文件应该放在哪里?

**在项目根目录下创建 `.cursor` 文件夹**,然后在里面创建 `skills` 文件夹。

**完整的目录结构示例**:

```
my-website/                    ← 项目根目录(用 Cursor 打开的文件夹)
├── .cursor/                   ← 在根目录下创建(与 src、package.json 同级)
│   └── skills/                ← 在 .cursor 里创建 skills 文件夹
│       ├── code-review/       ← 第一个技能
│       │   └── SKILL.md       ← 技能文件
│       └── api-generator/     ← 第二个技能
│           └── SKILL.md
├── src/                       ← 你的源代码(与 .cursor 同级)
├── package.json               ← 项目配置(与 .cursor 同级)
└── README.md                  ← 项目说明(与 .cursor 同级)
12345678910
```

**关键点**:

- ✅ `.cursor` 文件夹与 `src` 、 `package.json` 等在 **同一层级**
- ✅ 不是在 `src` 里面创建 `.cursor`
- ✅ 不是在其他子文件夹里创建 `.cursor`

### 3.3 标准结构(推荐)

```
项目根目录/
├── .cursor/
│   └── skills/
│       ├── my-skill/           # 技能文件夹(kebab-case 命名)
│       │   ├── SKILL.md        # 核心文件(必须大写)
│       │   ├── template.ts     # 可选:代码模板
│       │   └── example.json    # 可选:示例文件
│       └── another-skill/
│           └── SKILL.md
└── AGENTS.md                   # 可选:技能索引文件(与 .cursor 同级)
12345678910
```

### 3.4 如何在 Cursor 中找到项目根目录?

**方法 1: 查看 Cursor 窗口标题**

- 窗口标题会显示当前打开的文件夹名称

**方法 2: 查看左侧文件树**

- 左侧文件树最顶层的文件夹就是项目根目录

**方法 3: 使用终端**

```bash
# 在 Cursor 中打开终端(Ctrl+\` 或 Cmd+\`)
# 执行以下命令查看当前目录
pwd          # Mac/Linux
cd           # Windows CMD
pwd          # Windows PowerShell
bash12345
```

### 3.5 关键规则

1. **文件夹命名**: 使用 kebab-case(小写字母+连字符),如 `code-review` 、 `api-generator`
2. **SKILL.md 命名**: 必须是 `SKILL.md` (全大写),不能是 `skill.md` 或其他名称
3. **name 字段匹配**: YAML 中的 `name` 字段应与文件夹名一致

---

## 第四章：三种安装方式

### 4.1 方式一: 使用 openskills 命令行工具 (推荐)

**适用场景**: 批量管理技能、自动化安装、团队协作

#### 步骤 1: 安装 Node.js

确保已安装 Node.js v18 或更高版本:

```bash
node -v  # 检查版本
bash1
```

如未安装,访问 [nodejs.org](https://nodejs.org/) 下载 LTS 版本。

#### 步骤 2: 安装 openskills

```bash
npm install -g openskills
bash1
```

**权限问题处理**:

```bash
# Mac/Linux 如果提示权限不足
sudo npm install -g openskills

# Windows 如果提示权限不足
# 以管理员身份运行 PowerShell 或 CMD,然后执行上面的命令
bash12345
```

#### 步骤 3: 从 GitHub 安装技能

**⚠️ 核心说明**:

- `openskills install` 命令是从 **GitHub** 下载技能仓库
- **所有从 GitHub 安装的操作都需要外网访问**
- 国内用户需要使用代理/VPN,或手动下载后本地安装

**基本格式**:

```bash
openskills install GitHub用户名/仓库名
bash1
```

这个命令会从 `https://github.com/用户名/仓库名` 下载技能。

---

**最常用: 安装 Anthropic 官方技能库**

```bash
# 进入你的项目目录
cd /path/to/your/project

# 安装官方技能库(推荐,包含多个高质量技能)
openskills install anthropics/skills
bash12345
```

这会从 `https://github.com/anthropics/skills` 下载官方技能库。

**为什么推荐安装官方库?**

- ✅ Anthropic 官方维护,质量有保证
- ✅ 包含多个实用技能(代码审查、API 生成、测试编写等)
- ✅ 持续更新和维护
- ✅ 社区广泛使用

---

**安装其他 GitHub 用户的技能**

如果其他开发者在 GitHub 上分享了技能仓库,你也可以安装:

```bash
# 格式: openskills install GitHub用户名/仓库名

# 示例 1: 安装用户 eastlondoner 的 cursor-tools 仓库
openskills install eastlondoner/cursor-tools

# 示例 2: 安装你自己的技能仓库
openskills install your-username/my-cursor-skills

# 示例 3: 安装团队的私有技能库(需要 GitHub Token)
openskills install your-company/team-skills
bash12345678910
```

**安装特定版本或分支**:

```bash
# 安装特定分支
openskills install anthropics/skills#main
openskills install anthropics/skills#develop

# 安装特定标签/版本
openskills install eastlondoner/cursor-tools#v2.0.0
openskills install your-username/my-skills#v1.5.0
bash1234567
```

---

**国内用户: 无法访问 GitHub 的解决方案**

**方法 1: 设置代理**

```bash
# Mac/Linux
export https_proxy=http://127.0.0.1:7890  # 替换为你的代理地址和端口
export http_proxy=http://127.0.0.1:7890
openskills install anthropics/skills

# Windows CMD
set https_proxy=http://127.0.0.1:7890
set http_proxy=http://127.0.0.1:7890
openskills install anthropics/skills

# Windows PowerShell
$env:https_proxy="http://127.0.0.1:7890"
$env:http_proxy="http://127.0.0.1:7890"
openskills install anthropics/skills
bash1234567891011121314
```

**方法 2: 手动下载后本地安装**

```bash
# 步骤 1: 在浏览器中访问(需要能访问 GitHub)
# https://github.com/anthropics/skills

# 步骤 2: 点击绿色的 "Code" 按钮 → "Download ZIP"

# 步骤 3: 解压 ZIP 文件到本地,例如解压到:
# D:\downloads\anthropics-skills-main

# 步骤 4: 使用本地路径安装
openskills install ./anthropics-skills-main
# 或使用绝对路径
openskills install D:\downloads\anthropics-skills-main
bash123456789101112
```

---

**其他安装选项**

**全局安装** (所有项目可用):

```bash
openskills install anthropics/skills --global
# 安装到 ~/.claude/skills/,所有项目都能使用这些技能
bash12
```

**通用模式** (多代理兼容):

```bash
openskills install anthropics/skills --universal
# 安装到 .agent/skills/,兼容 Cursor、Claude Code 等多种 AI 代理
bash12
```

**本地路径安装** (不需要访问 GitHub):

```bash
# 安装本地技能文件夹
openskills install ./my-custom-skill

# 安装绝对路径
openskills install /Users/username/my-skills/custom-skill
bash12345
```

#### 步骤 4: 交互式选择

安装命令会打开交互式界面:

```bash
openskills install anthropics/skills
bash1
```

**界面示例** (默认全部选中):

```
? Select skills to install (Press <space> to select, <a> to toggle all, <i> to invert selection)
❯◉ code-review
 ◉ api-generator
 ◉ test-writer
 ◉ documentation
 ◉ refactor-helper
123456
```

**⚠️ 注意**: 默认情况下所有技能都是选中状态(◉),不是未选中(◯)!

**操作说明**:

- `↑↓` 方向键: 上下移动光标
- `空格`: 选中/取消选中当前项 (◉ ↔ ◯)
- `a`: 全选/全不选切换
- `i`: 反选(已选变未选,未选变已选)
- `回车`: 确认安装选中的技能

**选择技能**:

1. 用方向键移动到需要的技能
2. 按空格选中(◯ 变成 ◉)
3. 重复步骤 1-2 选择多个技能
4. 按回车确认安装

**快速安装所有技能** (跳过交互式选择):

```bash
openskills install anthropics/skills --yes
# 或简写
openskills install anthropics/skills -y
bash123
```

**选择后的示例**:

```
? Select skills to install
 ◉ code-review
 ◉ api-generator
 ◯ test-writer          ← 取消选中
 ◉ documentation
 ◯ refactor-helper      ← 取消选中

✓ Installing 3 skills...
✓ code-review installed to .claude/skills/code-review
✓ api-generator installed to .claude/skills/api-generator
✓ documentation installed to .claude/skills/documentation
1234567891011
```

#### 步骤 5: 同步技能(重要)

```bash
openskills sync
bash1
```

**这个命令的作用**:

1. 扫描已安装的所有技能
2. 生成 `AGENTS.md` 索引文件
3. 让 Cursor 能够识别和使用这些技能

**执行后的输出示例**:

```
✓ Scanning skills...
✓ Found 3 skills:
  - code-review (v1.0.0)
  - api-generator (v2.1.0)
  - documentation (v1.5.0)
✓ Generated AGENTS.md
✓ Skills synced successfully!
1234567
```

**生成的 AGENTS.md 文件示例**:

```markdown
# Available Skills

<available_skills>

## code-review
对代码变更进行全面审查,关注最佳实践、安全性和性能。

## api-generator
根据规范自动生成 REST API 端点代码。

## documentation
为代码自动生成文档注释和 README 文件。

</available_skills>
markdown1234567891011121314
```

**重要提示**:

- 每次安装新技能后都要运行 `openskills sync`
- 如果技能不显示,尝试重新运行 `openskills sync`
- 同步后无需重启 Cursor,技能会自动加载

#### 优缺点对比

| 维度 | 优点 | 缺点 |
| --- | --- | --- |
| **操作难度** | 命令行操作,适合开发者 | 需要基本的命令行知识 |
| **灵活性** | 可选择安装单个或多个技能 | \- |
| **管理** | 支持版本管理和更新 | \- |
| **安装范围** | 支持项目级和全局安装 | \- |
| **依赖** | 需要 Node.js 环境 | 需要先安装 Node.js |
| **网络要求** | 从 GitHub 安装需要外网 | 国内用户需要代理或手动下载 |
| **自动化** | 自动生成 AGENTS.md 索引 | \- |
| **适用场景** | 适合长期使用和团队协作 | 不适合快速体验 |

---

### 4.2 方式二: 从 GitHub 直接导入

**适用场景**: 快速体验、无需命令行

**⚠️ 网络要求**: 此方法需要能够访问 GitHub,国内用户可能需要使用代理或 VPN。

#### 操作步骤

**步骤 1: 打开 Cursor 设置**

- Mac: `Cmd + Shift + J`
- Windows/Linux: `Ctrl + Shift + J`
- 或点击左下角齿轮图标 → Settings

**步骤 2: 导航到规则设置**

- 点击左侧菜单的 **Settings**
- 找到 **Rules** 或 **Rules and Commands** 选项卡
- 在 **Project Rules** 区域操作

**步骤 3: 添加远程规则**

- 点击 **Add Rule** 按钮
- 选择 **Remote Rule (Github)** 选项
- 如果没有看到这个选项,可能需要更新 Cursor 到最新版本

**步骤 4: 输入仓库 URL**

**官方技能库**:

```
https://github.com/anthropics/skills
1
```

**其他示例**:

```
https://github.com/eastlondoner/cursor-tools
https://github.com/your-username/your-skills-repo
12
```

**步骤 5: 确认并等待加载**

- 点击确认按钮
- Cursor 会自动拉取仓库内容
- 等待几秒钟,技能会自动加载

**界面位置参考**:

```
Cursor 设置窗口
├── General (通用)
├── Features (功能)
├── Rules (规则) ← 在这里
│   ├── User Rules (用户规则)
│   ├── Project Rules (项目规则) ← 点击这里的 Add Rule
│   └── Agent Decides (代理决定)
└── Beta (测试功能)
12345678
```

#### 私有仓库处理

如需导入私有仓库,需要 GitHub Personal Access Token (PAT):

**步骤 1: 生成 GitHub Token**

1. 登录 GitHub
2. 点击右上角头像 → **Settings**
3. 左侧菜单最底部 → **Developer settings**
4. 点击 **Personal access tokens** → **Tokens (classic)**
5. 点击 **Generate new token** → **Generate new token (classic)**
6. 设置 Token:
	- Note: 填写描述,如 “Cursor Skills Access”
		- Expiration: 选择过期时间(建议 90 days 或 No expiration)
		- 勾选权限: **repo** (完整的仓库访问权限)
7. 点击 **Generate token**
8. **立即复制 Token** (只显示一次!)

**步骤 2: 使用 Token 安装**

格式: `https://TOKEN@github.com/用户名/仓库名`

```
https://ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxx@github.com/your-company/private-skills
1
```

**真实示例**:

```
# 假设你的 Token 是: ghp_abc123def456ghi789
# 私有仓库是: acme-corp/internal-skills

在 Cursor 的 Remote Rule 输入框中填写:
https://ghp_abc123def456ghi789@github.com/acme-corp/internal-skills
12345
```

**安全提示**:

- ⚠️ 不要将包含 Token 的 URL 提交到公开仓库
- ⚠️ Token 泄露后立即在 GitHub 删除并重新生成
- ✅ 建议为不同用途创建不同的 Token
- ✅ 定期更新 Token

#### 优缺点对比

| 维度 | 优点 | 缺点 |
| --- | --- | --- |
| **操作难度** | 图形界面操作,简单直观 | \- |
| **技术要求** | 无需命令行知识 | \- |
| **速度** | 快速导入整个仓库 | \- |
| **灵活性** | \- | 无法选择单个技能 |
| **管理** | \- | 更新和管理不便 |
| **网络要求** | 需要访问 GitHub | 国内用户需要代理/VPN |
| **适用场景** | 适合快速体验和测试 | 不适合长期使用和精细管理 |

---

### 4.3 方式三: 手动创建自定义技能

**适用场景**: 个性化需求、团队专属工作流

详见下一章 [第五章：创建自定义技能](#%E7%AC%AC%E4%BA%94%E7%AB%A0%E5%88%9B%E5%BB%BA%E8%87%AA%E5%AE%9A%E4%B9%89%E6%8A%80%E8%83%BD) 。

---

## 第五章：创建自定义技能

### 5.1 基础结构

#### 步骤 1: 创建目录

**首先,确认你在项目根目录**:

假设你的项目叫 `my-website`,在 Cursor 中已经打开。

```bash
# 在 Cursor 中打开终端(Ctrl+\` 或 Cmd+\`)
# 确认当前在项目根目录
pwd    # 应该显示类似: /Users/yourname/projects/my-website
bash123
```

**创建技能目录**:

```bash
# Mac/Linux
mkdir -p .cursor/skills/my-skill

# Windows CMD
mkdir .cursor\skills\my-skill

# Windows PowerShell
New-Item -ItemType Directory -Path .cursor\skills\my-skill -Force
bash12345678
```

**创建后的结构**:

```
my-website/              ← 你的项目根目录
├── .cursor/             ← 新创建的文件夹
│   └── skills/          ← 新创建的文件夹
│       └── my-skill/    ← 新创建的技能文件夹
├── src/                 ← 你原有的代码
└── package.json         ← 你原有的文件
123456
```

#### 步骤 2: 创建 SKILL.md

在 `.cursor/skills/my-skill/` 目录下创建 `SKILL.md` 文件:

```markdown
---
name: my-skill
description: 简短描述这个技能的用途和触发时机
---

# My Skill

详细的技能说明和使用指南。

## 何时使用

- 当用户请求 XXX 时
- 当项目包含 YYY 文件时
- 当需要执行 ZZZ 任务时

## 执行步骤

1. 第一步:分析项目结构
2. 第二步:读取相关配置文件
3. 第三步:生成目标代码/文档
4. 第四步:验证结果并提示用户

## 注意事项

- 确保项目包含必要的依赖
- 遵循项目现有的代码风格
- 如有疑问,使用 ask questions 工具询问用户
markdown123456789101112131415161718192021222324252627
```

### 5.2 YAML 前置元数据详解

#### 必填字段

```yaml
---
name: my-skill              # 技能标识符(kebab-case)
description: 技能的简短描述  # 帮助 AI 判断何时使用
---
yaml1234
```

#### 可选字段

```yaml
---
name: my-skill
description: 技能的简短描述
: 你的名字
version: 1.0.0
disable-model-invocation: false  # true 则只能手动调用
---
yaml1234567
```

### 5.3 完整示例: 代码审查技能

```markdown
---
name: code-review
description: 对代码变更进行全面审查,关注最佳实践、安全性和性能。适用于审查 PR 或代码修改。
---

# 代码审查技能

系统化地审查代码变更,确保质量、安全性和可维护性。

## 何时使用

- 用户请求"审查代码"、"code review"、"检查这段代码"
- 用户提到"pull request"或"PR 审查"
- 用户询问代码质量或潜在问题

## 审查清单

### 1. 代码结构
- 函数和类的职责是否单一
- 代码组织是否清晰合理
- 命名是否具有描述性

### 2. 安全性
- 是否存在 SQL 注入风险
- 用户输入是否经过验证
- 敏感信息是否被正确处理

### 3. 性能
- 是否存在不必要的循环嵌套
- 数据库查询是否优化
- 是否有内存泄漏风险

### 4. 最佳实践
- 是否遵循项目编码规范
- 错误处理是否完善
- 是否有足够的注释

## 输出格式

审查结果应包含:
1. **优点**: 代码中做得好的地方
2. **问题**: 发现的问题及严重程度(高/中/低)
3. **建议**: 具体的改进建议和示例代码
4. **总结**: 整体评价和是否建议合并
markdown1234567891011121314151617181920212223242526272829303132333435363738394041424344
```

### 5.4 带资源文件的技能

对于复杂技能,可以包含额外的资源文件:

```
.cursor/skills/api-generator/
├── SKILL.md              # 主技能文件
├── template.ts           # TypeScript API 模板
├── template.py           # Python API 模板
└── openapi-schema.json   # OpenAPI 规范示例
12345
```

在 `SKILL.md` 中引用这些文件:

```markdown
## 模板文件

根据项目语言选择合适的模板:
- TypeScript 项目: 使用 \`template.ts\`
- Python 项目: 使用 \`template.py\`

参考 \`openapi-schema.json\` 了解 API 规范格式。
markdown1234567
```

### 5.5 优缺点对比

| 维度 | 优点 | 缺点 |
| --- | --- | --- |
| **定制化** | 完全个性化,满足特定需求 | \- |
| **控制权** | 完全掌控技能内容和逻辑 | \- |
| **网络要求** | 不需要访问外网 | \- |
| **团队协作** | 可创建团队专属工作流 | \- |
| **学习成本** | \- | 需要理解 SKILL.md 格式 |
| **维护** | \- | 需要自己维护和更新 |
| **时间成本** | \- | 需要时间编写和测试 |
| **适用场景** | 适合有特殊需求的场景 | 不适合快速上手 |

---

## 第六章：技能使用方法

### 6.1 自动触发(推荐)

AI 会根据对话上下文自动选择合适的技能。只需自然地描述你的需求:

```
"帮我审查一下这段代码"
→ AI 自动调用 code-review 技能

"生成一个 REST API 端点"
→ AI 自动调用 api-generator 技能
12345
```

### 6.2 手动调用

使用斜杠命令显式调用技能:

```
/code-review
/api-generator
/my-skill
123
```

**在 Agent 聊天中**:

1. 输入 `/` 会显示可用技能列表
2. 选择或继续输入技能名称
3. 按回车确认

### 6.3 Composer 模式

按 `Cmd + I` (Mac) 或 `Ctrl + I` (Windows/Linux) 打开 Composer:

1. 描述你想完成的任务
2. AI 会自动选择并应用相关技能
3. 可以在多文件间协调工作

### 6.4 查看已安装的技能

**方法 1: 通过设置界面**

- 打开 Settings → Rules
- 查看 “Agent Decides” 部分

**方法 2: 通过 AGENTS.md**

- 打开项目根目录的 `AGENTS.md` 文件
- 查看所有已注册的技能列表

---

## 第七章：常见问题解答

### 7.1 技能不显示或不工作?

**检查清单**:

1. ✅ 确认文件名是 `SKILL.md` (全大写)
2. ✅ 确认路径正确:
	```
	项目根目录/.cursor/skills/技能名/SKILL.md
	例如: my-website/.cursor/skills/code-review/SKILL.md
	123
	```
3. ✅ 确认 `.cursor` 文件夹在项目根目录下(与 src、package.json 同级)
4. ✅ 检查 YAML 前置元数据格式:
	```yaml
	---
	name: skill-name
	description: 描述
	---
	yaml1234
	```
5. ✅ 确认 `name` 字段与文件夹名匹配
6. ✅ 尝试重启 Cursor

### 7.2 openskills 安装失败?

**解决方案**:

```bash
# 检查 Node.js 版本(需要 >= 18)
node -v

# 清除 npm 缓存
npm cache clean --force

# Mac/Linux 权限问题
sudo npm install -g openskills

# Windows 权限问题
# 以管理员身份运行 PowerShell 或 CMD
bash1234567891011
```

**如果从 GitHub 安装技能失败**:

```bash
# 错误示例:
# Error: connect ETIMEDOUT
# Error: getaddrinfo ENOTFOUND github.com

# 原因: 无法访问 GitHub(国内网络限制)

# 解决方法 1: 使用代理
export https_proxy=http://127.0.0.1:7890  # Mac/Linux
set https_proxy=http://127.0.0.1:7890     # Windows CMD
$env:https_proxy="http://127.0.0.1:7890"  # Windows PowerShell

# 解决方法 2: 手动下载
# 1. 在浏览器访问 https://github.com/anthropics/skills
# 2. 点击 Code → Download ZIP
# 3. 解压到本地
# 4. 使用本地路径安装
openskills install ./anthropics-skills-main
bash1234567891011121314151617
```

### 7.3 如何更新已安装的技能?

**使用 openskills**:

```bash
# 更新所有技能
openskills update

# 更新特定技能
openskills update skill-name

# 重新安装
openskills install anthropics/skills
openskills sync
bash123456789
```

**手动更新**:

1. 删除 `.cursor/skills/` 下的旧技能文件夹
2. 重新安装或创建新版本

### 7.4 技能自动触发不准确?

**优化建议**:

**1\. 改进 description 字段**:

```yaml
# ❌ 不好
description: 代码审查工具

# ✅ 好
description: 对代码变更进行全面审查,关注最佳实践、安全性和性能。当用户请求代码审查、PR 审查或代码质量检查时使用。
yaml12345
```

**2\. 使用手动调用**:

```
/code-review  # 明确指定使用哪个技能
1
```

**3\. 添加 disable-model-invocation**:

```yaml
---
name: my-skill
description: 描述
disable-model-invocation: true  # 禁用自动触发,只能手动调用
---
yaml12345
```

### 7.5 全局技能和项目技能的优先级?

**Cursor 识别的技能目录** (按优先级从高到低):

1. `./.cursor/skills/` (项目级,Cursor 专用)
2. `~/.cursor/skills/` (全局,Cursor 专用)
3. `./.claude/skills/` (项目级,Claude Code 兼容)
4. `~/.claude/skills/` (全局,Claude Code 兼容)
5. `./.agent/skills/` (项目级,多代理通用)
6. `~/.agent/skills/` (全局,多代理通用)

**openskills 工具的安装路径**:

- 默认: `./.claude/skills/` (项目级)
- `--global`: `~/.claude/skills/` (全局)
- `--universal`: `./.agent/skills/` (多代理兼容)

**建议**:

- 通用技能放在全局目录
- 项目特定技能放在项目目录
- 同名技能会被项目级覆盖全局级

---

## 第八章：最佳实践

### 8.1 技能命名规范

```yaml
# ✅ 好的命名
name: code-review
name: api-generator
name: test-writer

# ❌ 不好的命名
name: CodeReview      # 不要用驼峰命名
name: code_review     # 不要用下划线
name: 代码审查         # 不要用中文
yaml123456789
```

### 8.2 编写清晰的 description

```yaml
# ❌ 太简短
description: 审查代码

# ✅ 详细且明确
description: 对代码变更进行系统化审查,检查代码质量、安全性、性能和最佳实践。适用于 PR 审查、代码重构前的检查、或代码质量评估。
yaml12345
```

### 8.3 结构化指令

使用清晰的章节结构:

```markdown
## 何时使用
明确触发条件

## 前置条件
列出必要的环境要求

## 执行步骤
详细的操作流程

## 输出格式
期望的结果格式

## 注意事项
特殊情况和边界条件
markdown1234567891011121314
```

### 8.4 提供示例

在技能中包含具体示例:

```markdown
## 示例

### 输入
用户请求: "生成一个用户登录的 API 端点"

### 输出
\\`\\`\\`typescript
// POST /api/auth/login
export async function loginHandler(req: Request, res: Response) {
  const { email, password } = req.body;
  // ... 实现细节
}
\\`\\`\\`
markdown12345678910111213
```

### 8.5 版本控制

为技能添加版本号和更新日志:

```yaml
---
name: my-skill
description: 描述
version: 1.2.0
---

# My Skill

## 更新日志

### v1.2.0 (2026-02-15)
- 新增: 支持 TypeScript 5.0
- 修复: 模板生成的路径问题

### v1.1.0 (2026-01-10)
- 新增: 错误处理示例
yaml12345678910111213141516
```

---

## 第九章：推荐资源

### 9.1 官方资源

| 资源 | 地址 | 说明 |
| --- | --- | --- |
| Anthropic Skills 仓库 | [github.com/anthropics/skills](https://github.com/anthropics/skills) | 官方技能库 |
| OpenSkills GitHub | [github.com/numman-ali/openskills](https://github.com/numman-ali/openskills) | 命令行工具 |
| Claude Skills 指南 | [design.dev/guides/claude-skills](https://design.dev/guides/claude-skills/) | 详细文档 |

### 9.2 社区资源

| 资源 | 地址 | 说明 |
| --- | --- | --- |
| Cursor 官方论坛 | [forum.cursor.com](https://forum.cursor.com/) | 讨论和问题解答 |
| Skills 目录 | [playbooks.com/skills](https://playbooks.com/skills) | 社区贡献的技能集合 |

---