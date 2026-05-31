# Personal Portfolio Website

一个面向 coding agent 的设计师个人简历与作品集网站 skill。通过分阶段对话采集内容，再按固定视觉规范生成可直接使用的单页作品集网站。核心 `SKILL.md` 可被 Codex、Cursor、Claude Code 等具备文件系统与 shell 访问能力的 coding agent 读取。

## What This Does

**Personal Portfolio Website** 帮助产品设计师、UX 设计师、UI 设计师和交互设计师，在没有完整前端经验的情况下，快速搭建一份专业、可投递的个人作品集网站。

与常见「先问配色、再问布局」的流程不同，本 skill 采用**内容与设计分离**的策略：

这里是一个通过本 skill 生成的网站演示视频：

<video src="demo.mp4" controls width="100%"></video>

- **内容采集**由 `references/content-prompt.md` 负责——通过自然对话逐步收集个人信息、项目、经历与联系方式。
- **视觉与布局**由 `references/design.md` 负责——暗色高级、强排版、专业克制，无需用户描述审美偏好。

Agent 会先帮你把话说清楚，再按统一规范把网站做出来。

### Key Features

- **内容与样式分离** — 采集逻辑和视觉规范各自独立，便于维护和迭代。
- **分阶段对话采集** — 不会一次性抛出冗长问卷；每个问题都带可复制占位符和示例。
- **固定设计系统** — 暗色背景、Kanit + Noto Sans SC 字体、紫粉橙发光强调，避免通用 AI 审美。
- **完整页面结构** — 导航、Resume、Project、Ability、Experience、Others、Contact 七大模块一次到位。
- **项目详情页支持** — 每个项目要求 16:9 封面（推荐 `1920×1080`）和 PDF，用于详情页展示。
- **生产级默认栈** — 新建项目默认 React + Vite + Tailwind；修改已有网站时优先沿用现有技术栈。
- **真实信息优先** — 可润色表达，但不编造关键履历事实。

## Installation

### Via Codex

将 skill 安装到 Codex skills 目录：

```bash
mkdir -p ~/.codex/skills/personal-portfolio-website
cp -R SKILL.md references agents ~/.codex/skills/personal-portfolio-website/
```

或直接克隆：

```bash
git clone <your-repo-url> ~/.codex/skills/personal-portfolio-website
```

安装后在 Codex 中使用 `$personal-portfolio-website` 引用本 skill，例如：

```text
使用 $personal-portfolio-website 帮我采集作品集内容，并生成一个设计师个人简历作品集网站。
```

### Via Cursor

将 skill 复制到 Cursor skills 目录，或在项目中直接引用本仓库：

```bash
mkdir -p ~/.cursor/skills/personal-portfolio-website
cp -R SKILL.md references agents ~/.cursor/skills/personal-portfolio-website/
```

在 Cursor Agent 对话中，指向本仓库或 `SKILL.md` 即可使用。

### Via Claude Code

手动安装到 Claude Code skills 目录：

```bash
mkdir -p ~/.claude/skills/personal-portfolio-website
cp -R SKILL.md references agents ~/.claude/skills/personal-portfolio-website/
```

或直接克隆：

```bash
git clone <your-repo-url> ~/.claude/skills/personal-portfolio-website
```

安装后在 Claude Code 中输入 `/personal-portfolio-website` 使用。

### Other Coding Agents

Codex、Cursor、Claude Code、Kimi Code、OpenCode、Gemini CLI 等本地 coding agent 均可使用本 skill。最简单的方式是把本仓库链接发给 agent，并说明要使用 Personal Portfolio Website skill：

```text
<your-repo-url>
```

如果 agent 能读取 GitHub 仓库或本地文件，应从 `SKILL.md` 开始，并按需加载以下支持文件：

- `references/content-prompt.md`
- `references/design.md`
- `agents/openai.yaml`

部分 agent 可自动安装到本地 skills 目录；若不能，也可在当前会话中直接遵循 `SKILL.md` 工作流。

## Usage

### 创建新的作品集网站

```text
使用 $personal-portfolio-website 帮我做一个 UX 设计师作品集网站
```

Claude Code 手动安装后，使用 `/personal-portfolio-website` 代替 `$personal-portfolio-website`。

Skill 会按以下流程工作：

1. **采集个人身份** — 姓名、岗位、城市、工作年限、个人照片、标签、slogan
2. **确认网站用途与受众** — 求职投递、作品集展示、个人品牌等
3. **收集项目资料** — 16:9 封面图、项目 PDF、类型与时间
4. **整理经历与技能** — 工作经历、教育经历、专业能力与软件技能
5. **确认联系方式** — 电话、微信（默认 `/wx.svg`）、邮箱
6. **读取 `design.md` 并生成网站** — 输出完整可运行代码
7. **启动本地服务并验收** — 检查桌面端/移动端布局与 16:9 封面

### 更新已有作品集网站

```text
使用 $personal-portfolio-website 帮我更新项目区和联系方式
```

修改已有网站时，skill 会：

1. 优先沿用当前项目技术栈与代码结构
2. 只更新用户提供的内容字段
3. 视觉改动严格遵循 `design.md`
4. 重新验证响应式布局与资源引用

### 更新 skill 文档本身

若需调整采集问题或视觉规范：

- 内容问题、占位符、示例 → 更新 `references/content-prompt.md`
- 风格、布局、组件、响应式规则 → 更新 `references/design.md`
- 若 skill 已安装到本地，同步更新对应目录下的 `references/` 文件

## Included Page Sections

本 skill 生成的是**单页纵向滚动**作品集，模块顺序固定：

| 模块 | 说明 |
| --- | --- |
| **Navigation** | 固定顶部导航，桌面端完整链接组，移动端精简布局 |
| **Resume / Hero** | 大标题身份区、个人照片、标签、slogan、基础信息卡片 |
| **Project** | 项目列表，16:9 封面，hover 展开，可跳转详情页 |
| **Ability** | 专业技能与软件技能，进度条展示 |
| **Experience** | 工作经历与教育经历，左右分栏（移动端单列） |
| **Others Project** | 其他设计作品、设计思考、推荐语等可选内容 |
| **Contact** | 电话、微信、邮箱，微信图标固定使用 `/wx.svg` |

### 设计系统概览

- **气质** — 暗色高级、强排版、专业克制、轻微未来感与发光感
- **主背景** — `#0C0C0C`
- **主文字** — `#D7E2EA`
- **强调色** — Magenta `#B600A8`、Violet `#7621B0`、Warm Orange `#BE4C00`
- **字体** — Kanit（英文标题）+ Noto Sans SC（中文正文）
- **默认技术栈** — React、TypeScript、Vite、Tailwind CSS、framer-motion、lucide-react

完整色彩、字体、组件、动效与响应式规则见 [`references/design.md`](references/design.md)。

## Content Collection Stages

内容采集由 [`references/content-prompt.md`](references/content-prompt.md) 定义，共分十个阶段：

| 阶段 | 内容 |
| --- | --- |
| 1 | 个人身份信息 |
| 2 | 网站用途与目标受众 |
| 3 | 项目信息、16:9 封面与 PDF |
| 4 | 工作经历 |
| 5 | 教育经历 |
| 6 | 专业技能与软件技能 |
| 7 | 联系方式 |
| 8 | 其他展示内容（可选） |
| 9 | 内容整理规则 |
| 10 | 生成网站 |

每个阶段的提问都包含**可复制占位符**和**至少一组示例**，方便用户直接填写替换。

## Architecture

本 skill 采用**渐进式披露**——`SKILL.md` 是工作流地图，支持文件按需加载：

| 文件 | 用途 | 加载时机 |
| --- | --- | --- |
| `SKILL.md` | 核心工作流与规则 | 始终（skill 调用时） |
| `references/content-prompt.md` | 分阶段内容采集、占位符与示例 | 阶段 1：内容采集 |
| `references/design.md` | 视觉规范、布局、组件、响应式 | 阶段 2：网站生成 |
| `agents/openai.yaml` | Agent 界面配置与默认 prompt | Agent 注册时 |

这种设计与 [Frontend Slides](https://github.com/zarazhangrui/frontend-slides) 一致：先给 agent 一张地图，再按当前任务只加载需要的文件。

## Philosophy

本 skill 基于以下信念：

1. **设计师不该被反复问配色。** 视觉方向应内置在规范里，对话只聚焦内容与事实。
2. **内容与样式必须分离。** 改文案不应牵动设计系统，改设计不应破坏采集流程。
3. **真实比华丽更重要。** 可以润色表达，但不能编造履历；作品集首先是可信的。
4. **首屏就是作品，不是广告。** 网站打开即可阅读，不做营销落地页式的空转引导。
5. **规范即产品。** 好的 skill 不是一次性 prompt，而是可维护、可迭代的工作流文档。

## Requirements

- 具备文件系统访问与 shell 命令执行能力的本地 coding agent
- 用户提供真实个人信息、项目封面（16:9）与项目 PDF
- 新建项目时：Node.js（用于 React + Vite 开发服务）
- 个人照片建议提供去背景 PNG；微信图标默认使用 `/wx.svg`

## Credits

Inspired by the agent-skill packaging approach of [Frontend Slides](https://github.com/zarazhangrui/frontend-slides) by [@zarazhangrui](https://github.com/zarazhangrui).
