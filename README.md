# Awesome-LLM-Reinforcement-Learning-RLHF

# Top LLM Reinforcement Learning (RLHF) Ecosystem

**Curated List of SaaS Products & Open-Source GitHub Projects**  
*Focused on Human Feedback Collection, Preference Optimization & Self-Hosted Alignment Frameworks*  
**Last updated: October 2026**

This repository tracks notable **SaaS platforms** and **open-source projects** for **LLM Reinforcement Learning from Human Feedback (RLHF)**. These tools enable organizations to align language models with human preferences—collecting high-quality feedback data, training reward models, and running RL algorithms like PPO and GRPO—transforming base models into helpful, harmless, and honest assistants.

**Examples** include Scale AI, Surge AI, Labelbox, Snorkel Flow, Appen, and Hugging Face TRL (the category leaders).

**Open-source emphasis**: This section is heavily expanded with every major active project for self-hosting, avoiding per-label vendor fees, and retaining full control over the alignment pipeline—ideal for research labs, enterprises with sensitive data, and teams that want to understand every step of the RLHF process. The open-source landscape is anchored by **Hugging Face TRL** (the most mature and widely adopted training library), **OpenRLHF** (the production-grade distributed framework with Ray and vLLM integration), **verl** (ByteDance's HybridFlow framework for reproducing reasoning-model recipes), and **Distilabel** (the synthetic data and AI feedback engine), with **Unsloth** and **Axolotl** providing memory-efficient fine-tuning that often precedes RLHF.

Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.

## Table of Contents
- [SaaS/Hosted Platforms](#saas-hosted-platforms)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

## SaaS/Hosted Platforms

- **[Surge AI](https://www.surge.ai/)**  
  **The RLHF data heavyweight and neutrality beneficiary.** Bootstrapped, low-profile, and reportedly out-earning Scale AI as early as 2024 with a fraction of the headcount . Became the default neutral choice for frontier-lab human feedback and evaluation data after Scale's Meta entanglement. Elite annotator pools, strong on nuanced text and preference data. Premium pricing, with computer vision not the center of gravity. Best for LLM labs buying RLHF, red-teaming, and eval data at quality-over-cost economics.

- **[Scale AI](https://scale.com/)**  
  **The former default, now a neutrality concern.** Meta invested a reported **$14.3 billion for a 49% stake** in June 2025, and Scale's founder left to lead Meta's superintelligence effort . Within days, Google and OpenAI were reported to be winding down work with the company. For any lab competing with Meta, Scale stopped being a neutral vendor. Still offers annotation, RLHF data, and evaluation services, but the strategic risk is significant. Best for organizations not competing directly with Meta that value Scale's scale and existing integrations.

- **[Labelbox](https://labelbox.com/)**  
  **The annotation platform pivoting to RL environments.** Now sells four things: **Horizon** (RL environments and preference signal), **Terra** (robotics data), **Alignerr** (2.6M+ knowledge expert network), and **Recursion** (enterprise RL platform for specialist agents) . The classic annotation tool still exists but is no longer the headline product. **Caveat**: the public pricing page is gone, making the platform a moving target with opaque cost . Best for teams wanting an established platform leaning into evals and RL-era data.

- **[Snorkel Flow](https://snorkel.ai/)**  
  **The programmatic labeling alternative.** Takes a different approach from human-workforce vendors—uses weak supervision and programmatic labeling to generate training data without manual annotation at scale . Best for organizations with domain expertise that want to encode labeling logic rather than pay per label.

- **[Appen](https://appen.com/)**  
  **The multilingual reach veteran.** One of the industry's oldest names, with a global crowd spanning hundreds of languages and dialects. After difficult years, refocused on LLM data services and remains hard to beat when a dataset needs authentic coverage across dozens of locales, especially in speech and search relevance . Best for multilingual text, speech, and relevance data at serious breadth.

- **[Toloka](https://toloka.ai/)**  
  Global crowd-sourced data platform with expertise in RLHF, evaluation, and multilingual data collection. Best for organizations needing cost-effective human feedback at scale across diverse geographies.

- **[iMerit](https://imerit.net/)**  
  Veteran managed-services provider with deep benches in computer vision, geospatial, medical, and autonomous-vehicle data, plus its own Ango Hub platform. Full-time trained annotators rather than crowds . Best for long-running, high-volume CV and AV programs needing process maturity.

## Open-Source GitHub Projects

- **[Hugging Face TRL](https://github.com/huggingface/trl)**  
  **The most mature and widely adopted RLHF training library.** 18K+ GitHub stars, 17.5K+ updated weekly . **Ecosystem position**: TRL is the official implementation standard for post-training in the Hugging Face ecosystem, with seamless integration into `transformers`, `accelerate`, and `peft` . **Algorithm coverage**: SFT, DPO, IPO, KTO, GRPO, BCO, and PPO via `PPOTrainer`. **GRPOTrainer** (v0.17.0+) removes the critic model and significantly reduces VRAM, making it the preferred algorithm for reproducing reasoning models like DeepSeek-R1 . **Strengths**: clean `Trainer` APIs, excellent documentation, and the lowest barrier to entry for researchers and educators. **Limitations**: default `generate()` is not system-optimized for large-scale distributed training; single-node efficiency is good but multi-node scaling lags behind OpenRLHF and verl . Best for algorithm researchers, educators, and teams with limited compute (single-node or single-GPU) validating new reward functions or training models under 30B.

- **[OpenRLHF](https://github.com/OpenRLHF/OpenRLHF)**  
  **The production-grade distributed framework.** 9K+ GitHub stars, updated weekly . **Architecture**: Ray-based distributed computing with **vLLM for inference acceleration** and DeepSpeed ZeRO for memory efficiency. The PPO's four models (Actor, Critic, Reward, Reference) are physically separated onto different GPU resource groups—eliminating the monolithic architecture's shortcomings . **Key innovation**: first framework to integrate vLLM into the RLHF training loop, using PagedAttention and tensor parallelism for multi-fold generation throughput improvement . **Algorithm support**: PPO, DAPO, REINFORCE++, RLOO, and rejection sampling. **Token-level pipeline** supports multi-turn agentic training without distribution shift . **Adoption**: integrated into CMU's Advanced NLP course (Spring 2025), used by Google, ByteDance, Baidu, NVIDIA, Tencent, and UC Berkeley's Starling Team . **Limitations**: language models only (no multimodal support); dependencies on Ray, vLLM, and DeepSpeed introduce upstream compatibility maintenance . Best for production deployments and teams training 70B+ models or running agentic RL at scale.

- **[verl (Volcano Engine RL)](https://github.com/volcengine/verl)**  
  **ByteDance's HybridFlow framework.** 19K+ GitHub stars, updated weekly . **Positioning**: the de-facto framework people use to **reproduce DeepSeek-R1 and Qwen-style GRPO/DAPO/GSPO recipes** . **Architecture**: HybridFlow design with strong multi-node scaling; powerful but architecturally dense (Ray + multiple backends) . **Learnability**: medium-low—more complex than TRL but more scalable than single-node approaches. Best for teams reproducing frontier reasoning-model recipes and organizations with dedicated infrastructure engineers.

- **[Distilabel](https://github.com/argilla-io/distilabel)**  
  **The synthetic data and AI feedback engine.** The industry standard for creating high-quality datasets for fine-tuning frontier models . **Function**: builds complex pipelines leveraging LLMs to generate, augment, and filter datasets, incorporating "LLM-as-a-judge" patterns for quality assurance . **Key use case**: creating **preference datasets for DPO and RLHF workflows**—generating multiple responses to the same prompt and using a stronger model to rank them . **Strengths**: provider-agnostic (Anthropic, OpenAI, vLLM, Ollama), reliable pipeline logic (retries, rate limiting, caching), and rich component library (UltraFeedback, Evol-Instruct, DEITA) . **Limitations**: generating large datasets via frontier APIs can be expensive; synthetic data inherits generator model biases . Best for teams that need to scale from hundreds to tens of thousands of high-quality training examples before running RLHF.

- **[Unsloth](https://github.com/unslothai/unsloth)**  
  **The memory-efficient fine-tuning precursor.** Dominant memory-efficient finetuning library with **2–5x speedups and 50–70% memory savings** versus naive Hugging Face Trainer . **Benchmark**: 7B model QLoRA on RTX 4090 uses 11GB VRAM at 3,400 tokens/sec vs. baseline 18GB at 1,200 tokens/sec . **Role in RLHF**: typically used for the SFT stage or for memory-constrained DPO/GRPO training before full RLHF. **Limitations**: single-GPU focus; multi-GPU support is partial. Best for teams fine-tuning on consumer hardware (24GB or less) who need maximum speed and minimum VRAM.

- **[Axolotl](https://github.com/axolotl-ai-cloud/axolotl)**  
  **The production finetuning framework for community releases.** Dominant YAML-config-driven framework with extensive hardware support and every training method (DPO, RLHF, ORPO, KTO) . **Strengths**: multi-GPU via DeepSpeed/FSDP, config-as-artifact for reproducibility. **Trade-offs**: slower than Unsloth on single GPU (1,500 vs. 3,400 tokens/sec) . Best for production-grade training and research where the config is the deliverable.

### Additional Strong Open-Source Options

- **LLaMA-Factory** — Broadest feature set with a web UI (LLaMA Board), supporting 100+ models and training methods including DPO, PPO, KTO, ORPO . Best for non-expert users and teams wanting a single tool for training, evaluation, and export.
- **Open-Instruct** — Allen AI's framework for instruction tuning and RLHF. Best for research teams wanting a reference implementation aligned with academic best practices .
- **Frameworks for building custom systems**: Use **TRL + Unsloth** for pedagogical experiments and single-GPU work. Use **OpenRLHF** for production-scale training with vLLM acceleration. Use **verl** to reproduce frontier reasoning-model recipes. Use **Distilabel** to generate preference data before training. Pair **Axolotl** for production SFT/DPO and **LLaMA-Factory** when a web UI is needed.

## How to Contribute

1. Fork the repo.
2. Add/edit entries in `README.md` (follow existing format).
3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.
4. Submit PR with a short explanation.

Star the repo if you find it useful!

## Disclaimer

- This is a **community-curated** list — not exhaustive and not an endorsement.
- **Vendor neutrality is now a strategic concern**: Scale AI's Meta investment ($14.3B for 49%) and the subsequent exodus of Google and OpenAI make it a risky choice for labs competing with Meta . Surge AI emerged as the primary neutral alternative.
- **Framework choice depends on scale and expertise**: TRL for learning and small-scale experiments; OpenRLHF for production with vLLM; verl for reproducing frontier recipes. There is no single "best" framework—the right choice depends on your team's infrastructure skills and model size .
- **Data quality dominates algorithm choice**: Distilabel and human feedback vendors address the upstream bottleneck. No RL algorithm can compensate for poor preference data.
- **SaaS RLHF vendors charge premium prices**: Surge AI and Labelbox operate at quality-over-cost economics. Evaluate whether in-house annotation or programmatic labeling (Snorkel) is viable before committing to managed services.

---

**Made for ML researchers, alignment engineers, and organizations building aligned language models.**  
Let's make LLM reinforcement learning more open, scalable, and understandable.
