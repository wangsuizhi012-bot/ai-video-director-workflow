# ai-video-director-workflow

> AI Video Director Workflow — 一套"人做决策、AI 做执行"的 AI 视频导演工作流开源方法论。
> 导演只动嘴（审核 / 改稿 / 提供思路），Agent 负责写稿、分镜、生成、迭代。

This is an open-source methodology for directing AI-generated videos. The human is the director who makes decisions and gives feedback; the agent handles writing, storyboarding, generation, and iteration. Built from a real production case: *Qianxi Signal · Self-Replicating AI Reflection* (千禧信号·自复制AI反思).

## 痛点 / Why This Workflow

| 痛点 | 现状 | 本工作流的解法 |
|---|---|---|
| ① 主流视频工具是空模板，全靠人填 | 打开工具是一张白纸，所有分镜、提示词、节奏都要导演自己手写 | **预填式看板**：Agent 先按剧本把镜头卡片、提示词、参考图、旁白全部预填好，导演只做验收 |
| ② 纯命令行流水线无可视化 | 生成过程是一串脚本日志，看不到每个镜头到了哪一步 | **导演台打勾推进**：镜头卡片 + 状态点（IMG / END / AUD / LTX / VID / OK），每步完成即打勾 |
| ③ 迭代无法归因 | 改了一堆东西，出问题了不知道是哪一步引入的 | **单变量迭代 + 版本快照**：每次只改一个变量，prompt 与结果成对存档，可回退对比 |
| ④ 生成前无验收标准，靠感觉返工 | 图出了才发现不对，全凭"看着不行"返工 | **验收标准前置**：每镜生成前先写一句话通过标准，生成后逐条对照 |

## 解决方案总览 / Solution Overview

一条六阶段流水线，加上两件配套"武器"（Prompt 分层、验收标准）和三条迭代纪律：

```
点子输入 → 稿子输出 → 审稿 → 分镜与生成 → 导演台审核 → 迭代与成片
```

- **预填式看板（Prefilled Board）**：Agent 按剧本预填镜头卡片与资产，导演只验收，不填表。
- **导演台（Director Board）**：可视化看板，镜头卡片 + 状态点（IMG/END/AUD/LTX/VID/OK）打勾推进。
- **验收标准前置（Rubric First）**：每镜一句通过标准，生成前写、生成后对照。
- **单变量迭代（Single-Variable Iteration）**：每次只改一个变量，其余冻结。
- **版本快照（Version Snapshot）**：prompt + 结果成对存档，可回退、可对比。

## 快速开始 / Quick Start

```bash
git clone https://github.com/<your-name>/ai-video-director-workflow.git
cd ai-video-director-workflow
```

四步走（4 steps）：

1. **丢点子（Give an idea）**：把点子丢给 Agent，它写成旁白/文案稿 → `docs/workflow.md` Stage 1–2
2. **审稿（Review the script）**：指出哪里好、哪里不好，Agent 据此修改 → `docs/workflow.md` Stage 3
3. **验收分镜（Approve the storyboard）**：Agent 出分镜与提示词，导演台逐镜打勾验收 → `docs/director-board.md`
4. **迭代到成片（Iterate to final）**：按反馈改提示词、重生成，满意即成片 → `docs/iteration.md`

## 目录结构 / Directory Structure

```
ai-video-director-workflow/
├── README.md                  # 项目总览（本文件）
├── docs/
│   ├── workflow.md            # 六阶段工作流详解（输入/输出/负责人/要点）
│   ├── prompt-system.md       # Prompt 分层体系（固定层/可变层）
│   ├── review-rubric.md       # 镜头验收标准模板与方法
│   ├── iteration.md           # 迭代纪律（单变量/快照/批量策略/A-B）
│   ├── director-board.md      # 导演台看板规范（状态点/回填/实战）
│   └── case-study.md          # 实战案例：千禧信号·自复制AI反思
└── templates/
    ├── shot-rubric.md         # 镜头验收标准模板（可直接复制）
    └── prompt-block.md        # Prompt 分层模板（可直接复制）
```

## 案例 / Case Study

实战案例《千禧信号·自复制AI反思》：22 镜 4 场叙事片（245s / 1920x1080 / 30fps），本地 ComfyUI 生成、Remotion 总装、IndexTTS-2 音色克隆、ByteCut Director 预填看板。详见 [`docs/case-study.md`](docs/case-study.md)。

## License

MIT
