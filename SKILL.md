# handbook-writing｜AI 课程实操手册制造机

> **一条龙把任何"实操技能"做成一门标准课程**：手册 + 物料包 + 讲师卡 + 发布。
> 给任何 AI Agent（Claude Code / WorkBuddy / Cursor / Codex CLI / OpenClaw…）装上这份 SKILL.md，它就能按同一套质量标准，帮你写出一本"初中文化能看懂、复制即用、每章留钩"的实操手册。

---

## 这是什么

你只要把**课程方案（哪怕只是一段口述录音转的文字）**丢给 Agent，说"用 handbook-writing 出手册"，它就会按下面的流水线交付：

```
你的课程方案（口述/md/docx 都行）
        ↓
┌─────────────────────────────────────────┐
│  ① 创作线（8 步）                        │
│  读方案定位 → 设计数据闭环 → 写三段标签指令 │
│  → 物料包（双 zip）→ 主手册 → 三层钩子     │
│  → 课后练习 → 讲师卡 + 通读校对            │
├─────────────────────────────────────────┤
│  ② 发布线（可选）                         │
│  md → Notion 原生排版 + 附件置顶           │
└─────────────────────────────────────────┘
        ↓
<课程名>/
├── 第N节课手册｜<钩子标题>.md     ← 纯学员版主手册
├── 讲师练习卡｜第N节.md           ← 内部资料（节奏表/保命提醒/暗号SOP）
├── 物料包/…-Win版.zip            ← Windows 自带解压不乱码（GBK 文件名）
├── 物料包/…-Mac版.zip            ← Mac/Linux 正常（UTF-8 文件名）
└── （可选）Notion 课程页
```

## 五分钟上手

### 第 1 步：把 skill 装进你的 Agent

不同 Agent 的 skills 目录位置不同，任选一条执行：

```bash
# 通用做法：克隆到本地
git clone https://github.com/chenlongdei12-dev/handbook-writing.git

# Claude Code / Codex CLI / OpenClaw（项目级）
cp -r handbook-writing/* .claude/skills/handbook-writing/

# Claude Code（用户级，所有项目可用）
cp -r handbook-writing/* ~/.claude/skills/handbook-writing/

# WorkBuddy
cp -r handbook-writing/* ~/.workbuddy/skills/handbook-writing/

# Cursor / 其他 Agent：放进你所用 Agent 的 skills/commands 目录即可，
# 核心是保证 SKILL.md 与 references/、scripts/ 三个部分在一起。
```

> 没有 git？在本仓库页面点 **Code → Download ZIP**，解压后同样复制。Windows 用户用资源管理器复制即可，不需要命令行。

### 第 2 步：扫一眼真实成品（强烈建议）

打开 `examples/` 里的两份手册（Word 课 + Excel 课，真实交付版），对照 `examples/README.md` 的"看点对照表"——什么是三段标签指令、什么是钩子、讲师卡和学员手册怎么分工，一眼看懂。

### 第 3 步：对 Agent 说一句话

```
用 handbook-writing 这个 skill，帮我把这份课程方案做成实操手册。
[粘贴方案 / 指明文件路径 / 直接口述需求]
```

Agent 会先问你四个决策问题（课程结构/工具主线/学员批次/发布平台），答完就开工。

### 第 4 步：验收产出

拿到交付物后按这个清单验收（Agent 自己也会跑一遍，你可以复核）：

- [ ] 手册是**纯学员版**（无节奏表/保命提醒/讲师话术——那些在讲师卡里）
- [ ] 每条指令是**三段标签**：`【1.读哪些材料】【2.做什么&输出什么格式】【3.绝对不能破的规矩】`
- [ ] 物料是 **docx/xlsx/txt**（绝无 md 学员物料），Win/Mac 双 zip
- [ ] 手册里**没有编造数字**：耗时要么讲师实测、要么留 `____`
- [ ] 每章末尾留钩，附录 A 有全部指令速查

## 文件结构

```
handbook-writing/
├── SKILL.md                      ← 总路由：意图识别 + 两条子流程 + 铁律
├── examples/                     ← 两套真实交付成品（Word课 + Excel课，含讲师卡）
│   └── README.md                 ← 先看这里：范例看点 × skill 概念对照表
├── references/
│   ├── handbook-writing.md       ← 创作线：八步流程 + 30 条实战踩坑清单
│   ├── handbook-template.md      ← 13 章写作模板（系列课骨架；单节课弹性取用）
│   └── notion-publishing.md      ← 发布线：Notion 推送流程 + 排版规范 + 排错对照
└── scripts/
    └── pack_materials.py         ← Win/Mac 双 zip 打包器（内置双版本校验）
```

## 核心方法论（为什么按这套来）

- **结果先行**：开篇先亮成品，学员看到结果再学步骤
- **指令三段标签**：给材料/给格式/给边界——第 3 段"规矩"是防 AI 编数的防线
- **数据闭环**：物料之间数字互锁（会议记录说的数 = 数据表里的数），乱数据用脚本生成并程序化校验
- **绝不编数**：课堂引用的耗时/成绩一律真实记录或留空，学员手里有真数，编了就穿帮
- **快慢班兜底**：01 原材料堆自足（没素材也能跑全流程）+ 02 预置标准产物（跟不上的直接取用）
- **三层钩子**：开场钩（成品对比）→ 认知冲突钩（裸指令翻车 vs 规矩版）→ 行动钩（选择题式暗号）
- **纯学员版 + 讲师卡分离**：手册给学员看，节奏表/保命提醒/暗号 SOP 归内部卡

30 条踩坑清单都在 `references/handbook-writing.md`，全部来自真实课程迭代——写手册遇到怪问题，先查它。

## 环境要求

- 任何能跑 Markdown 技能文件的 AI Agent（Claude Code、WorkBuddy、Cursor、Codex CLI、OpenClaw 等）
- Python 3.8+（仅打包物料时用到，标准库即可，无需 pip 安装）
- 发布线需要 Notion MCP 连接器（不发 Notion 可完全不用）

## License

MIT
