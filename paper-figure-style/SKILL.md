---
name: paper-figure-style
description: 生成顶会论文风格配图的 prompt 与规范，覆盖 CVPR / ICCV / ECCV / ICRA / IROS / CoRL / RSS。适用于撰写 teaser 首页图、方法总览图、pipeline 架构图、机器人硬件与实验设置图、VLA 具身管线图、结果对比图的图像生成 prompt，或为这些图制定配色、版式、字体、箭头规范。Use when generating prompts or style specs for publication-quality paper figures (teaser, method overview, pipeline, hardware/setup, VLA, comparison) for top CV/robotics conferences.
---

# 顶会论文配图风格 (CVPR / ICCV / ECCV / ICRA / IROS)

产出"可直接粘贴到图像生成模型"的配图 prompt，并保证风格符合顶会惯例。

## 工作流

1. 先确定这张图的**角色**（见下表），一张主图只讲一件事。
2. 选对应的**分类型模板**，填 `Goal / Components / Layout` 三段。
3. 把**通用风格块**整段粘到 prompt 末尾。
4. 出图后用**检查清单**过一遍再定稿。

输出给用户时，默认给"可直接粘贴的完整 prompt"，prompt 主体用英文（图像模型对英文更稳），中文留给说明。

## 配图角色表（先想清楚画哪一种）

| 角色 | 用途 | 关键元素 |
|------|------|----------|
| Teaser / 首页图 | 一眼说清问题与亮点 | 任务场景、系统输出、对比效果，少细节 |
| 方法 / 系统总览 | 论文门面，讲清方法怎么走 | 嵌套框、清晰模块边界、带标注的数据流 |
| 架构 / 管线 | 顺序处理流程 | 框 + 箭头，左到右或上到下 |
| 硬件 / 实验设置 | 可复现性（机器人系） | 真机照片标部件、通信拓扑、坐标系 |
| 结果对比 | baseline vs 我们的 | 并排面板、强调色突出"我们的" |
| 消融 | 各组件贡献 | 柱状图、高亮关键行 |

视觉系 (CVPR/ICCV/ECCV) 偏抽象概念化，teaser 常跨整页宽并在角落嵌"ours vs SOTA"迷你图；近年流行把真实 prompt/文本当图元 (text example-centric)。机器人系 (ICRA/IROS/CoRL/RSS) 偏具体模块化，首页图常画真机分步连拍 ①②③④，系统图/硬件图/实验设置图分开画；VLA 论文流行"语言指令→视觉→动作"三段式。

## 核心规范（精简）

- **版式**：单一主方向（推荐左到右），需要反馈加一条带标注的回路；对齐到隐形网格，框尺寸与间距一致，留白 ≥ 15%；嵌套框表达"包含"，主模块 5–7 个。
- **配色**：全图 ≤ 4 个主色，先用灰度能区分再上色。用对色盲友好的离散调色板（避免红绿对比），从 Okabe-Ito 取色池中为单图选 ≤ 4 色：黑 `#000000`、橙 `#E69F00`、天蓝 `#56B4E9`、青绿 `#009E73`、黄 `#F0E442`、蓝 `#0072B2`、朱红 `#D55E00`、紫红 `#CC79A7`。留一种强调色只给"我们的方法/新模块"，其余用中性灰蓝。配合线型/形状/纹理做冗余编码，定稿前用色盲模拟工具核验。
- **字体**：图内一律无衬线（Helvetica / Arial / Inter / IBM Plex Sans）且全图统一；最终尺寸下正文级图内字 ≥ 7–8 pt；面板编号用 `(a) (b) (c)`；只写短标签不写整句。
- **箭头**：实线=数据流，虚线=可选路径/反馈；每根箭头加短变换标签（如 `embedding`、`top-k`、`context`、`status`）。
- **导出**：矢量优先 (PDF/SVG)，位图素材（真机照片）≥ 300 dpi；按目标栏宽设计（CVPR/ECCV 双栏，跨栏大图用 `figure*`）。

## 通用风格块（粘到任意图像生成 prompt 末尾）

```text
Style: publication-quality figure for a top computer-vision / robotics conference
(CVPR / ICCV / ECCV / ICRA / IROS). Strictly flat 2D vector illustration (exception:
CNN/Transformer architecture diagrams may use isometric 3D blocks to show layer stacking),
no perspective, no photorealism. White background, generous whitespace (>15%), thin 1px
clean strokes, elements aligned to an invisible grid, consistent box sizes and spacing.
Restrained colorblind-safe palette, at most 4 colors (Okabe-Ito or Paul Tol), neutral
gray-blue for ordinary modules and ONE accent color reserved for the proposed / novel
module; redundant encoding via solid vs dashed lines, not color alone. Crisp sans-serif
typography (Helvetica / Arial), short phrase labels only, no full sentences inside the
figure. Solid arrows = data flow, dashed arrows = optional / feedback; put a short
transformation label on each arrow. Limit to 5-7 main components. No drop shadows, no
gradients, no decorative icons, no clutter. Legible at final print size; high resolution.
```

## 五段式填空模板

```text
Goal: <一句话说清这张图要让读者理解什么>

Components: <列出方框及其层级/包含关系；标出哪个是"我们的"新模块>

Layout: <主方向，如 left-to-right pipeline；谁在谁下面；反馈回路接到哪；
         箭头标签，如 "embedding" / "top-k" / "context" / "answer">

Style: <粘贴上面的"通用风格块">

Constraints: <长宽比，如 16:9 或单栏 4:3；双语或单语标签；图注文字；
              必须避免的元素>
```

## 分类型模板

方法 / 系统总览图：

```text
Goal: overview of the proposed method so a reader grasps the data flow before the text.
Components: input -> {modules as nested boxes} -> output; mark the novel module with the accent color.
Layout: left-to-right pipeline with one labeled feedback loop; short arrow labels for each transformation.
Style: <通用风格块>
Constraints: two-column width (16:9), self-contained caption "Figure 1. Overview of <method>.".
```

Teaser / 首页图 (FPF)：

```text
Goal: one-glance elevator pitch — the problem and our result, eye-catching, minimal detail.
Components: task scene / system output / before-vs-after comparison panels; optionally a small quantitative chart (mini bar/scatter plot) in the corner showing "ours vs SOTA" metrics.
Layout: large full-page-width banner; emphasize the result, hide implementation detail.
Style: <通用风格块>，可保留必要的真机/场景照片元素
Constraints: full text width, bold visual hierarchy, very few words.
```

机器人硬件 / 实验设置图：

```text
Goal: show the robot platform and the deployment setup for reproducibility.
Components: real robot photo with labeled parts (camera, lidar, onboard computer);
            separate communication/topology block (onboard <-> laptop <-> GPU server, ROS topics);
            optional coordinate frames.
Layout: photo on the left with callout labels; system/topology block on the right.
Style: clean callout lines, sans-serif labels, neutral palette; keep the photo, annotate flatly.
Constraints: single- or two-column; concise caption listing sensors and compute.
```

VLA / 具身智能管线图：

```text
Goal: show the vision-language-action pipeline for an embodied AI system.
Components: language instruction (text prompt overlaid on scene) -> vision encoder -> policy network -> action output; real robot photo sequence showing task execution steps ①②③④.
Layout: top row = pipeline (left-to-right), bottom row = real-world task frames with step annotations.
Style: <通用风格块>，真机照片保留，pipeline 部分用扁平矢量框
Constraints: emphasize end-to-end multimodal interaction; caption self-contained with task description.
```

结果对比图：

```text
Goal: show our method beats baselines on the same input.
Components: side-by-side panels, same scene per row; columns = {Input, Baseline A, Baseline B, Ours, GT}.
Layout: grid, identical crops; highlight "Ours" column header with the accent color; arrows/boxes on key regions.
Style: <通用风格块>
Constraints: aligned grid, consistent zoom, minimal labels; differences readable in grayscale.
```

## 定稿检查清单

- 主图只讲一件事，主模块 5–7 个。
- 单一主方向数据流，反馈回路有标注。
- 颜色 ≤ 4（从 Okabe-Ito 调色板选取），色盲友好，强调色只给"我们的"；用色盲模拟工具实测。
- 图内全无衬线、统一字体，只用短标签，最终尺寸下 ≥ 7–8 pt。
- 实线=数据流、虚线=可选/反馈，箭头带短变换标签。
- 对齐网格，留白 ≥ 15%，无阴影/渐变/多余边框与图标。
- 矢量导出，100% 缩放清晰；照片 ≥ 300 dpi。
- 图注自包含；面板用 `(a)(b)(c)`；术语与正文一致。

## 参考

- Marshall, Freitas & Jay (2025). An evidence-based guidance framework for neural network system diagrams. *PLOS ONE* 20(1):e0318800. 基于 120 张顶会神经网络系统图的循证研究。
- Okabe & Ito 色盲安全配色；Paul Tol、IBM Design、Wong 2011 (Nature Methods) 调色板。
- Crameri et al. (2024). Choosing Suitable Color Palettes for Accessible and Accurate Science Figures. *Current Protocols*.
- ICRA / IROS / CoRL / RSS 论文的系统总览图、真机硬件图与实验设置图惯例（实际论文观察）。
