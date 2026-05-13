# 企智汇 QiZhiHui


**基于 MiMo-V2.5‑Pro 的企业级多模态知识库智能管理系统**

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![MiMo Powered](https://img.shields.io/badge/Powered%20by-MiMo--V2.5--Pro-orange)](https://mimo.xiaomi.com)
[![Docker](https://img.shields.io/badge/Docker-Supported-brightgreen)](docker-compose.yml)

> 统一管理文档、图片、音频、视频，用 100 万 Token 超长上下文实现真正的语义检索与智能问答。  
> 让企业的每一份知识都能被“问到即所得”。

---

## 痛点与方案

企业知识管理面临三大难题：

- **知识分散**：PDF、Word、Excel、图片、会议录音、培训视频散落各处，无法统一调用。
- **检索低效**：关键词匹配式搜索无法理解业务意图，员工一半的时间都在“找”知识。
- **多模态处理难**：图片里的文字、音频里的指令、视频中的场景长期处于沉睡状态，价值无法释放。

**企智汇** 构建了统一的多模态知识库，并借助 **MiMo-V2.5‑Pro** 的以下特性，让知识真正“活”起来：

- **100 万 Token 超长上下文窗口** – 可将整本产品手册、完整会议录音直接送入模型，精准提取跨章节、跨段落的信息。
- **MoE 架构高效推理** – 激活参数仅 150 亿，兼顾高吞吐与低成本。
- **原生多模态理解** – 同时处理文本、图像、音频，避免信息割裂。

## 功能演示

| 多模态上传 | 智能语义检索 | 答案溯源 |
| :---: | :---: | :---: |
| ![上传PDF/图片/音频](docs/images/upload.gif) | ![自然语言检索](docs/images/search.gif) | ![查看答案来源](docs/images/trace.gif) |

*（上方为 GIF 动图，请替换为实际演示录屏）*

## 技术架构

```
┌──────────────┐     ┌──────────────┐     ┌─────────────────┐
│  Vue.js 前端  │────▶│ Spring Boot  │────▶│  MiMo-V2.5-Pro  │
│  (管理界面)   │     │   (业务逻辑)  │     │  (100万Token推理) │
└──────────────┘     └──────┬───────┘     └─────────────────┘
                            │
              ┌─────────────┴─────────────┐
              │   MongoDB (非结构化元数据) │
              │   MySQL   (知识图谱)       │
              └───────────────────────────┘
```

详细设计见 [`docs/architecture.md`](docs/architecture.md)。

## 快速开始

### 环境要求
- Docker ≥ 20.10
- 已注册 MiMo API 账号并获取 API Key

### 一键部署
```bash
git clone https://github.com/your-org/QiZhiHui.git
cd QiZhiHui

# 配置环境变量（填入你的 MiMo API Key）
cp .env.example .env
# 编辑 .env 中的 MIMO_API_KEY 等字段

docker compose up -d
```
浏览器访问 `http://localhost:3000` 即可体验。

## 本项目与 MiMo Orbit 100T Token 计划

企智汇基于 **MiMo-V2.5‑Pro** 构建，正在申请 **“MiMo Orbit 100T Token 计划”** 的 Max 档额度（16 亿 Credits），以支持以下真实高消耗场景：

| 场景 | 预估 Token 消耗 | 说明 |
|------|----------------|------|
| 历史数据批量导入 | ~100 亿 Token | 处理 10 万份多模态文档，提取文本、OCR、ASR 转写 |
| 模型上下文适配 | ~150 亿 Token | 利用长上下文 Few‑shot 对垂直领域进行适配（替代微调） |
| 日常检索与问答 | ~150 亿 Token | 支撑 1000 名员工并发使用，每人日均 10 次长上下文检索 |

> 完整 Token 消耗规划及预测曲线见 [`docs/token-consumption-plan.md`](docs/token-consumption-plan.md)。

## 项目里程碑

| 阶段 | 目标 | 预计完成 |
|------|------|---------|
| **v0.3.0** | 多模态采集与预处理流水线、基础语义检索 | ✅ 已完成 |
| **v0.5.0** | 智能问答、答案溯源、权限管理 | 🔄 进行中 |
| **v1.0.0** | 企业级 SaaS 多租户支持、MCP 智能体集成 | 📅 2026 Q4 |

## 文档与贡献

- 📘 [系统架构](docs/architecture.md)  
- 📘 [API 参考](docs/api-reference.md)  
- 📘 [部署指南](docs/deployment.md)  
- 📘 [用户手册](docs/user-guide.md)  
- 📘 [Token 消耗计划](docs/token-consumption-plan.md)  
- 📘 [风险管理](docs/risk-management.md)  

欢迎贡献代码或提出建议，请参考 [`CONTRIBUTING.md`](CONTRIBUTING.md) 并遵守我们的行为准则。

## 许可证

本项目采用 [Apache License 2.0](LICENSE) 开源。

## 致谢

- 感谢 [小米 MiMo 团队](https://mimo.xiaomi.com) 提供的模型与 Token 支持。
- 项目使用了 LangChain、Dify、Spring Boot 等优秀开源框架。
