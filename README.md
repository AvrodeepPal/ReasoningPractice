# 🧩 Reasoning Practice: RL Foundations, Test-Time Compute & DeepSeek Architecture

[![Reinforcement Learning](https://img.shields.io/badge/RL-Policy%20Gradients-blue.svg)](https://www.google.com/search?q=Sutton+Barto+Reinforcement+Learning)
[![DeepSeek](https://img.shields.io/badge/DeepSeek-R1%20%7C%20V3-purple.svg)](https://github.com/deepseek-ai)
[![vLLM](https://img.shields.io/badge/Serving-vLLM-orange.svg)](https://github.com/vllm-project/vllm)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

> A research-paper library and set of handwritten notes tracing how modern LLMs learn to *reason*: from the reinforcement learning foundations that make chain-of-thought and RLHF possible, through test-time compute scaling, to the DeepSeek family of models that popularized large-scale RL-trained reasoning and the inference infrastructure (vLLM) that serves it efficiently.

---

## 📌 Table of Contents

- [🔬 Overview](#-overview)
- [🗂️ Directory Blueprint](#️-directory-blueprint)
- [🎯 Reinforcement Learning Foundations (`Reasoning/`)](#-reinforcement-learning-foundations-reasoning)
- [🐋 DeepSeek Architecture & Serving (`DeepSeek/`)](#-deepseek-architecture--serving-deepseek)
- [👤 Author](#-author)

---

## 🔬 Overview

Reasoning in modern LLMs isn't a single technique — it's the layering of three ideas:

1. **Classical RL** — value functions, policy gradients, and trust-region optimization, the machinery underneath RLHF and RL-from-verifiable-rewards.
2. **Prompting & test-time compute** — chain-of-thought elicits latent reasoning without any weight updates; scaling *inference-time* compute can outperform scaling parameters.
3. **DeepSeek's reasoning models** — R1 and V3 operationalize RL-trained reasoning at scale, and this repo tracks the surrounding serving stack (vLLM, PagedAttention-style memory management) needed to run them efficiently.

This repo is a literature + notes archive, not a codebase — it exists to keep the papers and the handwritten synthesis of them in one place.

---

## 🗂️ Directory Blueprint

```
reasoningpractice/
├── DeepSeek/                                          # DeepSeek model family & serving
│   ├── DeepSeek_R1.pdf                                # Reasoning model trained via large-scale RL
│   ├── DeepSeek_V3.pdf                                # MoE base model architecture & training report
│   ├── DeepSeek_V4.pdf                                # Latest generation architecture notes
│   ├── DeepSeek_ConditionalMemoryviaScalableLookup.pdf# Conditional/sparse memory via scalable lookup
│   └── Deepseek + vLLM.pdf                            # Handwritten notes: serving DeepSeek models on vLLM
│
├── Reasoning/                                         # RL & reasoning foundations
│   ├── Reinforcement Learning - Richard Sutton.pdf    # Sutton & Barto — the RL reference text
│   ├── Policy Gradient Methods for RL with Function Approximation.pdf  # Sutton et al. (1999/2000)
│   ├── Trust Region Policy Optimization.pdf           # Schulman et al. (2015) — TRPO
│   ├── Chain-of-Thought Prompting Elicits Reasoning in LLMs.pdf        # Wei et al. (2022)
│   ├── Scaling LLM Test-Time Compute Optimally...pdf  # Snell et al. — inference-time scaling vs. parameter scaling
│   └── The HARPY Speech Recognition System.pdf        # Early search-based reasoning/decoding system (historical reference)
│
└── Deepseek + vLLM.pdf                                # Root copy of the DeepSeek/vLLM serving notes
```

---

## 🎯 Reinforcement Learning Foundations (`Reasoning/`)

| Paper / Text | Key Contribution to Reasoning in LLMs |
| :--- | :--- |
| **Reinforcement Learning: An Introduction** *(Sutton & Barto)* | The canonical RL text — MDPs, value functions, TD learning, and policy-based methods underlying every modern RLHF/RLVR pipeline. |
| **Policy Gradient Methods for RL with Function Approximation** *(Sutton et al.)* | Establishes the policy gradient theorem — the mathematical basis for directly optimizing a stochastic policy, precursor to PPO/GRPO used in LLM post-training. |
| **Trust Region Policy Optimization** *(Schulman et al., 2015)* | Constrains policy updates within a trust region to guarantee monotonic improvement — the conceptual ancestor of PPO, the workhorse of RLHF. |
| **Chain-of-Thought Prompting Elicits Reasoning in Large Language Models** *(Wei et al., 2022)* | Shows that prompting a model to produce intermediate reasoning steps substantially improves performance on multi-step tasks — no training required. |
| **Scaling LLM Test-Time Compute Optimally Can Be More Effective Than Scaling Model Parameters** | Demonstrates that, under a fixed compute budget, spending it at *inference time* (more reasoning steps, search, verification) can beat spending it on more parameters — the thesis underpinning R1-style reasoning models. |
| **The HARPY Speech Recognition System** | Historical CMU system using a search-based/beam-decoding approach — included as an early precedent for structured, multi-hypothesis decoding. |

---

## 🐋 DeepSeek Architecture & Serving (`DeepSeek/`)

| Paper / Notes | Key Contribution |
| :--- | :--- |
| **DeepSeek-R1** | Trains reasoning capability directly via large-scale reinforcement learning (RL-from-verifiable-rewards), largely bypassing supervised chain-of-thought data. |
| **DeepSeek-V3** | Mixture-of-Experts base model — architecture, training infrastructure, and efficiency techniques (MLA, auxiliary-loss-free load balancing). |
| **DeepSeek-V4** | Notes on the next-generation architecture. |
| **Conditional Memory via Scalable Lookup** | Sparse/conditional memory mechanisms relevant to scaling model capacity without proportional compute cost. |
| **Deepseek + vLLM (handwritten notes)** | How DeepSeek's MoE and MLA architecture maps onto vLLM's serving engine — KV-cache memory management (PagedAttention), batching, and throughput considerations when self-hosting reasoning models. |

---

## 👤 Author

**Avrodeep Pal**
- GitHub: [@AvrodeepPal](https://github.com/AvrodeepPal)
- Collaboration: Open issues, discussions, or pull requests are warmly welcomed!

⭐ *If you find this repository useful, feel free to star it.*
