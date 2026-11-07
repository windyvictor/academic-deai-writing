# 证据与政策：AI 文本特征、检测可靠性、披露要求

本文件汇总改写规则的外部依据，核对日期 **2026-11-07**。按证据强度分档：**一手实证**为同行评议论文或语料研究，**官方文件**为机构发布的规范与政策，**二手转引**为综述、媒体报道或政府网站转载，**项目内实测**为 `lieflat-less-ai-tone` 的对照语料研究（非同行评议）。引用数字只在其研究设置内成立，不外推到所有检测器、所有语言或所有年份。

## 一、AI 写作的语言特征

| 来源 | 强度 | 结论 |
|---|---|---|
| Kobak D, González-Márquez R, Horvát EÁ, Lause J. *Delving into LLM-assisted writing in biomedical publications through excess vocabulary*, **Science Advances** 2025, 11(27): eadt3813, DOI [10.1126/sciadv.adt3813](https://doi.org/10.1126/sciadv.adt3813), [PMID 40601754](https://pubmed.ncbi.nlm.nih.gov/40601754/) | 一手实证 | 分析 2010–2024 年逾 1500 万篇 PubMed 摘要，发现若干风格词在 2023–2024 年突增；据此估计 2024 年至少 **13.5%** 的摘要经过 LLM 处理（**下界估计**，部分子语料达 40%）。测量的是词频变化，不是单篇作者身份 |
| Matsui K. *Delving Into PubMed Records: How AI-Influenced Vocabulary has Transformed Medical Writing since ChatGPT*, **Perspectives on Medical Education** 2025, DOI [10.5334/pme.1929](https://doi.org/10.5334/pme.1929), [PMID 41356414](https://pubmed.ncbi.nlm.nih.gov/41356414/) / [PMC12679996](https://pmc.ncbi.nlm.nih.gov/articles/PMC12679996/) | 一手实证 | 汇总 15 项研究的 135 个疑似 AI 影响词，以 84 个常用学术短语作对照；2024 年 103 个词显著上升，`delve / underscore / primarily / meticulous / boast` 最明显。但上升趋势**早于 ChatGPT 发布的 2020 年已开始**，2023–2024 才加速，提示 LLM 放大既有语言趋势而非凭空造词 |
| Desaire M 等，2023，用 20 个文体特征区分人类科学家与 ChatGPT 撰写的学术引言，[PMC10328544](https://pmc.ncbi.nlm.nih.gov/articles/PMC10328544/) | 一手实证 | 20 个特征中 18 个在**人类科学家**文本中更多：更长的段落、更大的句长变化、问号／破折号／括号／分号／冒号、`however / but / although / because / this`、数字、专有名词与缩略词。ChatGPT 更多用单引号和 `others / researchers` 这类泛化指称。作者自述测试集小（180 篇、约 1200 段）、贡献是「方法而非通用模型」，且 20 个特征可被少量定向编辑规避 |
| Weber-Wulff D 等, *Testing of detection tools for AI-generated text*, **International Journal for Educational Integrity** 2023 | 二手转引 | 评测的十余款检测工具准确率均低于 80%；机器翻译或改写后的 AI 文本检出率大幅下降。用于说明「改写会破坏检测信号」，不用于评价 2026 年产品 |
| `lieflat-less-ai-tone`（CC BY-NC 4.0，作者 shiujan）[RESEARCH.md](https://github.com/larashero3-dotcom/lieflat-less-ai-tone) | 项目内实测 | 629 篇中文对照 + 270 对同题同事实配对复测。翻案腔、结论提示冒号、相邻句同构、术语漂移等两轮同向；序数词小标题、空转句引列表、「这意味着」复述、句长参差等**方向反转或无差异**。已证伪清单见 `false-positive-guard.md` |

**推论**：词频上升是群体统计现象，不能当作单篇判据。按禁用词表删词、按「AI 爱用某个词」改写句子，既没有单篇证据，也会误伤正常学术表达。这组研究同时说明，模型迭代与写作者主动回避会持续改变词频，任何固定词表都有保质期。

**独立互证**：Desaire 的英文学术语料研究与 `lieflat-less-ai-tone` 的中文配对复测在不同语言、不同语料上得到同向结论——问句、破折号／分号、句长参差、精确数字、转折让步词都是**人类作者用得更多**。删这些写法不是「去 AI 味」，是在抹掉研究者本来的写法。这是把「防误改」独立成规则的实证依据，见 `false-positive-guard.md`。

## 二、检测器为什么不能当验收指标

| 来源 | 强度 | 结论 |
|---|---|---|
| Liang W 等, *GPT detectors are biased against non-native English writers*, **Patterns** 2023, DOI [10.1016/j.patter.2023.100779](https://doi.org/10.1016/j.patter.2023.100779), [arXiv:2304.02819](https://arxiv.org/abs/2304.02819) | 一手实证 | 7 个检测器对 91 篇非母语者 TOEFL 作文平均误判 **61.3%**，19.8% 被全部 7 个判为 AI，97.8% 被至少一个判为 AI；母语八年级作文组基本判对。用 ChatGPT 把同一批作文改写成「更 sophisticated」后误判大幅下降，说明检测器抓的是文风而非作者身份 |
| OpenAI, [*New AI classifier for indicating AI-written text*](https://openai.com/index/new-ai-classifier-for-indicating-ai-written-text/), 2023-01-31 | 官方文件 | 自报英文挑战集真阳性 **26%**、人类文本误判 **9%**；明确「not fully reliable」「should not be used as a primary decision-making tool」，并列出短文本（<1000 字符）、非英语、代码、编辑过的 AI 文本等限制。**2023-07-20 因准确率低下线** |
| Sadasivan VS, Kumar A, Balasubramanian S, Wang W, Feizi S. [*Can AI-Generated Text be Reliably Detected?*](https://arxiv.org/abs/2303.11156), 2023 提交，2025 年 v4，发表于 TMLR | 一手实证 | 递归改写攻击可显著降低多种检测方案（水印、神经分类器、零样本、检索式）的检出率，且文本质量只轻微下降；给出最优检测器 AUROC 与人机文本分布总变差距离的理论联系——两者分布越接近，检测越难 |
| ACRL/ALA, [*AI Text Detection Tools*](https://acrl.ala.org/IS/wp-content/uploads/fall-25-tips-and-trends.pdf), 2025 秋 | 二手转引（学术图书馆协会综述） | 汇总多项独立评测的误报与漏报；Vanderbilt、Michigan State、Waterloo 等校关闭 Turnitin AI 检测；建议把检测结果作为沟通性、公平评估过程的一个环节，而非单独依据 |
| 北京市人民政府网转载《半月谈》调查 [*查了个寂寞？被「AI 查重」困住的大学生*](https://www.beijing.gov.cn/fuwu/bmfw/sy/jrts/202607/t20260721_4774560.html)，2026-07-21；[南都快评](https://news.qq.com/rain/a/20260723A00F6G00)，2026-07-23 | 二手转引（媒体调查与评论） | 同一篇论文跨平台检测结果可从 30% 到 90%；《荷塘月色》被测出 62.88%、《滕王阁序》100% AI 疑似度；有平台同时售卖「降 AIGC」服务。专家意见：检测结果**不能直接作为认定学术不端的唯一依据**，仅凭报告不经学术委员会复核、不给申辩机会即作学位处置涉嫌程序违法 |

**推论**：分数是线索，不是结论。误报在非母语写作、公式化学术体裁、短文本、人写后 AI 润色的混合稿件中更集中；中文作者写英文论文尤其容易落入这一类。即使误报率很低，大规模评审中仍会产生大量错误指控。检测分数下降与论文质量提升没有因果关系。

> **注意**：2023 年的准确率数字不能直接用来评价 2026 年的产品；商业检测器在未经编辑的 AI 文本上已有明显改进，但**混合人机写作**仍是各评测里最弱的场景。本文件不主张「检测器一律无效」，只主张其分数不构成改写完成条件。

## 三、官方政策与披露要求

| 来源 | 强度 | 要点 |
|---|---|---|
| ICMJE Recommendations, [V. Use of Artificial Intelligence in Publishing](https://www.icmje.org/recommendations/browse/artificial-intelligence) | 官方文件 | AI 不得列为作者或被引为作者；人类须核对 AI 辅助生成内容的准确性、引用与是否抄袭；投稿、编辑、评审各阶段须透明披露所用工具及用途；编辑、审稿人不得在无法保证保密性时把稿件上传 AI 系统；期刊应制定并公开政策 |
| COPE Council, [*Authorship and AI tools*](https://publicationethics.org/guidance/cope-position/authorship-and-ai-tools), 2024, DOI [10.24318/cCVRZBms](https://doi.org/10.24318/cCVRZBms) | 官方文件 | AI 工具不满足作者资格（无法承担责任、无法声明利益冲突、无法管理版权许可）；在方法或同类章节披露使用了哪个工具、如何使用；作者对手稿全部内容负责，包括 AI 生成部分 |
| WAME, [*Chatbots, Generative AI, and Scholarly Manuscripts*](https://wame.org/page3.php?id=106), 2023-05-31 | 官方文件 | AI 不能作为作者；要求披露所用工具、版本、提示与使用时间；作者核实 AI 生成内容的准确性与引文；不得把审稿材料上传到未经许可的平台 |
| 中国科学院科研道德委员会, [*关于在科研活动中规范使用人工智能技术的诚信提醒*](https://www.cas.cn/sygz/202409/t20240910_5031186.shtml), 2024-09-10 | 官方文件 | 共八条。**提醒二**：申报材料使用 AI 生成内容须对内容负责并全面如实声明。**提醒五**：可用 AI 辅助整理已有理论、材料与方法，可做语言润色、翻译、规范化检查；反对把 AI 生成内容作为核心创新成果，反对生成整篇成果及参考文献。**提醒七**：须在注释、致谢、参考文献或附录声明工具名称、版本、日期及使用过程 |
| Springer Nature / Nature Portfolio, [*Artificial Intelligence (AI) editorial policies*](https://www.nature.com/natbiomedeng/editorial-policies/ai) 与 [*Guidance for researchers on use of AI in publishing*](https://www.springernature.com/de/group/guidance-for-researchers-on-use-of-ai-in-publishing/27826146) | 官方文件 | LLM 不满足作者资格，使用须记入 Methods；**「AI assisted copy editing」——对人工撰写文本做可读性、风格、语法、拼写、标点、语气的改进——无需声明**，但不含生成性编辑工作与自主内容创作；作者始终对终稿负责，并须确认改动反映其原始工作 |
| 中国科学技术信息研究所 × Elsevier × Springer Nature × Wiley, [*学术出版中 AIGC 使用边界指南*](https://www.istic.ac.cn/html/1/227/243/245/1701698014446298352.html)，2023-09-20 | 官方文件 | 语言润色、提高文本可读性、启发内容逻辑、提供句式可用；生成研究假设、直接撰写整篇论文、解释数据、得出科学结论不可用。须披露使用者、系统与版本号、时间日期、所用提示、由 AIGC 编写或共同编写的部分 |
| 科技部《负责任研究行为规范指引（2023）》，2023-12-21 | 二手转引（[人民网](https://finance.people.com.cn/BIG5/n1/2024/0118/c1004-40161643.html)／[中国经济网](https://www.ce.cn/cysc/tech/gd2012/202401/18/t20240118_38871243.shtml)转述） | 生成式 AI 生成的内容应明确标注并说明生成过程；不得使用 AIGC 直接生成申报材料。正式引用请核对规范原文 |
| 《中华人民共和国学位法》，2025-01-01 施行，第三十七条第一款；教育部《高等学校预防与处理学术不端行为办法》 | 二手转引（政府网站转述法条，非规范原文） | 规制对象是代写、剽窃、伪造等学术不端行为，经学位评定委员会决议处理；认定学术不端须由学术委员会组织调查。援引法条时以官方文本为准 |

**推论**：披露义务不因文字改写而消失。把「去 AI 味」做成隐瞒 AI 使用痕迹，与 ICMJE、COPE、WAME 和中科院提醒的透明原则直接冲突。本技能的定位是修复**已有稿件**的表达与论证，不代写整篇成果、不生成参考文献、不把改写后的表述包装成新的创新点。

**边界**：Springer Nature 把「对人工稿件的纯语言校对」与「生成性编辑、自主内容创作」分开，后者才要求声明。本技能的三条红线（不改科学含义、不补原文没有的信息、只围绕明确问题修订）正好落在前者。一旦改写演变成补写论证、生成新段落或重做创新点，就跨到需要披露的一侧。不同期刊与机构的分界线不完全一致，以投稿期刊和所在单位的规定为准；本技能不协助隐瞒 AI 使用。

## 四、实践经验与被证伪的「AI 特征」

- **为降分改坏文本**（媒体调查，见第二节末行）：把流畅句子改得磕磕巴巴、把学术表达掺入个人情绪，是「追分数」最直接的代价。这类改动同时违反本技能的信息守恒与结论强度要求。
- **禁用词表管不住 AI 味**（`lieflat-less-ai-tone` 项目经验 + 本节第一节语料研究）：语料里「赋能／闭环／抓手」等词在配对后无显著差异；真正影响阅读的是论证组织，不是某个词。
- **一次性喂十几条规则会让模型过度清理**（项目经验）：模型会连设问、序数词小标题、正常衔接一起删，改写后反而不像人写。这也是本技能把「防误改」独立成文件、把诊断设为可选分支的原因。
- **已证伪特征清单**：序数词小标题、「这意味着」复述、空转句引列表、概括替代、精确数字堆砌、句长或段长不参差、名词化与设问、被动句等，见 `false-positive-guard.md`。

## 五、对改写的可操作结论

1. 不承诺检测分数下降，不循环改写直到分数达标，不判断作者身份。验收看事实保留、论证连贯、表达自然。（依据：二、三）
2. 不按词表删词，不把词频上升当作单篇证据。（一）
3. 不为降低检出率制造句长参差、口语化、错别字或情绪化表达。（二、四）
4. 诊断报告区分「研究语料中的统计显著」与「本篇单次命中」；保留项给出可举证的理由。（一、二）
5. 术语一致、信息守恒优先于「像人写」。最小改动，改完逐项核对事实锚点。（四、项目内实测）
6. 已证伪特征常驻防线，命中不等于改。（四）
7. 改写不替代披露：按期刊与机构要求在方法、致谢或附录声明工具、版本、日期及用途。纯语言校对与生成性改写的分界按投稿期刊规定判断，不协助隐瞒 AI 使用。（三）
8. 不代写整篇成果，不生成参考文献，不把 AI 生成内容写成核心创新。（三）
9. 贡献是否成立、证据是否充分、创新点能否扩张，交作者与人审，模型不代判。（三，ICMJE 人类责任）

## 六、与常见误改冲突的注意事项

- 「删掉 AI 高频词就能降 AI 味」——词表无单篇判据，且删词会丢信息。（一）
- 「问句、破折号、分号、句长参差、精确数字都是 AI 痕迹」——英文学术语料与中文配对复测都发现人类作者用得更多；删这些写法是在抹掉研究者本来的写法。（一）
- 「句子长短要拉开才像人写」——配对复测中句长离散度无差异，机械参差化更糟。（四）
- 「段落衔接太顺就是 AI」——学术论证链本就要求紧扣；只修逻辑关系不成立的连接词，不制造跳转。（`false-positive-guard.md` 学术体裁例外）
- 「把编号小标题和『首先／其次』删掉更自然」——人类作者用得更多，且属版式与步骤要求。（四）
- 「检测报告说 AI 率高，说明这段要重写」——分数是线索；先看事实与论证有没有问题。（二）
- 「改写后就不必声明用了 AI」——披露义务与文本风格无关。（三）

## 七、局限

- 模型与检测器迭代快，本文件的准确率数字只描述各自发表时的评测设置；不对 2026 年产品作整体判断。
- 第二节部分结论来自综述与媒体转引，未逐篇核对原始论文（ACRL 综述、NIST 2024 试点、Weber-Wulff 等 14 工具评测）。引用时按「二手转引」对待。
- 中文政策部分除中科院原文外，法条内容来自政府网站转载，正式引用请核对官方文本。
- 第一节的语料研究以英文生物医学摘要为主，中文科研写作的可迁移部分是方法结论（词频不等于单篇证据），不是具体词表。
