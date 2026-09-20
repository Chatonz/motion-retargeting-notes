# 动作重定向调研：技术脉络与资源索引

> 来源：[飞书《重定向》](https://cwjgfm21di.feishu.cn/wiki/IbI1wVvmSiBde4kcyZrcHinOnpA)。整理日期：2026-09-20。
> 本文基于原文可读条目和 BeyondRetarget 配图整理。分类属于整理者的归纳；尚未逐一核验链接、阅读外部论文或复现代码。原文未提供的信息标为待补充，不据此判断性能与可用性。

## 1. 总体脉络

核心问题是：如何将人的动作迁移到结构不同的机器人，并使结果适合实际执行？

材料可以沿以下问题组织：

1. **动作处理与基础映射**：如何导入、编辑、配置和转换动作？
2. **形态适配**：如何处理人体与机器人以及不同机器人之间的结构差异？
3. **物理可行性与控制衔接**：映射后的动作如何满足动力学要求、方便跟踪执行？
4. **灵巧操作**：如何迁移手部动作，并保持接触与交互关系？
5. **视频到机器人**：能否直接从视频学习机器人动作？

这些是问题维度，不代表已核实的历史演进顺序。同一方法可以覆盖多个维度。

## 2. 人体与人形机器人重定向

### 2.1 工具与工程入口

| 条目 | 原文提供的信息 | 资源 |
| --- | --- | --- |
| human-humanoid-tools | 工具链接 | [中文 README](https://github.com/Roboparty/human-humanoid-tools/blob/main/README_cn.md) |
| HoloMotions | 仅列名称 | 待补充 |
| robot-retarget | 仅列名称 | 待补充 |
| scaleBFM retarget | 仅列名称 | 待补充 |
| gmr-motionlab | 标注为网页版动作编辑工具 | [GitHub](https://github.com/chaowei-code/gmr-motionlab) |
| soma_retargeter_autoconfig | 配置相关项目入口，功能待核实 | [GitHub](https://github.com/XinyuSong123/soma_retargeter_autoconfig) |
| Soma-retarget | 仅列名称 | 待补充 |

### 2.2 形态适配与跨机器人迁移

以下按名称及论文标题归类，具体方法边界有待阅读论文确认。

| 方法 | 文档中的标题或线索 | 资源 |
| --- | --- | --- |
| X-Morph | Human Motion Priors for Scalable Robot Learning Across Morphologies | [原文所附仓库](https://github.com/Maker-Rat/morph) |
| AdaMorph | Unified Motion Retargeting via Embodiment-Aware Adaptive Transformers | 待补充 |
| Human2Humanoid | Physics-Aware Cross-Morphology Motion Retargeting for Humanoid Robots；同时涉及物理约束 | 待补充 |
| IKMR | 附代码和论文链接；归类暂定 | [GitHub](https://github.com/Cybercal/IKMR/) · [论文](https://openreview.net/pdf?id=1fQ18mBmI7) |

### 2.3 物理可行性与控制衔接

这一组关注从动作映射到可执行动作的衔接，条目描述仅采用原文标题中的信息。

| 方法 | 文档中的研究主题 | 资源 |
| --- | --- | --- |
| DynaRetarget | Dynamically-Feasible Retargeting using Sampling-Based Trajectory Optimization：动力学可行性、采样式轨迹优化 | [论文](https://arxiv.org/pdf/2602.06827) |
| ReActor | Reinforcement Learning for Physics-Aware Motion Retargeting：强化学习、物理感知 | [论文](https://arxiv.org/pdf/2605.06593) |
| SPARK | Skeleton-Parameter Aligned Retargeting on Humanoid Robots with Kinodynamic Trajectory Optimization | 待补充 |
| NMR / Make Tracking Easy | Neural Motion Retargeting for Humanoid Whole-body Control：神经重定向与全身控制 | [GitHub](https://github.com/NJU3DV-HumanoidGroup/MakeTrackingEasy) |
| PHUMA | 原文仅列名称，具体定位待确认 | 待补充 |

原文注明 NMR 已开源到 Hugging Face，但未给出对应链接；实际开放内容有待核验。

## 3. 灵巧手与接触交互

### 3.1 手部模型与重定向项目

| 项目 | 原文提供的信息 | 资源 |
| --- | --- | --- |
| revo2_description | 标注为“官方强脑2代” | [GitHub](https://github.com/BrainCoTech/revo2_description) |
| brainco-retargeting | 灵巧手重定向相关仓库 | [GitHub](https://github.com/ronan-lebas/brainco-retargeting/tree/master) |
| wuji-retargeting | 灵巧手重定向相关仓库 | [GitHub](https://github.com/wuji-technology/wuji-retargeting) |
| AnyDexRetarget | 灵巧手重定向相关仓库 | [GitHub](https://github.com/qqsq12321/AnyDexRetarget) |

### 3.2 研究方法

- **Smooth Operator: A Real-Time Sampling-Based Algorithm for Kinematic Hand Retargeting**：标题强调实时、采样式、运动学手部重定向。原文单独列为章节，尚无论文或代码链接。
- **TopoRetarget: Interaction-Preserving Retargeting for Dexterous Manipulation**：标题强调灵巧操作中的交互保持。原文放在人体部分，此处按主题归入灵巧操作。资源：[论文](https://arxiv.org/pdf/2606.16272)、[原文所附复现项目](https://github.com/Key-Zzs/TopoRetarget-Repro/blob/main/README.zh-CN.md)、[另一个所附仓库](https://github.com/0iui0/toporetarget)。仓库与论文作者的关系尚未核验。

## 4. UMR：待展开的独立线索

原文单独列出“UMR动作重定向”，附 [GitHub 仓库](https://github.com/hanyang9/UMR)。尚未提供方法描述、适用范围或评测结果，因此暂不强行归入具体技术路线。

## 5. BeyondRetarget：从单目视频学习机器人动作

完整标题：**BeyondRetarget: Learning Executable Humanoid Motions Directly from Monocular Video**。

资源：[项目页](https://bear-ty.github.io/Beyondretarget_page/) · [GitHub](https://github.com/bear-ty/BeyondRetarget)。

原文配图呈现两种路径：

- **传统两阶段路径**：视频 → 人体动作估计 → 各机器人的重定向过程。
- **BeyondRetarget 路径**：视频 → 共享运动特征 → 各机器人解码器。

架构图还展示了时序模块、接触预测和细化模块。这一部分将问题从“如何映射已有的人体动作”推进到“如何直接从视觉输入学习机器人动作”。图示和标题不能替代实验验证；执行效果及适用条件仍需查阅论文。

## 6. 后续对比框架

为了从资源清单形成可用于选型的调研，建议逐项补全以下维度：

| 维度 | 需要回答的问题 |
| --- | --- |
| 输入与输出 | 接收视频、人体姿态还是动作轨迹？输出关节轨迹还是其他表示？ |
| 适配范围 | 支持哪些机器人、手型与自由度？新增机器人需要多少配置或训练？ |
| 方法 | 使用逆运动学、优化、采样、神经网络或强化学习中的哪些组成部分？ |
| 约束 | 是否考虑关节限制、碰撞、接触、平衡及动力学？ |
| 时间特性 | 在线还是离线？延迟、吞吐量和硬件要求是什么？ |
| 验证 | 是否有仿真或真机实验？采用什么数据集、基线和指标？ |
| 开放程度 | 是否公开代码、权重、数据、配置和许可证？ |

## 7. 整理记录与边界

- 合并了原文重复出现的 DynaRetarget 和 PHUMA 条目。
- 将 TopoRetarget 按主题移到灵巧操作部分。
- 保留 UMR 的独立位置，避免在证据不足时推断其方法。
- 未将原页面的 AI 推荐问题当作正文。
- 未复制原文图片，仅概括已查看的 BeyondRetarget 配图。
- 尚未给出性能排名、部署推荐或开源可用性结论。
