# 生图提示词模板

每张图单独生成。根据正文内容替换变量，不要把多张图拼在一起。

先从当前变体文件取两块，再填入下方模板：

- `{VISUAL_DNA}` ← `references/styles/<style-id>.md` 里的英文 Visual DNA 块
- `{CHARACTER_BLOCK}` ← `references/ips/<ip-id>.md` 里的英文 prompt 块
- `{CHARACTER_NAME}` ← 当前 IP 显示名（小黑 / 便签 / 句号 / 火柴人 / 小猫 / 恐龙）
- `{LABEL_LANG}` ← `zh` / `en` / `bilingual`（图上标注语言，来自 intake）
- `{LABEL_LANG_RULE}` ← 按下表填入
- `{LABELS}` ← 已按 label_lang 写好的短标注

| label_lang | LABEL_LANG_RULE |
|------------|-----------------|
| `zh` | All handwritten labels must be short Chinese (2–8 characters each). No English labels unless a proper noun. |
| `en` | All handwritten labels must be short English (1–4 words each). No Chinese labels. |
| `bilingual` | Handwritten labels may pair tiny Chinese + English (e.g. 审核 / review). Keep each side very short; at most 5–8 label places total. Not a translation table. |

```text
Generate one standalone 16:9 horizontal article illustration.

Visual DNA:
{VISUAL_DNA}

Recurring IP character required:
{CHARACTER_BLOCK}

Label language:
{LABEL_LANG_RULE}

Theme:
{正文配图主题}

Structure type:
{结构类型：Workflow / 系统局部 / 前后对比 / 角色状态 / 概念隐喻 / 方法分层 / 地图路线 / 小漫画分镜}

Core idea:
{这张图要表达的核心意思}

Composition:
{具体画面：角色在哪里、正在做什么、主要物件是什么、信息如何流动}

Suggested elements:
{元素1} / {元素2} / {元素3} / {元素4}

Handwritten labels (must match label language {LABEL_LANG}):
{LABELS}

Color use:
Follow the current style file. Typically: black for main line art and {CHARACTER_NAME}; orange for main flow/path/arrows; red only for key warnings/problems/results; blue only for secondary notes or feedback/system state.

Constraints:
One image explains only one core structure. Keep the main subject around 40%-60% of the canvas. Preserve at least 35% blank white space. Use at most 5-8 short handwritten labels. Do not write a title in the top-left corner. Do not write the structure type on the image. Do not make it a formal diagram, course slide, or dense explainer. Do not copy prior examples or reuse known case compositions unless explicitly requested; invent a fresh visual metaphor for this specific article. It should be clear but not instructional, interesting but not childish, strange but clean. {CHARACTER_NAME} must do the core work, not stand as decoration.
```

## 图像编辑提示

去掉左上角标题：

```text
Edit the provided image. Remove only the handwritten title "{要删除的文字}" and its underline from the top-left corner. Fill that area with the same clean white background, matching the surrounding blank paper. Preserve everything else exactly: characters, labels, paths, line style, composition, aspect ratio, and image quality. Do not add any new text or objects.
```

增强角色参与感：

```text
Regenerate this illustration with the same core meaning and simple layout, but make {CHARACTER_NAME} more central to the conceptual action. {CHARACTER_NAME} should be doing the strange work that explains the idea, not standing beside the diagram. Keep the same IP appearance and current visual style. Keep it clean, sparse, hand-drawn, and not cute.
```
