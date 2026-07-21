---
name: joel-article-illustrations
description: 生成正文配图 skill。用户给链接或原文时先读文确认并用问答锁定 IP/风格/图上文字语言/张数；IP 含小黑/便签/句号/火柴人/小猫/恐龙；风格含纯白手绘/柔纸/笔记本笔/双色孔版/粗马克笔；支持中英双语标注、shot list、改图。默认小黑 + 纯白手绘 + 中文标注。
---

# Joel 正文配图（问答锁定变量 + IP/风格可变）

## 核心定位

为中文文章设计和生成 16:9 横版正文配图。目标不是做商业插画、PPT 信息图或可爱卡通，而是把文章里的关键判断、流程、结构、状态或隐喻，变成一张清爽、怪诞、有创意、可读但不说明书的手绘解释图。

角色人格固定：认真、冷幽默、不卖萌的荒诞工位员，必须参与核心动作。  
**外形（IP）和画风（style）可选。**

## 默认入口：交互问答

当用户提供**链接或原文**要配图，且没有说「直接生成/别问了」、也没一次写齐参数时：

1. 读文章  
2. 用简短结构**确认理解**（请用户纠正）  
3. **一次问清变量**：IP、风格、**图上文字语言**、模式、张数、其他约束  
4. **等用户回答**  
5. 复述锁定结果，再执行 shot list / 生图  

问答题面与规则见：`references/intake-qa.md`。  
**在用户回答变量之前：不要调用 image_gen，不要输出完整长 shot list。**

### 跳过问答

用户明确说「直接生成」「别问了」「用默认」或一句话已写齐关键变量时，可跳过问答；缺项用默认：

| 变量 | 默认 |
|------|------|
| IP | `xiaohei`（小黑） |
| style | `white-handdrawn`（纯白手绘） |
| label_lang | `zh`（**中文默认**；图上标注中文，未指定不得改英） |
| 模式 | `generate` |
| 张数 | `5` |

## 变体菜单

- IP：`references/ips/catalog.md`（`xiaohei` / `note` / `dot` / `stick` / `cat` / `dino`）
- 风格：`references/styles/catalog.md`（`white-handdrawn` / `soft-paper` / `notebook-pen` / `risograph-duo` / `bold-marker`）

### 加载规则（控制上下文）

变量锁定后**只读**：

1. `references/personality.md`
2. `references/ips/<ip-id>.md`
3. `references/styles/<style-id>.md`
4. 按需：`composition-patterns.md` / `prompt-template.md` / `qa-checklist.md`
5. `assets/examples/`：仅默认变体低频校准；其他 IP 不要照抄小黑外形

## 工作流（变量锁定之后）

### 1. 消化正文（问答阶段已做初读；执行前可再收紧锚点）

提炼认知锚点，不要平均配图。优先：核心判断、断点、闭环、分流、前后对比、路径、常见坑、状态变化。

### 2. 配图策略（shot list）

模式为 `shot-list` 或 `generate` 时输出 shot list。每张写清：

- 放在哪个段落后  
- 主题、核心意思、结构类型  
- **当前 IP 角色**在做什么  
- 建议元素与**标注词**（语言必须符合 `label_lang`）  

开头一行：`变体：IP=… · style=… · label_lang=… · 张数=…`  
张数以用户锁定为准；未锁定时默认 4–8 张思路，落地按锁定张数裁剪。

### 3. 单张生成

仅当模式为 `generate` / `generate-only`，且变量已锁定（或用户跳过问答）时，用 `image_gen` **每张单独**生成。

提示词：

- 骨架：`prompt-template.md`
- 填入当前风格 Visual DNA + 当前 IP 角色块 + **`label_lang` 标注语言**
- 16:9、留白、短标注、角色做核心动作
- 禁止 PPT/可爱/复杂架构/左上角类型标题
- 不复刻旧案例构图，按本文发明隐喻

### 4. 检查与迭代

按 `references/qa-checklist.md`。失败则重生成或局部编辑。

### 5. 保存交付

```text
assets/<article-slug>-illustrations/
01-topic-name.png
```

## 输出口径

- 问答阶段：短确认 + 选项表，不灌风格理论  
- 执行后：变体（含图上语言）、张数、用途、路径、哪张稳/可选  

不要长篇解释；让图自己说话。
