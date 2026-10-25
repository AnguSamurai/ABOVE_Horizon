---
layout: default
title: "Horizon Summary: 2026-10-25 (ZH)"
date: 2026-10-25
lang: zh
---

> 从 26 条内容中筛选出 7 条重要资讯。

---

**科技新闻**
1. [Brotli 解码器高危漏洞波及 Python 与 Node.js 组件](#item-tech-news-1) ⭐️ 8.0/10
2. [美国媒体、影视与艺术岗位减少 20 万，AI 该负多少责任？](#item-tech-news-2) ⭐️ 7.0/10
3. [Cerebras 介绍万亿参数模型的晶圆级部署架构](#item-tech-news-3) ⭐️ 7.0/10
4. [Goose 编程语言公开，内存管理设计引发讨论](#item-tech-news-4) ⭐️ 7.0/10
5. [Dan Luu 主张软件构建者应更有野心](#item-tech-news-5) ⭐️ 7.0/10

**科技博客**
1. [别把大科技公司当人，也别当程序](#item-tech-blog-1) ⭐️ 6.0/10

**财经新闻**
1. [2025 年全国总人口减少 339 万 逼近 14 亿关口](#item-finance-news-1) ⭐️ 7.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [Brotli 解码器高危漏洞波及 Python 与 Node.js 组件](https://www.aikido.dev/blog/python-packages-vulnerable-node2shell-brotli-cve-2026-111497) ⭐️ 8.0/10

谷歌 Brotli 解码器的高危漏洞 CVE-2026-111497（CVSS 4.0 评分 9.2）影响 1.0.3 至 1.2.0 版本。远程未认证攻击者可发送特制压缩流，造成内存损坏、敏感数据泄露、进程崩溃，并可能执行任意代码；该漏洞已波及 Python 和 Node.js 的 HTTP 相关组件。按来源给出的修复版本，Python 的 Brotli 需升级至 1.2.1，brotlicffi 需升级至 1.2.1.0；Node.js 的修复版本为 22.23.4、24.22.1 或 26.12.1。该漏洞最初以 Node2Shell 名称披露，后被称为 HTTP2Shell，来源称 OpenAI 于今年 2 月发现该问题。

telegram · zaihuapd · 10月25日 02:42

**「漏洞根因」** 这一漏洞的根因是谷歌 Brotli 的 C 解码器缺陷，并非 Node.js 或 Python 本身；PyPI 上的 Brotli 和 brotlicffi 直接基于同一份 C 源码构建，因此也包含存在问题的解码器。除 Node.js 和 Python 外，使用 Brotli 解码的 Bun、Envoy 等组件同样受影响，并且已在某个 Node.js 构建上演示了代码执行。

**「影响与处置」** 对使用 Brotli 解码 HTTP 压缩内容的 Node.js 或 Python 服务而言，未修复版本会让未认证远程请求触发内存损坏，因此应尽快核对依赖版本，并升级到上述修复版本；若服务不直接解码 Brotli 内容，仍需确认底层 HTTP 组件是否调用了受影响解码器。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://opensourcemalware.com/blog/node2shell-affects-python">Python Packages Vulnerable to Node 2Shell Brotli CVE</a></li>
<li><a href="https://thehackernews.com/2026/10/brotli-decoder-flaw-behind-nodejs-rce.html">Brotli Decoder Flaw Behind Node . js RCE Also Affects Bun, Python ...</a></li>

</ul>
</details>

**标签**: `#security-vulnerability`, `#brotli`, `#CVE`, `#nodejs`, `#python`

---

<a id="item-tech-news-2"></a>
### [美国媒体、影视与艺术岗位减少 20 万，AI 该负多少责任？](https://www.apricitas.io/p/ai-and-the-fall-of-the-creative-class) ⭐️ 7.0/10

Apricitas 的一篇分析聚焦美国媒体、影视和艺术行业约 20 万个岗位的流失，追问其中有多少应归因于 AI。文章把自动化冲击与行业本身的成本削减、外包和商业模式压力放在一起讨论，而不是把岗位下降简单归为单一原因。对受影响从业者而言，关键争议在于如何区分 AI 带来的新增冲击与此前已经存在的行业收缩。

hackernews · gnabgib · 10月24日 23:11 · [社区讨论](https://news.ycombinator.com/item?id=50226419)

**「背景」** Apricitas 的 Joseph Politano 在 9 月下旬的分析中已把美国创意产业就业下滑拆到数字艺术各子行业，发现这些子行业普遍在减少岗位，而线下娱乐就业仍在稳步增长。Gizmodo 随后在 9 月 29 日的报道中概括称，基于劳工数据的分析显示，过去四年电影、电视、出版和平面设计等创意行业合计流失超过 20 万个岗位，其中影视岗位减少逾 10 万、出版业减少逾 7 万。Politano 的文章还提到，艺术与娱乐从业者中约 32% 使用生成式 AI，低于全行业 62% 的平均水平，这使把下滑主要归因于 AI 变得复杂。

**「社区讨论」** 评论者对 AI 的责任范围看法不一：有人认为商业插画等岗位的消失与 Stable Diffusion 兴起的时间点相近，另一些人则强调媒体岗位在图像模型出现前就因广告预算收缩和内容供给过剩而下降，因此更应观察趋势是否出现断点。还有评论把问题指向娱乐业追逐效率、制作外迁以及流媒体订阅价格上涨带来的需求压力。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.apricitas.io/p/ai-and-the-fall-of-the-creative-class">AI and the Fall? of the Creative Class - by Joseph Politano</a></li>
<li><a href="https://daily.dev/posts/america-has-lost-200k-of-jobs-in-media-film-and-the-arts-how-much-is-ai--atirjqule">America Has Lost 200k of Jobs in Media, Film and the Arts ...</a></li>
<li><a href="https://gizmodo.com/creative-jobs-have-plummeted-amid-the-ai-boom-2000818893">Creative Jobs Have Plummeted Amid the AI Boom - Gizmodo</a></li>

</ul>
</details>

**标签**: `#AI and jobs`, `#creative industries`, `#media industry`, `#economic analysis`, `#AI labor impact`

---

<a id="item-tech-news-3"></a>
### [Cerebras 介绍万亿参数模型的晶圆级部署架构](https://www.cerebras.ai/blog/how-we-deploy-trillion-parameter-frontier-models-on-cerebras) ⭐️ 7.0/10

Cerebras 发布博客，介绍在晶圆级系统上部署万亿参数前沿模型的推理架构，并称请求可在管线中连续流动，而不必等待同批其他请求完成。该文属于厂商自述，目前无法从所给材料独立复核其吞吐、延迟或精度表现。

hackernews · gmays · 10月25日 01:33 · [社区讨论](https://news.ycombinator.com/item?id=50227356)

**「背景」** Cerebras 的 WSE-3T 单块晶圆只有 44 GB 片上内存，而万亿参数模型仅权重就需要数 TB 存储，因此模型必须切分到多块晶圆上，并在晶圆之间传递激活值。Cerebras 在介绍这一部署方式时称，其面向万亿参数前沿模型的推理可达到每秒 1,000–2,000+ token。正因如此，跨晶圆互连以及 prefill 阶段的通信效率，成为衡量这套方案实际表现的关键前提。

**「影响」** 对评估 Cerebras 的团队来说，这篇部署说明不能替代针对目标模型的实测：选型前应确认所需模型是否在可访问目录中、服务采用何种量化精度，以及跨晶圆互连在 prefill 等阶段的延迟和吞吐。

**「社区讨论」** 评论者 keyle 称，Cerebras 实际可访问的模型有限，GPT OSS 120b 速度很快但“大多是错的”，并认为 OpenRouter 的选项更实用；tgtweak 则批评文章引用全精度基准、实际却采用 4 位量化。ismailmaj 质疑文章只说明了 decode 阶段的 RDMA 跨晶圆通信，未解释 prefill 如何同样保持快速，n\_u 也追问“不同于 GPU batch”的连续管线究竟是硬件限制还是软件脚手架缺失。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.cerebras.ai/blog/how-we-deploy-trillion-parameter-frontier-models-on-cerebras">How we deploy Trillion-parameter frontier models on Cerebras</a></li>
<li><a href="https://x.com/cerebras/article/2113315017714246003">How we deploy Trillion-parameter frontier models on Cerebras</a></li>

</ul>
</details>

**标签**: `#Cerebras`, `#AI hardware`, `#LLM inference`, `#model deployment`, `#wafer-scale computing`

---

<a id="item-tech-news-4"></a>
### [Goose 编程语言公开，内存管理设计引发讨论](https://aardappel.github.io/goose/) ⭐️ 7.0/10

开发者 Aardappel 公开了名为 Goose 的编程语言及 GitHub 仓库，配套教程用 \`u8\[\]\[&gt;..\]\` 动态数组和 \`push\(str\(...\)\)\` 示例来说明其内存分配方式，作者也在 Hacker News 讨论中确认身份并邀请提问。当前材料只有链接与评论，尚不能独立验证教程所称的分配优势；评论者已就示例是否真能避免逐字符串堆分配，以及如何表示任意数量且可随机增删的动态大小值提出质疑。

hackernews · bobbydigitales · 10月24日 19:06 · [社区讨论](https://news.ycombinator.com/item?id=50224100)

**「背景」** Goose 的项目仓库将其描述为一种语法接近 C 和 Rust 的内存安全系统语言，不需要堆分配器、垃圾回收器或生命周期标注，动态值由编译器通过数据栈管理。这一路线与更早的基于区域（region）的内存管理研究相呼应：ML Kit 等工作曾用静态分析推断内存分配和释放的位置，以类似栈的方式回收区域。

**「影响」** 对需要任意数量动态大小值的程序，Goose 当前展示的固定栈思路会迫使用户评估额外堆分配或间接层的成本；在教程示例的分配行为被核实前，潜在采用者不宜把“避免逐字符串分配”当作已确认保证。

**「社区讨论」** jcmoyer 指出教程首个内存分配示例不成立，因为示例中的字符串可走小字符串优化，从而避免逐字符串堆分配；malisper 追问固定数量栈如何表示任意数量、可随机增删的字符串哈希表，ebiederm 则把这一方向类比为 ML 的 region，并提到文献中曾有内存占用偏高的经验。作者 Aardappel 在评论中确认自己创建了该语言并给出仓库。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://github.com/aardappel/goose/tree/master/">GitHub - aardappel/goose: The Goose Programming Language</a></li>
<li><a href="https://elsolitario.org/en/2026/10/24/goose-language-no-heap-garbage-collector/">Goose Language: What It Is and How It Works Without a Heap</a></li>
<li><a href="https://www.academia.edu/48379445/Combining_region_inference_and_garbage_collection">(PDF) Combining region inference and garbage collection</a></li>

</ul>
</details>

**标签**: `#programming languages`, `#memory management`, `#language design`, `#static allocation`, `#Hacker News`

---

<a id="item-tech-news-5"></a>
### [Dan Luu 主张软件构建者应更有野心](https://danluu.com/ambitious/) ⭐️ 7.0/10

Dan Luu 在 danluu.com 发表观点文章，主张软件构建者应为所开发的软件追求更有野心的目标。文章没有发布新产品，也没有给出可量化的工程结果，而是引发了对 AI 工具、流程摩擦、软件质量与非标准开发方式的讨论。由于未提供原文正文，文中具体案例和论证细节无法核实。

hackernews · ltratt · 10月24日 21:47 · [社区讨论](https://news.ycombinator.com/item?id=50225695)

**「背景」** 这是 Dan Luu 的一篇观点随笔，而非产品发布或独立测量，因此文中的主张依赖作者论证与读者经验，没有版本号或基准数据可供核对。它接续了软件工程界一个反复出现的争论：从零自建编译器、游戏引擎这类基础设施，究竟是有价值的雄心，还是“永远交付不出东西”的典型症状——有评论者就以 Jonathan Blow 自写引擎、语言和编译器并最终发行游戏作为反例。

**「社区讨论」** 评论区对“野心”从何而来存在分歧：bob1029 认为团队协作成本和观念摩擦会抵消 AI 给单个开发者带来的编码收益，甚至称观察到团队退回全手工开发；jebarker 则以 Jonathan Blow 自建引擎、编程语言和编译器并最终交付游戏为例，反驳“造编译器的人从不交付”的说法。另有 fy20 以 Hitachi 热泵软件为例称大众软件质量仍然很差，thepoet 则表示 AI 让自己能完成过去没时间做的 Kobo 电子墨水 SDK 等项目。

**标签**: `#software engineering`, `#AI-assisted development`, `#software quality`, `#industry analysis`, `#developer productivity`

---

## 科技博客

<a id="item-tech-blog-1"></a>
### [别把大科技公司当人，也别当程序](https://seangoedecke.com/dont-anthropomorphize-big-tech-companies/) ⭐️ 6.0/10

rss · Sean Goedecke · 10月25日 00:00

**「背景」** 工程师常把雇主拟人化，觉得公司亏欠自己、憎恨自己，或与自己共享使命。Sean Goedecke 借 Bryan Cantrill 的“割草机”比喻提出，这种框架会妨碍工程师识别并规避大科技公司的风险。

**「方案」** 作者主张，大科技公司更像一辆危险但有用的汽车：它能成就你，也可能伤害你，却没有公平感，也不会尊重你的付出。公司不会因为你在某个项目上投入巨大就给予相称回报，高影响力工作往往难以预测；因此更有效的策略是寻找低投入、高回报的机会。有人辩称“公司恨我”只是“老板恨我”的简写，作者认为这仍然危险：高层管理者通常冷酷地按工具价值行事，被逼走的人可能只是被视为不可靠的工具，而经理往往只是暂时的。反过来，把公司当成计算机程序同样错误：手册、晋升指南和“首要任务”只是可读的上层结构，底下是不可读的人际依赖与激励网络，照字面执行会让人困惑。作者也承认经理确实可能记仇，自己的判断带有个人解释，但总体结论仍是应把公司当作机器来驾驶，而不是当作可讲道理的人。

**「启示」** 作者的结论是：不要期待公司像人一样讲公平或回报努力，而要学会驾驭这台由激励驱动的危险机器。这样既意味着可能无故受罚，也意味着有机会以较小努力获得不成比例的回报。

**标签**: `#organizational behavior`, `#big tech careers`, `#anthropomorphism`, `#engineering management`, `#career strategy`

---

## 财经新闻

<a id="item-finance-news-1"></a>
### [2025 年全国总人口减少 339 万 逼近 14 亿关口](https://weibo.com/1796087453/5357878513767954) ⭐️ 7.0/10

据荔枝新闻报道，2025 年末全国总人口为 140489 万人，比 2024 年末减少 339 万人，总人口面临跌破 14 亿。报道援引《中国统计年鉴 2026》数据称，全年出生 792 万人，出生率 5.63‰，自然增长率为-2.41‰。

telegram · zaihuapd · 10月25日 12:02

**「背景」** 人口减少的直接原因是死亡人数多于出生人数：国家统计局数据显示，2025 年死亡 1131 万人、出生 792 万人，自然增长率因此为-2.41‰。

**「影响」** 2025 年死亡人数（1131 万）已明显超过出生人数（792 万），人口总量的收缩将主要通过劳动力供给减少，以及养老金和医疗等公共与家庭支出上升，传导至企业和居民。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.globaltimes.cn/page/202608/1369306.shtml">China records 7.92 million births in 2025 as birth rate ...</a></li>
<li><a href="https://www.stats.gov.cn/english/PressRelease/202602/t20260228_1962661.html">STATISTICAL COMMUNIQUÉ OF THE PEOPLE&#x27;S REPUBLIC OF CHINA ON ...</a></li>
<li><a href="https://en.wikipedia.org/wiki/Demographics_of_China">Demographics of China - Wikipedia</a></li>

</ul>
</details>

**标签**: `#China demographics`, `#population decline`, `#birth rate`, `#regional divergence`, `#economic implications`

---