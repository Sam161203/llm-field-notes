# 🧠 llm-field-notes

> A living, categorized digest of what's actually moving in AI.
> Curated by someone who does security testing on real AI systems — not scraped, not auto-generated.

[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![Last Updated](https://img.shields.io/badge/Last%20Updated-April%202026-blue.svg)]()
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## Why This Over Other Awesome-AI Lists?

There are 300+ "awesome-llm" and "awesome-ai" repos on GitHub. Most are link dumps maintained by people who read about these tools — not people who use them.

This repo is different in three ways:

- **Opinionated** — entries include a curator's take where relevant, not just a description
- **Security-aware** — AI security gets real treatment here, not a three-link afterthought
- **Honest about failure** — the [Fracture Lines](FRACTURE-LINES.md) document covers what the field hasn't solved, with sources

If you want 500 links with no context, there are better repos for that.

---

## 📚 Table of Contents

- [🧩 LLMs](#-llms)
- [🤖 Agents](#-agents)
- [🛠️ Skills & Tools](#%EF%B8%8F-skills--tools)
- [🔐 AI Security](#-ai-security)
- [📄 Research Highlights](#-research-highlights)
- [📦 Datasets](#-datasets)
- [🔭 Multimodal](#-multimodal)
- [🧪 Fine-Tuning & Training](#-fine-tuning--training)
- [🚀 Inference & Deployment](#-inference--deployment)
- [🌐 Open Source AI Ecosystems](#-open-source-ai-ecosystems)
- [⚠️ Fracture Lines — Open Problems in AI](#%EF%B8%8F-fracture-lines--open-problems-in-ai)
- [🤝 Contributing](#-contributing)

---

## 🧩 LLMs

> Foundation and instruction-tuned language models worth knowing.
> Sorted by relevance, not hype.

| Model | Creator | Context | Notable | License | Date |
|-------|---------|---------|---------|---------|------|
| Claude 3.7 Sonnet | Anthropic | 200K | Extended thinking, hybrid reasoning mode | Proprietary | Feb 2025 |
| Claude 3.5 Haiku | Anthropic | 200K | Fast, cheap, surprisingly capable | Proprietary | Nov 2024 |
| GPT-4o | OpenAI | 128K | Native multimodal, real-time voice | Proprietary | May 2024 |
| GPT-4.1 | OpenAI | 1M | Stronger coding, instruction following | Proprietary | Apr 2025 |
| o3 / o4-mini | OpenAI | 200K | Chain-of-thought reasoning models | Proprietary | Apr 2025 |
| Gemini 2.0 Flash | Google | 1M | Native tool use, fast inference | Proprietary | Jan 2025 |
| Gemini 2.5 Pro | Google | 1M | Top-tier reasoning, multimodal | Proprietary | Mar 2025 |
| DeepSeek-R1 | DeepSeek | 128K | Open-weight, o1-level reasoning via GRPO | MIT | Jan 2025 |
| DeepSeek-V3 | DeepSeek | 128K | MoE architecture, strong at code/math | MIT | Dec 2024 |
| Llama 3.3 70B | Meta | 128K | Best open 70B you can run locally | Llama 3 | Dec 2024 |
| Llama 3.1 405B | Meta | 128K | Largest open-weight model from Meta | Llama 3 | Jul 2024 |
| Mistral Small 3 | Mistral | 32K | 24B params, Apache 2.0, fast inference | Apache 2.0 | Jan 2025 |
| Mistral Large 2 | Mistral | 128K | 123B, multilingual, strong reasoning | Mistral Research | Jul 2024 |
| Qwen2.5-72B | Alibaba | 128K | Strong coding and math, underrated | Apache 2.0 | Sep 2024 |
| Phi-4 | Microsoft | 16K | 14B, punches way above weight | MIT | Dec 2024 |
| Command R+ | Cohere | 128K | RAG-optimized, enterprise focused | CC-BY-NC | Apr 2024 |
| Falcon 3 | TII | 32K | Open-weight, Arabic + multilingual | Apache 2.0 | Dec 2024 |

**📍 Curator's Take:**
> DeepSeek-R1 is the most important open-weight release in the past year — MIT licensed, o1-level reasoning, and it changed how the field thinks about training reasoning without SFT. If you haven't run it, run it.
> Phi-4 at 14B is the most surprising — small enough to run on consumer hardware, genuinely competitive on reasoning tasks.

---

## 🤖 Agents

> Systems where LLMs plan, act, use tools, and operate autonomously.
> Most are still fragile in production — see [Fracture Lines](FRACTURE-LINES.md#-agent-reliability--trust).

| Project | Creator | Description | Link |
|---------|---------|-------------|------|
| OpenAI Operator | OpenAI | Browser-use agent for real-world tasks | [openai.com](https://openai.com/index/introducing-operator/) |
| Claude Computer Use | Anthropic | LLM controlling desktop GUI | [docs.anthropic.com](https://docs.anthropic.com) |
| Google Mariner | Google DeepMind | Deep research + browser agent | [deepmind.google](https://deepmind.google) |
| LangGraph | LangChain | Stateful, cyclical multi-agent framework | [github](https://github.com/langchain-ai/langgraph) |
| CrewAI | CrewAI Inc. | Role-based multi-agent orchestration | [github](https://github.com/crewAIInc/crewAI) |
| AutoGen v0.4 | Microsoft | Async event-driven agent framework | [github](https://github.com/microsoft/autogen) |
| LlamaIndex Workflows | LlamaIndex | Event-driven agentic pipelines | [github](https://github.com/run-llama/llama_index) |
| OpenDevin | OpenDevin | Open-source software engineering agent | [github](https://github.com/OpenDevin/OpenDevin) |
| SWE-agent | Princeton NLP | Autonomous GitHub issue resolver | [github](https://github.com/princeton-nlp/SWE-agent) |
| Agno (phidata) | Phidata | Fast, memory-aware agent framework | [github](https://github.com/agno-agi/agno) |
| Composio | Composio | Tool integrations layer for agents (250+ tools) | [github](https://github.com/ComposioHQ/composio) |
| Browser-Use | browser-use | Python library for browser automation via LLMs | [github](https://github.com/browser-use/browser-use) |
| Smolagents | HuggingFace | Minimal, code-first agent library | [github](https://github.com/huggingface/smolagents) |

**📍 Curator's Take:**
> LangGraph is the one framework actually used at scale in production — stateful, cyclical, controllable. Most of the others are better for prototyping than shipping.
> From a security angle: agents are the most interesting attack surface right now. Indirect prompt injection through external data sources can fully hijack mid-task behavior with no patch available.

---

## 🛠️ Skills & Tools

> Frameworks, libraries, and protocols that make AI actually useful in production.

### Orchestration & Protocols

| Tool | What It Does | Link |
|------|-------------|------|
| MCP (Model Context Protocol) | Anthropic's open standard for LLM ↔ tool communication | [modelcontextprotocol.io](https://modelcontextprotocol.io) |
| LangChain | Most-used LLM orchestration framework | [github](https://github.com/langchain-ai/langchain) |
| LlamaIndex | Data framework for RAG and LLM apps | [github](https://github.com/run-llama/llama_index) |
| Haystack | End-to-end NLP + LLM pipelines | [github](https://github.com/deepset-ai/haystack) |
| Semantic Kernel | Microsoft's SDK for AI integration | [github](https://github.com/microsoft/semantic-kernel) |

### LLM APIs & Routing

| Tool | What It Does | Link |
|------|-------------|------|
| LiteLLM | Unified API for 100+ LLMs — drop-in OpenAI replacement | [github](https://github.com/BerriAI/litellm) |
| OpenRouter | Route between models, pay per token | [openrouter.ai](https://openrouter.ai) |
| PortKey | LLM gateway — fallbacks, caching, observability | [github](https://github.com/Portkey-AI/gateway) |
| Martian | Route to cheapest model that can handle the task | [withmartian.com](https://withmartian.com) |

### Structured Outputs & Parsing

| Tool | What It Does | Link |
|------|-------------|------|
| Instructor | Pydantic-backed structured outputs from any LLM | [github](https://github.com/jxnl/instructor) |
| Outlines | Constrained generation — JSON, regex, grammar | [github](https://github.com/outlines-dev/outlines) |
| Marvin | Lightweight AI function decorators | [github](https://github.com/prefecthq/marvin) |
| Guardrails AI | Validation + correction for LLM outputs | [github](https://github.com/guardrails-ai/guardrails) |

### Prompt Engineering & Optimization

| Tool | What It Does | Link |
|------|-------------|------|
| DSPy | Programmatic prompt optimization — no manual tuning | [github](https://github.com/stanfordnlp/dspy) |
| PromptFlow | Microsoft's prompt engineering + eval suite | [github](https://github.com/microsoft/promptflow) |
| TextGrad | Backpropagation through text for prompt tuning | [github](https://github.com/zou-group/textgrad) |

### RAG & Vector Search

| Tool | What It Does | Link |
|------|-------------|------|
| Chroma | Lightweight open-source vector DB | [github](https://github.com/chroma-core/chroma) |
| Weaviate | Production vector DB with hybrid search | [github](https://github.com/weaviate/weaviate) |
| Qdrant | Rust-based, high-performance vector search | [github](https://github.com/qdrant/qdrant) |
| pgvector | Postgres extension for vector similarity search | [github](https://github.com/pgvector/pgvector) |
| Ragas | Evaluation framework specifically for RAG pipelines | [github](https://github.com/explodinggradients/ragas) |

**📍 Curator's Take:**
> Qdrant is underrated for production RAG — Rust backend, lower memory overhead than Chroma, and a better filtering API. Chroma is fine for local dev.
> Ragas is the only RAG eval framework worth using — everything else just checks retrieval recall without testing generation quality.

### Local LLMs

| Tool | What It Does | Link |
|------|-------------|------|
| Ollama | Run open models locally, one command | [github](https://github.com/ollama/ollama) |
| LM Studio | Desktop GUI for local LLMs | [lmstudio.ai](https://lmstudio.ai) |
| llama.cpp | C++ inference for Llama-family models | [github](https://github.com/ggerganov/llama.cpp) |
| Jan | Offline ChatGPT alternative, desktop app | [github](https://github.com/janhq/jan) |
| GPT4All | Local LLM runner with privacy focus | [github](https://github.com/nomic-ai/gpt4all) |

---

## 🔐 AI Security

> Attacks, defenses, red teaming, and the real intersection of AI and security.
> This section gets more attention here than in most AI repos because it deserves it.

### Attack Techniques

| Technique | Description | Resource |
|-----------|-------------|----------|
| Prompt Injection | Hijacking LLM behavior via malicious input in context | [OWASP LLM01](https://owasp.org/www-project-top-10-for-large-language-model-applications/) |
| Indirect Prompt Injection | Injecting instructions through external data the LLM reads — emails, docs, web pages | [Greshake et al. 2023](https://arxiv.org/abs/2302.12173) |
| Jailbreaking | Bypassing safety filters to elicit restricted outputs | [JailbreakBench](https://github.com/JailbreakBench/jailbreakbench) |
| Data Poisoning | Corrupting training or fine-tuning data to influence model behavior | [Nightshade Paper](https://arxiv.org/abs/2310.13828) |
| Model Inversion | Extracting memorized training data from model outputs | [arxiv](https://arxiv.org/abs/2311.17035) |
| Adversarial Inputs | Crafted inputs that fool predictions in vision/NLP tasks | [CleverHans](https://github.com/cleverhans-lab/cleverhans) |
| Backdoor Attacks | Planting triggers in models during training | [TrojAI](https://trojai.readthedocs.io) |
| Model Theft | Reconstructing a model via query-based extraction | [Tramèr et al.](https://arxiv.org/abs/1609.02943) |
| Agent Hijacking | Convincing an AI agent to take unintended actions mid-task via injected context | [Anthropic Research](https://www.anthropic.com/research) |
| Many-Shot Jailbreaking | Using long-context to override safety training via volume of examples | [Anthropic](https://www.anthropic.com/research/many-shot-jailbreaking) |
| RAG Poisoning | Injecting malicious content into knowledge bases to steer retrieval-augmented responses | [arxiv](https://arxiv.org/abs/2402.07867) |

### Defense & Red Teaming Tools

| Tool | Description | Link |
|------|-------------|------|
| Microsoft PyRIT | Python Risk Identification Toolkit for LLM red teaming | [github](https://github.com/Azure/PyRIT) |
| Garak | LLM vulnerability scanner — probes dozens of failure modes | [github](https://github.com/leondz/garak) |
| PromptBench | Robustness evaluation benchmark for LLMs | [github](https://github.com/microsoft/promptbench) |
| LLM Guard | Runtime input/output scanning for LLMs | [github](https://github.com/protectai/llm-guard) |
| Rebuff | Prompt injection detection layer | [github](https://github.com/protectai/rebuff) |
| AI Goat | Deliberately vulnerable LLM app for security training | [github](https://github.com/dhammon/ai-goat) |
| Vigil | LLM prompt injection and jailbreak detection | [github](https://github.com/deadbits/vigil-llm) |

### Standards & Frameworks

| Resource | Description | Link |
|----------|-------------|------|
| OWASP LLM Top 10 | The 10 most critical LLM application security risks | [owasp.org](https://owasp.org/www-project-top-10-for-large-language-model-applications/) |
| MITRE ATLAS | Adversarial threat landscape for AI systems | [atlas.mitre.org](https://atlas.mitre.org) |
| NIST AI RMF | US government AI risk management framework | [nist.gov](https://www.nist.gov/system/files/documents/2023/01/26/AI%20RMF%201.0.pdf) |
| Google SAIF | Google's Secure AI Framework | [safety.google](https://safety.google/cybersecurity-advancements/saif/) |

**📍 Curator's Take:**
> Indirect prompt injection is the most dangerous and least patched attack class right now. It's structural — LLMs can't reliably distinguish between "instructions from the system" and "instructions embedded in data they're reading." There is no clean fix, only mitigations.
> Garak is the tool most people sleep on — run it against any LLM-facing endpoint before you ship.

---

## 📄 Research Highlights

> Papers that actually changed how people think and build.
> Ordered roughly by long-term impact, not recency.

| Paper | From | What It Established | Link |
|-------|------|---------------------|------|
| Attention Is All You Need | Google Brain | Original Transformer — everything descends from this | [arxiv](https://arxiv.org/abs/1706.03762) |
| RLHF / InstructGPT | OpenAI | Training LLMs with human feedback — how alignment is done today | [arxiv](https://arxiv.org/abs/2203.02155) |
| Constitutional AI | Anthropic | RLHF replacement via self-critique and principles | [arxiv](https://arxiv.org/abs/2212.08073) |
| LoRA | Microsoft | Parameter-efficient fine-tuning — made fine-tuning accessible | [arxiv](https://arxiv.org/abs/2106.09685) |
| ReAct | Google / Princeton | Reasoning + Acting interleaved — foundation for modern agents | [arxiv](https://arxiv.org/abs/2210.03629) |
| Toolformer | Meta AI | LLMs that learn to call APIs themselves | [arxiv](https://arxiv.org/abs/2302.04761) |
| Tree of Thoughts | Princeton / Google | Structured multi-path reasoning over problems | [arxiv](https://arxiv.org/abs/2305.10601) |
| DeepSeek-R1 | DeepSeek | GRPO-based reasoning without supervised fine-tuning | [arxiv](https://arxiv.org/abs/2501.12948) |
| Scaling LLM Test-Time Compute | Google | More inference compute → better outputs | [arxiv](https://arxiv.org/abs/2408.03314) |
| Mixtral 8x7B | Mistral | Sparse mixture-of-experts beats dense models | [arxiv](https://arxiv.org/abs/2401.04088) |
| AgentBench | THUDM | First serious benchmark for LLM-as-agent | [arxiv](https://arxiv.org/abs/2308.03688) |
| GSM-Symbolic | Apple | Adding irrelevant clauses tanks LLM math — reasoning is brittle | [arxiv](https://arxiv.org/abs/2410.05229) |
| Sleeper Agents | Anthropic | Safety training doesn't remove hidden backdoors | [arxiv](https://arxiv.org/abs/2401.05566) |
| Many-Shot Jailbreaking | Anthropic | Long context can override safety training at scale | [anthropic.com](https://www.anthropic.com/research/many-shot-jailbreaking) |
| Lost in the Middle | Stanford / UC Berkeley | Models miss info placed in middle of long contexts | [arxiv](https://arxiv.org/abs/2307.03172) |

---

## 📦 Datasets

> Datasets powering training, fine-tuning, and evaluation.

### Pretraining

| Dataset | Size | Description | Link |
|---------|------|-------------|------|
| FineWeb | 15T tokens | High-quality web data, outperforms Common Crawl | [HuggingFace](https://huggingface.co/datasets/HuggingFaceFW/fineweb) |
| RedPajama-V2 | 30T tokens | Open dataset for LLM pretraining | [HuggingFace](https://huggingface.co/datasets/togethercomputer/RedPajama-Data-V2) |
| The Pile | 825GB | 22 diverse sources, foundational open dataset | [github](https://github.com/EleutherAI/the-pile) |
| ROOTS | 1.6TB | Multilingual, 59 languages | [HuggingFace](https://huggingface.co/bigscience-data) |
| Dolma | 3T tokens | OLMo's pretraining dataset, fully open | [HuggingFace](https://huggingface.co/datasets/allenai/dolma) |

### Instruction Fine-Tuning

| Dataset | Description | Link |
|---------|-------------|------|
| OpenHermes 2.5 | High-quality synthetic instruction data | [HuggingFace](https://huggingface.co/datasets/teknium/OpenHermes-2.5) |
| UltraFeedback | 64K preference pairs for RLHF/DPO | [HuggingFace](https://huggingface.co/datasets/openbmb/UltraFeedback) |
| Alpaca | 52K GPT-4 generated instruction-following examples | [github](https://github.com/tatsu-lab/stanford_alpaca) |
| Dolly 15K | 15K human-written instructions from Databricks employees | [HuggingFace](https://huggingface.co/datasets/databricks/databricks-dolly-15k) |
| WizardLM Evol-Instruct | Evolved instructions of increasing complexity | [HuggingFace](https://huggingface.co/datasets/WizardLM/WizardLM_evol_instruct_V2_196k) |

### Evaluation / Benchmarks

| Benchmark | Measures | Link |
|-----------|---------|------|
| MMLU | Knowledge across 57 subjects | [github](https://github.com/hendrycks/test) |
| HumanEval | Code generation correctness | [github](https://github.com/openai/human-eval) |
| MATH | High-school to competition-level math | [github](https://github.com/hendrycks/math) |
| HellaSwag | Commonsense reasoning | [github](https://github.com/rowanz/hellaswag) |
| MT-Bench | Multi-turn instruction following quality | [github](https://github.com/lm-sys/FastChat) |
| TruthfulQA | Measures hallucination and truthfulness | [github](https://github.com/sylinrl/TruthfulQA) |
| WildChat | Real user-LLM conversations in the wild | [HuggingFace](https://huggingface.co/datasets/allenai/WildChat) |
| BIG-Bench Hard | Tasks where LLMs still struggle | [github](https://github.com/suzgunmirac/BIG-Bench-Hard) |

---

## 🔭 Multimodal

> Models and tools that go beyond text.

### Vision-Language Models

| Model | Modalities | Notes | Link |
|-------|-----------|-------|------|
| GPT-4o | Text, image, audio, video | Best overall multimodal | [openai.com](https://openai.com) |
| Gemini 2.5 Pro | Text, image, audio, video, code | Native multimodal from ground up | [google.com](https://google.com) |
| Claude 3.7 Sonnet | Text + vision | Strong on documents, diagrams, structured data | [anthropic.com](https://anthropic.com) |
| Qwen2.5-VL | Text + vision | Open weights, very strong at doc/chart understanding | [github](https://github.com/QwenLM/Qwen2.5-VL) |
| LLaVA-Next | Text + vision | Open-source visual instruction tuning baseline | [github](https://github.com/haotian-liu/LLaVA) |
| InternVL2 | Text + vision | Competitive open-source vision model | [github](https://github.com/OpenGVLab/InternVL) |
| Phi-3.5 Vision | Text + vision | Lightweight 4.2B — small, surprisingly capable | [HuggingFace](https://huggingface.co/microsoft/Phi-3.5-vision-instruct) |

### Audio & Speech

| Model | What It Does | Link |
|-------|-------------|------|
| Whisper v3 | Best open speech-to-text | [github](https://github.com/openai/whisper) |
| MusicGen | Text-to-music generation | [github](https://github.com/facebookresearch/audiocraft) |
| Bark | Text-to-speech with emotion and tone control | [github](https://github.com/suno-ai/bark) |
| SeamlessM4T | Translate speech across 100 languages | [github](https://github.com/facebookresearch/seamless_communication) |

### Image & Video Generation

| Model | Description | Link |
|-------|-------------|------|
| FLUX.1 | State-of-the-art open image generation | [github](https://github.com/black-forest-labs/flux) |
| Stable Diffusion 3.5 | Open text-to-image, highly customizable | [github](https://github.com/Stability-AI/generative-models) |
| Sora | OpenAI's video generation model | [openai.com/sora](https://openai.com/sora) |
| Kling | High-quality video generation from Kuaishou | [klingai.com](https://klingai.com) |
| CogVideoX | Open-source video generation | [github](https://github.com/THUDM/CogVideo) |

---

## 🧪 Fine-Tuning & Training

> Tools and methods for adapting models to specific tasks without training from scratch.

| Tool / Method | Description | Link |
|--------------|-------------|------|
| Axolotl | Streamlined fine-tuning for Llama, Mistral, Falcon | [github](https://github.com/OpenAccess-AI-Collective/axolotl) |
| Unsloth | 2x faster fine-tuning, 70% less VRAM — actually works | [github](https://github.com/unslothai/unsloth) |
| TRL | HuggingFace's RLHF, DPO, PPO training library | [github](https://github.com/huggingface/trl) |
| LLaMA-Factory | All-in-one fine-tuning framework supporting 100+ models | [github](https://github.com/hiyouga/LLaMA-Factory) |
| LoRA / QLoRA | Train only adapter layers — dramatically reduces compute | [arxiv](https://arxiv.org/abs/2106.09685) |
| DPO | Direct Preference Optimization — RLHF without reward model | [arxiv](https://arxiv.org/abs/2305.18290) |
| ORPO | Fine-tune + align in one training step | [arxiv](https://arxiv.org/abs/2403.07691) |

**📍 Curator's Take:**
> Unsloth is the practical choice if you're fine-tuning on consumer or single-GPU hardware — the VRAM savings are real and it's not sacrificing accuracy to get there. Use it with QLoRA.

---

## 🚀 Inference & Deployment

> Getting models into production without losing your mind.

| Tool | Description | Link |
|------|-------------|------|
| vLLM | PagedAttention-based, highest-throughput open serving | [github](https://github.com/vllm-project/vllm) |
| TGI | HuggingFace Text Generation Inference — production-grade | [github](https://github.com/huggingface/text-generation-inference) |
| TensorRT-LLM | NVIDIA's optimized inference engine | [github](https://github.com/NVIDIA/TensorRT-LLM) |
| Triton Inference Server | Multi-model production serving from NVIDIA | [github](https://github.com/triton-inference-server/server) |
| BentoML | Package and serve ML models as APIs | [github](https://github.com/bentoml/BentoML) |
| Replicate | Run open models via API, pay per second | [replicate.com](https://replicate.com) |
| Modal | Serverless GPU cloud — spin up in seconds | [modal.com](https://modal.com) |
| Groq | Purpose-built LPU, lowest latency inference available | [groq.com](https://groq.com) |

**📍 Curator's Take:**
> vLLM for high-throughput batch serving. Groq for latency-sensitive, real-time use cases. Don't use TGI unless you're already in the HuggingFace ecosystem — vLLM has better throughput and a cleaner API.

---

## 🌐 Open Source AI Ecosystems

> Communities and platforms where real AI development happens in the open.

| Platform | Description | Link |
|---------|-------------|------|
| HuggingFace | Models, datasets, Spaces — the GitHub of AI | [huggingface.co](https://huggingface.co) |
| EleutherAI | Nonprofit research, open LLMs (GPT-J, Pythia, evaluation) | [eleutherai.org](https://www.eleutherai.org) |
| Together AI | Fine-tuning + inference platform for open models | [together.ai](https://together.ai) |
| LAION | Open large-scale datasets — LAION-5B and successors | [laion.ai](https://laion.ai) |
| Allen AI (AI2) | Academic research, open models including OLMo | [allenai.org](https://allenai.org) |
| Nous Research | Community fine-tuning, Hermes model family | [nousresearch.com](https://nousresearch.com) |

---

## ⚠️ Fracture Lines — Open Problems in AI

This section lives in its own dedicated document because it deserves more than a table.

**→ [Read the full Fracture Lines document](FRACTURE-LINES.md)**

A quick overview of what's covered:

| Problem | TL;DR |
|---------|-------|
| Alignment & Control | No reliable way to ensure AI does what we actually intend |
| Hallucination & Factuality | Structurally hard to fix — models don't "know" facts like databases |
| Long-Context Reliability | 1M token windows, but models lose info in the middle |
| Reasoning vs Pattern Matching | Frontier "reasoning" is more brittle than it looks |
| Agent Reliability | Multi-step agents still fail in unpredictable ways in production |
| AI Security Attack Surface | Years behind software security — prompt injection has no patch |
| Compute Concentration | Pretraining is becoming exclusive to a handful of orgs |
| Broken Evaluation | Benchmarks are saturated, contaminated, and misaligned with real capability |
| Environmental Cost | Energy and water usage largely undisclosed and unaccounted |

---

## 🤝 Contributing

Open a PR if you have something worth adding. One entry per PR.

See **[CONTRIBUTING.md](CONTRIBUTING.md)** for full guidelines.

Quick rules:
- Real tools and papers only — no vaporware, no demos
- Working source links required
- Keep the table format consistent
- Personal experience with a tool? Add a one-liner note in your PR description

---

<div align="center">

### Happy if others contribute here.
One honest, maintained place for the AI ecosystem — by people who actually build and test this stuff.

**[⭐ Star](https://github.com/Sam161203/ai-pulse)** · **[🔀 Fork](https://github.com/Sam161203/ai-pulse/fork)** · **[📬 Open a PR](https://github.com/Sam161203/ai-pulse/pulls)**

<sub>Maintained by <a href="https://github.com/Sam161203">Sam</a> · Bug bounty hunter · AI security · Open to contributions</sub>

</div>
