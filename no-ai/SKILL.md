---
name: no-ai
description: 识别并去掉文字里的 AI 口癖套路，改写得像真人自然表达，保留原意和技术准确性。当用户要求去 AI 味、消除 AI 痕迹、no-ai、让文字更像人写、判断某段文字是否太 AI、或列举 AI 写作痕迹时使用。
---

# no-ai

AI 写的文字有一批高度重复的固定模式。这个技能先教怎么识别（下面八类清单），再教怎么改掉（工作流 + 改法）。

## 判断原则

- 单个模式偶尔出现不算 AI 味，人也会这么写。
- 密集出现 + 内容空洞 + 到处对称工整，才是典型 AI 味。
- 越是"信息量低但语气笃定、结构特别齐整"，越可疑。
- 来源是模型被训得追求礼貌、完整、面面俱到、正能量收尾，于是套话和排比过量。

## 常见口癖清单

### 一、标志性词汇

英文高频词（尤其 delve 几乎是招牌）：
delve, dive into / deep dive, leverage, harness, robust, seamless, streamline, empower, foster, elevate, unlock, navigate, unleash, boasts, nestled, realm, landscape, tapestry, testament, underscore, pivotal, crucial, vital, game-changer, cutting-edge, state-of-the-art, holistic, myriad, plethora。

中文营销/黑话词：
口径、赋能、抓手、闭环、生态、链路、飞轮、范式、颗粒度、心智、维度、沉浸式、一键、打造、助力、护航、深耕、精准、高效便捷、全方位、多维度。

### 二、开场套话

- EN：In today's fast-paced world… / In the ever-evolving landscape of… / In an era where…
- ZH：在当今……的时代 / 随着科技的飞速发展 / 在这个日新月异的时代 / 众所周知

正文还没开始，先来一句放之四海而皆准的宏大铺垫。

### 三、否定式重构 / 对偶

- EN：It's not just X, it's Y. / This isn't merely X—it's Y. / It's not about X; it's about Y.
- ZH：不仅仅是……更是…… / 不是……而是……

用一个假对立把一句普通陈述包装得很有张力。

### 四、过渡词与信号词堆叠

- EN：Furthermore, Moreover, Additionally, That said, Ultimately, It's worth noting that, It's important to note that, Here's the thing。
- ZH：值得注意的是 / 需要指出的是 / 总而言之 / 综上所述 / 总的来说 / 其实 / 事实上 / 某种程度上。

靠连接词硬撑逻辑感，很多可以整句删掉。

### 五、三词排比（rule of three）

- EN：clear, concise, and compelling / fast, reliable, and scalable。
- ZH：高效、便捷、智能 / 稳定、安全、可靠。

三个近义词并列，凑气势而非增加信息。

### 六、结构套路

- 强行 First / Second / Finally，或事事都用 1、2、3、4 罗列，哪怕本该是一段话。
- 每段或每小节末尾都补一句重述总结。
- 加粗关键词后跟冒号解释：`**关键点：** ……`。
- 冒号式标题：`概述：xxxx` / `Overview: xxx` / `深度解析：xxx`。
- Emoji 当小标题或句尾装饰：✨🚀🔥✅。
- 结尾一段升华 / 口号式总结。

### 七、标点

- 破折号滥用——像这样——到处往句子里插。
- 大量括号（用来补充）（还层层嵌套）打断阅读。

### 八、修辞与语气

- 反问句开场：Ever wondered…? / 你是否曾经……？
- 谄媚开场：Great question! / Certainly! / 太棒了！ / 这是一个非常好的问题。
- 收尾讨好：I hope this helps! / Feel free to ask! / 希望这对你有帮助！ / 如有疑问随时问我。
- 空泛权威：Studies show… / Experts agree… / 研究表明 / 专家指出（没有具体出处）。
- 过度对称的排比长句，一段里句式完全平行。
- whether you're X or Y… / when it comes to X…

### 九 术语
- 不要出现太多的工程化术语 phase_a run_xxx 代码模块名称
- 在学术论文写作的时候, 符合学术化的术语规范

## 去 AI 味工作流

1. 通读原文，对照上面八类标出 AI tell 的地方。
2. 逐条替换或删除，只改表达不改原意。
3. 再通读一遍，确认没有为了去 AI 味把话改得生硬、跳跃或残缺。

## 改法

- 套话开场直接删，第一句就进入正题。
- "不是 X 而是 Y" / "不仅仅是……更是……" → 直接陈述结论。
- 破折号 → 换成句号、逗号，或直接删。
- 括号补充 → 并进正文，或删掉次要的。
- 三词排比 → 只留最准确的一两个。
- buzzword（赋能、抓手、leverage、seamless 等）→ 换成具体的动词或名词。
- 删掉每段末尾多余的重述总结。
- `**关键词：** 解释` → 改回正常句子。
- 冒号式标题 `概述：xxx` → 改成正常短语。
- 删谄媚开场（"这是个好问题"）和讨好结尾（"希望对你有帮助"）。
- 强行的 1234 罗列 → 改成连贯段落。

## 不要矫枉过正

- 破折号、括号、列表本身没问题，只有滥用或内容空洞时才改。真正的操作步骤、并列清单、代码，该用列表就用列表。
- 别为了"像人"故意写错字、断句破碎、逻辑跳跃。
- 保留专业术语和数字精度，技术含义不能改。
- 保持原文的语言和大致语气：中文改后还是中文，正式的保持正式。
- 目标是自然清楚，不是刻意口语或刻意简陋。

