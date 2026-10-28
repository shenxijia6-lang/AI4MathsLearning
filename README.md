# AI4MathsLearning

简体中文 | [English](README.en.md)

> **AI 时代的数学学习加速工具。**

AI 已经能陪人读书、答疑、检查证明，但"能回答"不等于"能让人学得更快"。一个泛泛的回答可能正确却没有帮助：它跳过了你卡住的那一步，或者把结论塞给你，让你没机会自己想出来。

这个仓库提供一组可以直接装进 AI 助手（Claude、Codex 等）的工具：技能（skills）、提示词和工作流。每一个都针对数学学习中一个具体的瓶颈，比如看不懂定义的动机、读不通证明、不知道自己的证明对不对，并把 AI 的回答方式调整到真正能缩短学习时间的方向上。

每一项都可以单独安装、单独使用，并同时提供中文版和英文版。

## 目录

| 名称 | 类型 | 用途 |
| --- | --- | --- |
| [motivated-math](skills/motivated-math/SKILL.md)（[English](skills/motivated-math/SKILL.en.md)） | Skill | 讲解研究生及以上数学：还原定义的动机，让定理可猜、可信，讲清证明每一步是怎么想到的 |

更多内容会陆续加入。

---

## motivated-math

### 它解决什么瓶颈

教科书按"定义 → 定理 → 证明"写，这是**验证**的顺序。学数学的人卡住，往往是因为看不到**发现**的顺序：这个定义是被什么问题逼出来的？这个定理为什么应该是对的？证明里那个辅助函数是怎么想到的？看不到这些，就只能硬记，学得慢，也迁移不到新问题上。

### 它做什么

让 AI 按**发现顺序**讲数学：

```text
问题 → 朴素尝试 → 失败 / 反例 → 修正 → 概念与命题浮现 → 证明 → 回顾与压缩
```

目标是让每一步都显得是**被迫的、自然的**，理想状态是读到一半就能猜出下一步。

它有三个模块：

- **定义的考古**：这个定义要解决什么问题；最朴素的定义为什么不行；逐个去掉条件会坏掉什么；典型例子、边缘例子、近似非例；几种等价视角。
- **让定理变得"显然"**：先给出它为什么应该成立的启发式理由（最简单情形、维数计数、线性化、物理类比……），再做假设审计，说明它推广了什么、又是什么的特例。
- **证明的考古**：先讲战略再讲战术；按"想要 X → 自然尝试 Y → 在 Z 处卡住 → 于是引入 W"来叙述关键步骤；辅助对象是**推导出来的**，不是凭空宣布的；最后回顾，把证明压缩成能口述的一两句话。

几条硬规矩：

- 不许"从帽子里变兔子"。任何新对象都要交代来源；确实只能靠灵感的地方，要明说"这是真正的 idea"。
- 启发式论证标为【启发】，严格论证标为【证明】，两者不混。
- 不编造历史。"逻辑上可能这样被发现"的理性重构会标明。

两种交互模式：

- **讲解模式**（默认）：完整讲一个概念、定理或证明。
- **发现模式**：你说"让我自己想""别直接告诉我"时启用。AI 一次只给一级提示，从方向性问题到关键 idea，最后才给完整论证。你提出错误猜想时，它会给一个让猜想失败的例子，让你自己修正。

### 用起来是什么样

装好之后直接问就行，AI 会在合适的时候自动调用这个技能：

- "为什么正规子群要这样定义？"
- "紧性为什么要用开覆盖来定义，而不是序列紧？"
- "讲讲 Hahn–Banach 定理的证明是怎么想到的。"
- "别直接告诉我答案，带我自己想出 Cantor 定理的证明。"

也可以手动点名（见下方各平台的"调用方式"）。

---

## 安装

技能文件夹里有两个文件：

```text
skills/motivated-math/
├── SKILL.md       # 中文版（默认）
└── SKILL.en.md    # 英文版
```

AI 助手只读取名为 `SKILL.md` 的文件，所以下面的命令装的是中文版。想用英文版，见[本节末尾](#改用英文版)。

先把仓库拿到本地：

```bash
git clone https://github.com/shenxijia6-lang/AI4MathsLearning.git
cd AI4MathsLearning
```

### Claude

#### Claude 网页版 / 桌面版 / 手机 App（claude.ai）

1. 打开 **Settings → Capabilities**，确认 **Code execution and file creation**（新版设置里叫 **Create and edit files**）已开启。技能依赖这个功能。
2. 把技能文件夹打成 zip。**zip 的根目录必须是 `motivated-math/` 这个文件夹**，不能把 `SKILL.md` 直接放在 zip 根目录：

   ```bash
   cd skills
   zip -r motivated-math.zip motivated-math
   ```

   也可以直接在文件管理器里右键 `motivated-math` 文件夹压缩。
3. 打开 **Customize → Skills**，点 **+** → **Create skill** → **Upload a skill**，上传 `motivated-math.zip`。
4. 上传后确认它在技能列表里是开启状态。

> Team / Enterprise 计划：需要组织管理员在 **Organization settings → Plugins & skills** 的 Policy 页里开启 Skills 和代码执行。管理员也可以在那里直接把技能分发给全组织。

#### Claude Code

装到个人目录，所有项目都能用：

```bash
mkdir -p ~/.claude/skills
cp -r skills/motivated-math ~/.claude/skills/
```

或者只装到某个项目里（可以提交进那个项目的 git，团队共享）：

```bash
mkdir -p /path/to/your-project/.claude/skills
cp -r skills/motivated-math /path/to/your-project/.claude/skills/
```

**调用方式**：提问内容匹配时 Claude 会自动加载；也可以在消息开头输入 `/motivated-math` 手动调用。

**不需要重启**，Claude Code 会自动发现新技能。例外：如果 `~/.claude/skills` 这个目录是在当前会话开始之后才创建的，运行一次 `/reload-skills`。

### Codex

适用于 Codex CLI、IDE 插件和 Codex App。

装到个人目录，所有项目都能用：

```bash
mkdir -p ~/.agents/skills
cp -r skills/motivated-math ~/.agents/skills/
```

或者只装到某个项目里（放在项目根目录的 `.agents/skills/` 下）：

```bash
mkdir -p /path/to/your-project/.agents/skills
cp -r skills/motivated-math /path/to/your-project/.agents/skills/
```

> 旧版本 Codex 读取的是 `~/.codex/skills/`。如果装完后列表里看不到，先升级 Codex；不方便升级的话，把技能复制到 `~/.codex/skills/` 下。

也可以不手动复制，直接在 Codex 里让内置的安装器去装：

```text
$skill-installer 安装 https://github.com/shenxijia6-lang/AI4MathsLearning/tree/main/skills/motivated-math
```

**调用方式**：提问内容匹配时 Codex 会自动使用；也可以输入 `$motivated-math` 点名，或用 `/skills` 从列表里选。

Codex 会自动检测新技能；如果没出现，重启 Codex。

### 一行命令同时装到 Claude Code 和 Codex（可选）

如果装了 Node.js，可以用社区工具 [skills](https://github.com/vercel-labs/skills)（Vercel 出品，非 Anthropic / OpenAI 官方）一次装好：

```bash
npx skills add shenxijia6-lang/AI4MathsLearning --skill motivated-math -g -a claude-code -a codex
```

`-g` 表示装到个人目录（全局），去掉则装到当前项目；`-a` 指定要装给哪些工具。

### 改用英文版

两个版本内容相同，只是语言不同。按上面任一方式装好后，已安装的文件夹里本来就带着 `SKILL.en.md`，进到那个文件夹里用它覆盖 `SKILL.md` 即可：

```bash
cd ~/.claude/skills/motivated-math && cp SKILL.en.md SKILL.md   # Claude Code
cd ~/.agents/skills/motivated-math && cp SKILL.en.md SKILL.md   # Codex
```

如果安装器把技能装到了别的位置（比如 `~/.codex/skills/`），在那个文件夹里执行同样的 `cp SKILL.en.md SKILL.md`。

claude.ai 上传英文版时，先把它改名成 `SKILL.md` 再打包：

```bash
mkdir -p build/motivated-math
cp skills/motivated-math/SKILL.en.md build/motivated-math/SKILL.md
cd build && zip -r motivated-math.zip motivated-math
```

### 更新

```bash
cd AI4MathsLearning
git pull
```

然后重复上面对应平台的安装命令（或重新打 zip 上传）。

---

## 设计思想的来源

- G. Pólya,《How to Solve It》《Mathematics and Plausible Reasoning》
- I. Lakatos,《Proofs and Refutations》
- R. L. Morris, *Motivated proofs: what they are, why they matter and how to write them* (2019)
- T. Gowers 的 structured motivated proofs 项目
- W. Thurston, *On proof and progress in mathematics* (1994)
- T. Tao, *There's more to mathematics than rigour and proofs* 及其 career advice 系列
- R. Vakil,《The Rising Sea》前言

## 反馈与贡献

欢迎提 [Issue](https://github.com/shenxijia6-lang/AI4MathsLearning/issues) 或 PR，特别是：

- AI 用了这个技能之后**仍然**讲得像"定义—定理—证明"倾倒的例子（附上你问的问题和它的回答）；
- 你觉得讲得特别好的例子；
- 更好的"校准示例"（短小、能一眼看出动机是怎么逼出定义的那种）。
