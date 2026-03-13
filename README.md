# Multi-Platform-Content-Engine
A Dify workflow for automated multi-platform content generation. It uses Gemini 2.5 Flash for multimodal analysis (images/docs) and GPT-4 for automated quality auditing. Features a "Verify-Retry" loop and Python-based regex sanitization to ensure structured, high-quality social media copy.
Description / 项目简介
A robust Dify-based workflow designed for automated multi-platform content generation.
本项目基于 Dify 0.6.0 构建，通过整合多模态输入处理与自动化质量审计，实现了从原始素材到社交媒体文案的高效生产线。

The engine uses Gemini 2.5 Flash for deep visual and textual analysis, while GPT-4 acts as a "Quality Auditor" to ensure every output meets professional standards.
核心特色在于其内置的“生成-校验-重试”闭环逻辑，能自动修复低质量文案并确保多平台适配。

Key Features / 核心特性
Multimodal Input Processing / 多模态输入: Simultaneously processes image files, PDF documents, and text drafts to build a comprehensive content foundation.

同时解析 user_file 列表中的视觉信息与文档提取器中的文本上下文。

Intelligent Platform Adaptation / 平台智能适配: Automatically standardizes platform names (e.g., "X" to "Twitter") and adjusts tone for Instagram, LinkedIn, etc.

通过参数提取器实现平台名称归一化，并针对各平台调性精准输出。

Dual-LLM Audit Loop / 双模型审计闭环: Uses GPT-4 to verify if the generated captions are compliant and complete.

引入 If-Else 条件分支：若审核未通过，系统将触发重试机制（LLM 4 -> LLM 5）。

Python-Powered Sanitization / 代码级数据清洗: Employs Python Regex to extract and repair JSON blocks from raw LLM responses.

内置 Python 脚本利用 re.search(r'\{.*\}', ...) 强制提取 JSON，解决模型输出冗余文字导致的解析错误。

Technical Workflow / 技术架构
Ingestion / 输入层: Captures image/file lists and specific tone preferences via the Start node.

Analysis / 分析层: Gemini 2.5 Flash synthesizes core messages, engagement opportunities, and strategic insights.

Drafting / 生成层: Tailors copy for each identified platform in a structured JSON format.

Verification / 校验层: GPT-4 audits the draft; if results are FALSE, the workflow triggers a second-pass generation.

Sanitization / 清洗层: Python Code nodes format the JSON into clean, human-readable text blocks.

Deployment / 快速部署
DSL Import: Download 2.yml and import it into your Dify workspace.

API Configuration: Ensure Google Gemini and OpenAI providers are configured in Dify.

Output: Enjoy high-quality, verified social media content across all your platforms.
