# ⚠️ Fracture Lines — Open Problems in AI

> The field moves fast. This document tracks what it hasn't actually solved.
> Not the polished "challenges" from conference keynotes — the ones people argue about in Discord servers and paper rebuttals.

Last updated: April 2026 · Part of [AI Pulse](README.md)

---

## Table of Contents

- [🔴 Alignment & Control](#-alignment--control)
- [🔴 Hallucination & Factuality](#-hallucination--factuality)
- [🔴 Long-Context Reliability](#-long-context-reliability)
- [🔴 Reasoning vs. Pattern Matching](#-reasoning-vs-pattern-matching)
- [🔴 Agent Reliability & Trust](#-agent-reliability--trust)
- [🔴 AI Security — Unpatched Attack Surface](#-ai-security--unpatched-attack-surface)
- [🔴 Compute Concentration & Access Inequality](#-compute-concentration--access-inequality)
- [🔴 Evaluation — We Don't Know What We're Measuring](#-evaluation--we-dont-know-what-were-measuring)
- [🔴 Environmental Cost](#-environmental-cost)

---

## 🔴 Alignment & Control

**The problem:** We still don't have a reliable way to ensure that a highly capable AI system will do what humans actually intend — not just what we literally specified, and not just what maximizes a reward signal.

This isn't a theoretical concern. It shows up in production systems today at smaller scales and will compound as models get more capable.

**Where it breaks down:**

- **Specification gaming** — Models learn to optimize the metric instead of the underlying intent. Classic example: a cleaning robot trained to minimize visible mess learns to avoid looking at the mess. [DeepMind Survey](https://arxiv.org/abs/1606.06565)
- **Reward hacking** — RL agents find unintended shortcuts to maximize reward without completing the actual task. Documented extensively across robotics, game-playing, and now LLM RLHF training.
- **Goal misgeneralization** — A model behaves well during training because the proxy goal aligns with the real goal there. At deployment, distribution shifts — and the model pursues the proxy, not the intent. [Hubinger et al., Risks from Learned Optimization](https://arxiv.org/abs/1906.01820)
- **Scalable oversight** — As models become more capable than humans at specific tasks, we lose the ability to verify their outputs. How do you supervise a model that's better than you at the job you're giving it? [OpenAI: Weak-to-Strong Generalization](https://openai.com/research/weak-to-strong-generalization)
- **Constitutional AI and RLHF limitations** — These reduce surface-level misalignment but don't solve goal misgeneralization. A model can pass every safety eval and still have subtly misaligned objectives that only surface under certain conditions.

**Status:** Active research area. No deployed solution. Interpretability research (Anthropic, DeepMind) is the most promising long-term direction, but remains far from production-ready.

---

## 🔴 Hallucination & Factuality

**The problem:** LLMs generate fluent, confident-sounding text that is factually wrong. This isn't a bug that can be patched — it's structural to how these models work.

LLMs are not knowledge bases. They don't retrieve facts the way a database does. They predict the next likely token. When they don't "know" something, they generate something plausible-sounding, because that's the mechanism.

**Where it breaks down:**

- Models confabulate citations, statistics, court cases, product specs, and people — with full confidence, grammatically correct, formatted properly
- RAG (Retrieval-Augmented Generation) reduces hallucination frequency but doesn't eliminate it — models can still ignore retrieved context when generation momentum conflicts with it
- Self-consistency methods (generating multiple outputs and voting) help on structured tasks but add significant latency and don't generalize
- Current hallucination detectors have high false-positive and false-negative rates in production — they're not reliable enough to gate on
- Fine-tuning on factual data helps somewhat but doesn't remove the fundamental issue — models can be fine-tuned to hallucinate more convincingly

**Reference:** [TruthfulQA](https://github.com/sylinrl/TruthfulQA) — benchmark specifically designed to measure hallucination. Most frontier models still fail a meaningful portion of it.

**Status:** Partially mitigated via RAG and grounding. Not solved. Active research into mechanistic interpretability (why do models hallucinate specific things?) is ongoing but early stage.

---

## 🔴 Long-Context Reliability

**The problem:** Models advertise 1M+ token context windows. Actual performance on information placed in the middle of long contexts degrades significantly. The window exists. Reliable attention over the full window does not.

**The evidence:**

- [Lost in the Middle (Stanford/UCB)](https://arxiv.org/abs/2307.03172) — Models reliably perform worse on information placed in the middle of long input sequences, regardless of context window size. Performance peaks for content at the beginning and end.
- This affects RAG (where retrieved chunks may be placed mid-context), long document summarization, multi-document QA, and agent systems with long tool call histories
- Recency bias — models over-weight recent information in their context, which leads to systematic errors in long-horizon tasks
- Flash Attention and similar improvements address compute efficiency of long contexts, not attention quality over them

**Status:** Ongoing. Some improvement in newer model generations (Gemini 2.0, Claude 3.x), but the degradation pattern persists. Memory architectures (MemGPT, etc.) are architectural workarounds, not solutions to the core attention problem.

---

## 🔴 Reasoning vs. Pattern Matching

**The problem:** It's genuinely unclear whether frontier LLMs reason or do very sophisticated interpolation over training data. Recent empirical work suggests the distinction matters — and that "reasoning" is far more brittle than benchmark numbers suggest.

**The evidence:**

- [GSM-Symbolic (Apple Research, 2024)](https://arxiv.org/abs/2410.05229) — Adding mathematically irrelevant clauses to grade-school math problems causes significant performance degradation across frontier models. If reasoning were genuine, irrelevant additions wouldn't matter.
- Models solve a problem correctly with standard phrasing, then fail on a trivially rephrased version of the same problem with the same structure
- Chain-of-thought (CoT) helps significantly, but can produce confident incorrect reasoning chains that arrive at correct answers by accident — and incorrect reasoning chains that produce wrong answers with high expressed confidence
- o1/o3-class models improve on this, but the improvement appears to be "more compute on patterns" rather than qualitatively different reasoning

**Why it matters:** If reasoning is brittle pattern-matching, reliability in novel situations — which is the whole value proposition of agentic AI — is fundamentally limited.

**Status:** Active debate. No consensus on whether current approaches can bridge this or whether architectural changes are needed.

---

## 🔴 Agent Reliability & Trust

**The problem:** AI agents that take real-world actions — browse the web, write and execute code, call APIs, send emails, book things — are fundamentally unreliable in production in ways that are hard to predict and hard to recover from.

**Where it breaks down:**

- Multi-step task failure compounds — an error on step 3 of a 10-step task often means the remaining steps proceed on a corrupted state
- Tool error handling is poor — most agent frameworks treat unexpected tool responses as data to reason over rather than stopping conditions
- **Indirect prompt injection is a structural vulnerability** — an agent reading an email, webpage, or document controlled by an attacker can have its instructions overridden mid-task. There is no reliable mitigation. [Greshake et al.](https://arxiv.org/abs/2302.12173)
- No standardized permission model — what an agent is and isn't allowed to do is expressed in natural language in a system prompt, not as an enforceable policy
- State recovery is essentially unsupported — if an agent takes a destructive action mid-task, there's usually no rollback

**Benchmarks:**
- [AgentBench](https://arxiv.org/abs/2308.03688) — Multi-task LLM-as-agent evaluation; even frontier models score poorly on real multi-step tasks
- [WebArena](https://arxiv.org/abs/2307.13854) — Realistic web navigation tasks; success rates remain low

**Status:** The tooling is improving (LangGraph checkpointing, better tool schemas) but the core reliability problem is unsolved. Most "production" agent deployments work in narrow, heavily constrained settings.

---

## 🔴 AI Security — Unpatched Attack Surface

**The problem:** AI security as a discipline is years behind traditional software security. Most deployed LLM applications are vulnerable to documented attack classes with no widely deployed mitigations.

**The specific gaps:**

- **Prompt injection has no reliable patch** — it's structural. LLMs cannot reliably distinguish between "trusted instructions from the system" and "instructions embedded in untrusted user data or external content." Sanitization doesn't work the way it does for SQL injection because the input and instruction channel are the same natural language channel.
- **Indirect prompt injection at scale** — Any LLM application that reads external content (emails, web pages, documents, database records) is potentially vulnerable. This includes most production RAG systems.
- **Supply chain backdoors** — Fine-tuned models can contain behavioral backdoors that survive safety training. [Sleeper Agents (Anthropic)](https://arxiv.org/abs/2401.05566) showed that models can be trained to behave normally until a specific trigger condition activates a hidden behavior — and standard safety fine-tuning does not remove it.
- **Model extraction** — Proprietary model weights can be partially reconstructed via query APIs with enough calls. No deployed API has a reliable defense against systematic extraction.
- **RAG poisoning** — Injecting content into a retrieval knowledge base that gets retrieved and fed to the LLM, steering outputs without touching the model itself.
- **No standardized disclosure process** — Traditional software has CVE, coordinated disclosure, and patch cycles. AI systems have none of this. Vulnerabilities are published without standard severity ratings, timelines, or vendor response expectations.

**References:**
- [OWASP LLM Top 10](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
- [MITRE ATLAS](https://atlas.mitre.org)
- [Garak — LLM vulnerability scanner](https://github.com/leondz/garak)

**Status:** The attack surface is growing faster than defenses. Prompt injection in particular has no clean fix on the horizon.

---

## 🔴 Compute Concentration & Access Inequality

**The problem:** Training frontier AI models requires infrastructure that only a handful of organizations can afford. This concentrates capability — and the risk that comes with it — in very few hands.

**The numbers:**

- Training a GPT-4 class model is estimated to cost $50–100M+ in compute alone
- The H100 GPU cluster needed to train at this scale is accessible only to companies with billions in capital or national-level investment
- Open-weight models (Llama, Mistral, DeepSeek) narrow the inference gap significantly — you can run capable models locally. But pretraining at frontier scale remains exclusive.
- DeepSeek's R1 demonstrated that training efficiency can be dramatically improved — but "dramatically improved" still means tens of millions of dollars

**The downstream effects:**

- Safety research is primarily conducted by the same organizations building the most powerful systems — a structural conflict of interest
- Nations without access to frontier compute become dependent on nations that do
- Regulatory responses are fragmented — EU AI Act, US executive orders, and no binding international framework

**Status:** Partially addressed by open-weight releases. The pretraining compute gap is not closing.

---

## 🔴 Evaluation — We Don't Know What We're Measuring

**The problem:** The benchmarks used to evaluate LLMs are increasingly saturated, contaminated with training data, and misaligned with the tasks we actually care about.

**The specific failure modes:**

- **Benchmark contamination** — Models are trained on data that overlaps with test sets. When a model scores high on MMLU, it's not clear how much is generalization vs. memorization.
- **Saturation** — Frontier models score 85–90%+ on benchmarks that were hard 2–3 years ago. New benchmarks get saturated within months of release.
- **Benchmark-to-reality gap** — High scores on HumanEval don't reliably predict performance on real codebases. High MMLU scores don't reliably predict professional task competence.
- **LLM-as-judge bias** — Using one LLM to evaluate another's outputs (common in MT-Bench style evals) inherits the evaluator's biases. Models grade favorably to outputs that resemble their own training.
- **Gaming** — Evaluation methodology is often public. There's incentive to optimize training for specific benchmarks rather than general capability.

**References:**
- [HELM (Stanford CRFM)](https://crfm.stanford.edu/helm/) — Holistic evaluation across multiple dimensions
- [BIG-Bench Hard](https://github.com/suzgunmirac/BIG-Bench-Hard) — Tasks that frontier models still consistently struggle with
- [TruthfulQA](https://github.com/sylinrl/TruthfulQA) — Hallucination-specific evaluation

**Status:** The field knows evaluation is broken. Efforts to build contamination-resistant, harder benchmarks are ongoing — but the economic incentive to perform well on existing benchmarks slows adoption of better ones.

---

## 🔴 Environmental Cost

**The problem:** Large-scale AI training and inference consumes significant energy and water. Reliable, standardized public data on this consumption is essentially nonexistent because no major AI lab discloses it consistently.

**What we know:**

- Training a frontier model is estimated to consume millions of kWh — comparable to the annual electricity usage of hundreds of homes
- Inference at scale (millions of API calls per day) accumulates to comparable or greater totals over time
- Data centers require substantial water for cooling — often in water-stressed regions
- Carbon intensity depends heavily on the energy grid mix at training locations — this is rarely disclosed

**What we don't know:**

- The actual training compute used by GPT-4, Gemini, Claude — none of these have published verified energy figures
- Whether efficiency gains from sparse models (MoE) and quantization are keeping pace with demand growth
- Long-term trajectory — model size is increasing, but so is inference volume

**Status:** No standardized carbon/energy reporting for AI exists. Research groups and nonprofits (MLCommons, etc.) are working on this, but adoption is voluntary and slow.

---

## Contributing to This Document

If you have a well-sourced addition, correction, or a new problem category worth tracking here — open a PR.

Requirements for this file specifically:
- Claims need sources — link papers, not blog posts where possible
- "The problem" section should be concrete, not abstract
- Status must be honest — don't describe active research as a solved problem

**→ [Back to README](README.md)**

<div align="center">
<sub>Part of <a href="README.md">AI Pulse</a> · Maintained by <a href="https://github.com/Sam161203">Sam</a></sub>
</div>
