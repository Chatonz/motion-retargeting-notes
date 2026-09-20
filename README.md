# 动作重定向调研：技术脉络与资源索引

> 来源：[飞书《重定向》](https://cwjgfm21di.feishu.cn/wiki/IbI1wVvmSiBde4kcyZrcHinOnpA)。整理日期：2026-09-20。
> 本文基于原文可读条目和 BeyondRetarget 配图整理，并于 2026-09-20 为缺少链接的条目补查论文、作者项目页和仓库。分类属于整理者的归纳；新增资源的匹配依据及歧义见第 8 节。未全面审读论文或复现代码，不能据此判断性能与部署可用性。

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

| 条目 | 定位与核验说明 | 资源 |
| --- | --- | --- |
| human-humanoid-tools | 工具链接 | [中文 README](https://github.com/Roboparty/human-humanoid-tools/blob/main/README_cn.md) |
| HoloMotions（疑指 HoloMotion） | 高概率匹配地平线 HoloMotion；其 HoloRetarget 模块处理动作重定向，保留原文拼写歧义 | [官方仓库](https://github.com/HorizonRobotics/HoloMotion) · [重定向文档](https://github.com/HorizonRobotics/HoloMotion/blob/master/docs/motion_retargeting.md) |
| robot-retarget | 找到同名 PyPI 包，但无法确认原文是否指它；包的源码链接仍是占位地址，暂不认定任何 GitHub 仓库为官方实现 | [同名候选包](https://pypi.org/project/robot-retarget/)；原始指代待确认 |
| scaleBFM retarget → ScaleRetarget | ScaleBFM 仓库中的重定向模块，将多种动捕格式转换为机器人轨迹 | [ScaleBFM 仓库](https://github.com/zengweishuai/ScaleBFM) · [ScaleRetarget 文档](https://github.com/zengweishuai/ScaleBFM/blob/main/ScaleRetarget/README.md) |
| gmr-motionlab | 标注为网页版动作编辑工具 | [GitHub](https://github.com/chaowei-code/gmr-motionlab) |
| soma_retargeter_autoconfig | 配置相关项目入口，功能待核实 | [GitHub](https://github.com/XinyuSong123/soma_retargeter_autoconfig) |
| Soma-retarget → SOMA Retargeter | NVIDIA 工具：SOMA 骨架 BVH → 人形机器人关节动画 CSV；输出为运动学动作 | [官方仓库与文档](https://github.com/NVIDIA/soma-retargeter) |

### 2.2 形态适配与跨机器人迁移

以下按名称及论文标题归类，具体方法边界有待阅读论文确认。

| 方法 | 文档中的标题或线索 | 资源 |
| --- | --- | --- |
| X-Morph | Human Motion Priors for Scalable Robot Learning Across Morphologies | [原文所附仓库](https://github.com/Maker-Rat/morph) |
| AdaMorph | Unified Motion Retargeting via Embodiment-Aware Adaptive Transformers | [论文](https://arxiv.org/abs/2601.07284)；本次未找到可确认的官方代码 |
| Human2Humanoid | Physics-Aware Cross-Morphology Motion Retargeting for Humanoid Robots；同时涉及物理约束 | [论文](https://arxiv.org/abs/2606.03476) · [作者项目页](https://huangtc233.github.io/human2humanoid_website/)；项目页代码状态为 Coming Soon |
| IKMR | 附代码和论文链接；归类暂定 | [GitHub](https://github.com/Cybercal/IKMR/) · [论文](https://openreview.net/pdf?id=1fQ18mBmI7) |

### 2.3 物理可行性与控制衔接

这一组关注从动作映射到可执行动作的衔接。条目描述来自原文标题或补查到的作者资源。

| 方法 | 文档中的研究主题 | 资源 |
| --- | --- | --- |
| DynaRetarget | Dynamically-Feasible Retargeting using Sampling-Based Trajectory Optimization：动力学可行性、采样式轨迹优化 | [论文](https://arxiv.org/pdf/2602.06827) |
| ReActor | Reinforcement Learning for Physics-Aware Motion Retargeting：强化学习、物理感知 | [论文](https://arxiv.org/pdf/2605.06593) |
| SPARK | Skeleton-Parameter Aligned Retargeting on Humanoid Robots with Kinodynamic Trajectory Optimization | [论文](https://arxiv.org/abs/2603.11480) · [第一作者主页（含演示入口）](https://hwang-warren.github.io/)；本次未找到可确认的官方代码 |
| NMR / Make Tracking Easy | Neural Motion Retargeting for Humanoid Whole-body Control：神经重定向与全身控制 | [GitHub](https://github.com/NJU3DV-HumanoidGroup/MakeTrackingEasy) |
| PHUMA / PhySINK | PHUMA 是人形运动数据集；其 PhySINK 流程负责物理约束重定向，需区分数据集与方法 | [论文](https://arxiv.org/abs/2510.26236) · [项目页](https://davian-robotics.github.io/PHUMA/) · [官方仓库](https://github.com/DAVIAN-Robotics/PHUMA) · [数据集](https://huggingface.co/datasets/DAVIAN-Robotics/PHUMA) |

NMR 的官方仓库明确给出 [Hugging Face 在线演示](https://huggingface.co/spaces/RayZhao/NMR) 和 [模型权重](https://huggingface.co/RayZhao/NMR) 链接，已补全。页面可访问不代表已完成推理运行验证。

## 3. 灵巧手与接触交互

### 3.1 手部模型与重定向项目

| 项目 | 原文提供的信息 | 资源 |
| --- | --- | --- |
| revo2_description | 标注为“官方强脑2代” | [GitHub](https://github.com/BrainCoTech/revo2_description) |
| brainco-retargeting | 灵巧手重定向相关仓库 | [GitHub](https://github.com/ronan-lebas/brainco-retargeting/tree/master) |
| wuji-retargeting | 灵巧手重定向相关仓库 | [GitHub](https://github.com/wuji-technology/wuji-retargeting) |
| AnyDexRetarget | 灵巧手重定向相关仓库 | [GitHub](https://github.com/qqsq12321/AnyDexRetarget) |

### 3.2 研究方法

- **Smooth Operator: A Real-Time Sampling-Based Algorithm for Kinematic Hand Retargeting**：提出 Sampling-Based Retargeter（SBR），面向低抖动的实时运动学手部重定向。资源：[论文](https://arxiv.org/abs/2607.07491) · [作者项目页](https://mimicrobotics.github.io/smooth-operator/) · [项目页所指官方代码 mimic_retargeter_lab](https://github.com/mimicrobotics/mimic_retargeter_lab)。代码仓库包含 `sampling_based` 及其他重定向实现。
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

## 8. 缺失资源补查记录

核验日期：**2026-09-20**。优先使用论文记录、作者项目页、官方仓库和作者发布的包信息。原文已有但未在本轮检查的链接，不视为已重新核验。

| 原始名称 | 匹配依据与结论 |
| --- | --- |
| HoloMotions | 未找到同拼写的明确机器人项目；[HoloMotion 官方 README](https://github.com/HorizonRobotics/HoloMotion) 明确包含 HoloRetarget，并链接专门的重定向文档。作为高概率候选补入，尚不能从原文独立确认作者本意。 |
| robot-retarget | [PyPI](https://pypi.org/project/robot-retarget/) 存在同名包，但其 Homepage/Source 指向 `github.com/yourusername/robot-retarget` 占位地址；搜索到的 [rfouyang 同名仓库](https://github.com/rfouyang/robot-retarget) 为空。仅记录候选包，保留待确认，不以相似项目替代。 |
| scaleBFM retarget | [ScaleRetarget README](https://github.com/zengweishuai/ScaleBFM/blob/main/ScaleRetarget/README.md) 明确位于 ScaleBFM 仓库，并说明动捕数据到机器人轨迹的转换流程。 |
| Soma-retarget | [NVIDIA 官方仓库](https://github.com/NVIDIA/soma-retargeter) 明确名称为 SOMA Retargeter，并描述 SOMA BVH 到机器人 CSV 的重定向功能。 |
| AdaMorph | [arXiv](https://arxiv.org/abs/2601.07284) 标题与原文完整一致；第一作者 Haoyu Zhang。未确认到官方代码不等于断言没有代码。 |
| Human2Humanoid | [arXiv](https://arxiv.org/abs/2606.03476) 标题完整一致，且直接链接作者项目页；该页明确标注 Code (Coming Soon)。 |
| SPARK | [arXiv](https://arxiv.org/abs/2603.11480) 标题完整一致，第一作者 Hanwen Wang 的主页也列出同一论文；本次未确认官方代码。 |
| PHUMA | [作者项目页](https://davian-robotics.github.io/PHUMA/) 直接链接论文、DAVIAN-Robotics 仓库及数据集。项目页/仓库使用 Physically Reliable，arXiv 条目使用 Physically-Grounded；以论文编号 2510.26236 和作者资源互链确认对应关系。 |
| Smooth Operator | [arXiv 正文](https://arxiv.org/html/2607.07491v2) 链接项目页，项目页的 Code 指向 mimic_retargeter_lab，形成论文—项目页—代码的对应链。 |
| NMR（额外补全） | [官方仓库](https://github.com/NJU3DV-HumanoidGroup/MakeTrackingEasy) 直接链接 RayZhao/NMR 的 Space 与模型仓库，区分在线演示和模型权重入口。 |
