# Inference Engineering Syntopicon

*As of 7 October 2026.*

A syntopical index of inference engineering, organised by 14 enduring tensions rather than by technique, with specific loci (sections, figures, chapters) for each reference.

## Contents

- [Inference Engineering Syntopicon](#inference-engineering-syntopicon)
  - [Contents](#contents)
  - [Purpose and design](#purpose-and-design)
  - [How to use it](#how-to-use-it)
  - [The canon](#the-canon)
    - [Spine texts](#spine-texts)
    - [Foundational books](#foundational-books)
    - [Additional readings](#additional-readings)
  - [The 14 Great Ideas](#the-14-great-ideas)
    - [1. Memory vs. compute (arithmetic intensity)](#1-memory-vs-compute-arithmetic-intensity)
    - [2. Prefill vs. decode](#2-prefill-vs-decode)
    - [3. The KV cache (state)](#3-the-kv-cache-state)
    - [4. Batching and scheduling](#4-batching-and-scheduling)
    - [5. Precision and quantization](#5-precision-and-quantization)
    - [6. Speculation](#6-speculation)
    - [7. Parallelism and communication](#7-parallelism-and-communication)
    - [8. Conditional computation (MoE, sparsity)](#8-conditional-computation-moe-sparsity)
    - [9. Kernels and compilation](#9-kernels-and-compilation)
    - [10. Disaggregation and system architecture](#10-disaggregation-and-system-architecture)
    - [11. Measurement and SLOs](#11-measurement-and-slos)
    - [12. Determinism and fidelity](#12-determinism-and-fidelity)
    - [13. Economics](#13-economics)
    - [14. Trust and security of inference](#14-trust-and-security-of-inference)
  - [Lexicon: bringing the authors to terms](#lexicon-bringing-the-authors-to-terms)
  - [Tracker, caveats and maintenance](#tracker-caveats-and-maintenance)
  - [Sources](#sources)

---

## Purpose and design

This syntopicon indexes inference engineering by 14 enduring tensions, not by technique, so it survives the field's 12–18 month technique churn. Techniques (PagedAttention, EAGLE, FP4) appear only as positions taken on those tensions.

Inspired by Adler's *Syntopicon* (1952), keeping the five parts of each Great Idea:

- introductory essay,
- outline of topics,
- references to specific loci,
- cross-references, and
- additional readings.

It adds three fields a *fast-moving* engineering field needs:

- **Hardware era** — Ampere, Hopper, Blackwell; findings often do not transfer across generations.
- **Superseded by** — the later work that displaces a reference.
- **Reconstruction exercise** — something to derive or rebuild, not just read.

| Organising approach | Pros | Cons |
| --- | --- | --- |
| By idea / tension (used here) | Durable; surfaces disagreements, which interviews probe | Harder to build; tensions must be named by you |
| By stack layer (Kiely's runtime / infrastructure / tooling) | Matches industry vocabulary | Fragments cross-cutting ideas such as memory vs compute |
| By technique | Fast to build; maps to job ads | Ages fastest; hides why techniques compete |

Each reference below also carries a stack-layer tag, which keeps the benefit of the second approach.

## How to use it

Read per idea, not per source: gather every locus on one idea, then write that idea's introductory essay. This follows Adler and Van Doren's five steps of syntopical reading (*How to Read a Book*, 1972, Part Four), adapted:

1. **Find the relevant passages** — use the loci listed per idea; never read a paper cover to cover on first pass.
2. **Bring the authors to terms** — normalise vocabulary using the [Lexicon](#lexicon-bringing-the-authors-to-terms); most apparent disagreements are definitional.
3. **Frame neutral questions** — the *Question* line under each idea.
4. **Define the issues** — which sources take which side (the *Controversy* line).
5. **Analyse the discussion** — write a one-page essay per idea stating the tension, the positions, the evidence type, and the conditions under which each side wins.

Recommended order, weighted for an inference performance and deployment role:

1. Memory vs compute (1)
2. Prefill vs decode (2)
3. The KV cache (3)
4. Batching and scheduling (4)
5. Measurement and SLOs (11)
6. Precision and quantization (5)
7. Speculation (6)
8. Disaggregation (10)
9. Parallelism (7) and conditional computation (8)
10. Kernels and compilation (9), alongside C++/CUDA practice
11. Determinism (12) and economics (13)
12. Trust and security of inference (14)

## The canon

Three spine texts carry the field; five foundational books carry the disciplines beneath it. Loci marked "verify" should be checked against your edition.

### Spine texts

| Work | Loci to read | Role | Caveat |
| --- | --- | --- | --- |
| [Kiely, *Inference Engineering* (Baseten Books, 2026)](https://www.baseten.co/inference-engineering/) | Ch. 0 (three layers: runtime, infrastructure, tooling); Ch. 6 Modalities; Ch. 7 Production; App. A glossary; App. B further reading | The field's map and first textbook; free online | Vendor-authored; frames problems platforms solve |
| [Austin et al., *How to Scale Your Model* (Google DeepMind, 2025)](https://jax-ml.github.io/scaling-book/) | Chapters "Rooflines", "All About Transformer Inference", "Serving LLaMA 3-70B" | First-principles performance derivation; free online | TPU-centric; translate to GPU |
| Huyen, *AI Engineering* (O'Reilly, 2025) | Ch. 9 "Inference Optimization" | Application-layer survey | Too shallow to be the spine |

### Foundational books

| Work | Loci to read | Feeds ideas |
| --- | --- | --- |
| Hennessy & Patterson, *Computer Architecture: A Quantitative Approach*, 6th ed. | Ch. 2 memory hierarchy; Ch. 4 data-level parallelism and GPUs; Ch. 7 domain-specific architectures (TPU case study) | 1, 9 |
| Hwu, Kirk & El Hajj, *Programming Massively Parallel Processors*, 4th ed. (2022) | Chs. 4–6: compute architecture, memory and data locality, performance considerations | 1, 9 |
| Harchol-Balter, *Performance Modeling and Design of Computer Systems* (CUP, 2013) | Little's Law chapter; M/G/1 scheduling part incl. SRPT (verify chapter numbers) | 4, 11 |
| Kleppmann, *Designing Data-Intensive Applications* | Ch. 1, section on describing performance (percentiles) | 11 |
| Gregg, *Systems Performance*, 2nd ed. (2020) | Ch. 2 Methodologies (USE method) | 11 |

### Additional readings

- Dean & Barroso, "The Tail at Scale", *CACM* 2013 — tail latency.
- Horace He, "Making Deep Learning Go Brrrr From First Principles" (2022 blog) — compute / memory / overhead triad.
- Stas Bekman, *Machine Learning Engineering Open Book* — inference chapter.
- [Kiely, Appendix B — diff it against this canon; gaps in either direction are informative.](https://github.com/stas00/ml-engineering)

## The 14 Great Ideas

Each idea gives: the neutral question, the loci, the live controversy, cross-references, and a reconstruction exercise. Stack-layer tags: **[R]** runtime, **[I]** infrastructure, **[T]** tooling, **[HW]** hardware.

### 1. Memory vs. compute (arithmetic intensity)

**Question:** Is this operation bound by FLOPs, memory bandwidth, or overhead?

**Loci:**

- Williams, Waterman & Patterson, "Roofline: An Insightful Visual Performance Model for Multicore Architectures", *CACM* 52(4), 2009 — definition of operational intensity; Fig. 1. [HW]
- Horace He, "Making Deep Learning Go Brrrr From First Principles" (2022) — the three regimes. [R]
- *How to Scale Your Model* — "Rooflines" chapter. [HW]
- Hennessy & Patterson Ch. 2; PMPP Ch. 5. [HW]

**Controversy:** Is a roofline enough once communication and kernel-launch overhead dominate small batches?

**Cross-refs:** 2, 4, 9.

**Reconstruct:** By hand, derive decode-step latency for a 70B dense model on one H100 at batch 1 and batch 64; find the batch size where decode turns compute-bound.

### 2. Prefill vs. decode

**Question:** Generation has two phases with opposite bottlenecks — compute-bound prefill, memory-bound decode. Should they share hardware?

**Loci:**

- Pope et al., "Efficiently Scaling Transformer Inference", MLSys 2023 (arXiv 2211.05102) — §2 inference cost trade-offs. [R]
- Kiely, Ch. 0. [R]

**Controversy:** Resolved in practice by idea 4 (chunked prefill) or idea 10 (disaggregation); which wins depends on workload mix.

**Cross-refs:** 4, 10, 11.

**Reconstruct:** Profile a small model in vLLM; plot time per step against prompt length and against batch size separately.

### 3. The KV cache (state)

**Question:** How is attention state stored, shared, compressed and evicted — and who owns the problem, model designers or serving engineers?

**Loci:**

- Shazeer, "Fast Transformer Decoding: One Write-Head is All You Need" (2019) — multi-query attention.
- Ainslie et al., "GQA", EMNLP 2023.
- DeepSeek-V2 technical report (2024) — §2.1 multi-head latent attention.
- Kwon et al., "Efficient Memory Management for LLM Serving with PagedAttention", SOSP 2023 — §3 memory challenges, §4 method. [R]
- Zheng et al., SGLang, NeurIPS 2024 — RadixAttention prefix sharing. [R]
- Xiao et al., StreamingLLM, ICLR 2024 — attention sinks.
- Zhang et al., H2O, NeurIPS 2023 — heavy-hitter eviction.
- Liu et al., KIVI (2024) — KV-cache quantisation.

**Controversy:** Architectural fixes (MQA, GQA, MLA) vs serving-time fixes (eviction, quantisation). Eviction methods often look fine on perplexity and fail on long-context retrieval.

**Cross-refs:** 5, 10, 14 (prefix caching as side channel).

**Reconstruct:** Build a paged KV allocator with a block table and copy-on-write prefix sharing in about 200 lines of Python.

### 4. Batching and scheduling

**Question:** How is aggregate throughput traded against each user's latency?

**Loci:**

- Yu et al., "Orca", OSDI 2022 — iteration-level scheduling, selective batching. [R]
- Agrawal et al., "Sarathi-Serve", OSDI 2024 — chunked prefill, stall-free batching. [R]
- Harchol-Balter — SRPT and M/G/1 scheduling (verify chapter).

**Controversy:** Fairness vs goodput; schedulers that rely on predicted output length are fragile when predictions are wrong.

**Cross-refs:** 2, 11.

**Reconstruct:** Discrete-event simulator comparing static vs continuous batching under Poisson arrivals; report p50/p99 TTFT and goodput.

### 5. Precision and quantization

**Question:** How much fidelity can be given up, in which tensors, and how would you know?

**Loci:**

- Dettmers et al., "LLM.int8()", NeurIPS 2022 — emergent outlier features.
- Frantar et al., "GPTQ", ICLR 2023 — second-order weight quantisation.
- Xiao et al., "SmoothQuant", ICML 2023 — migrating difficulty from activations to weights.
- Lin et al., "AWQ", MLSys 2024 — activation-aware weight protection.
- Micikevicius et al., "FP8 Formats for Deep Learning" (2022). [HW]
- Rouhani et al., "Microscaling Data Formats for Deep Learning" (2023). [HW]
- Dettmers & Zettlemoyer, "The case for 4-bit precision: k-bit Inference Scaling Laws", ICML 2023.

**Controversy:** Perplexity and headline benchmarks hide task-level degradation (long context, code, reasoning). This is the field's most contested measurement question.

**Cross-refs:** 3, 12, 13.

**Reconstruct:** Quantise one model with GPTQ and AWQ; compare perplexity against a task eval you choose; record where they diverge.

### 6. Speculation

**Question:** Can latency be bought by guessing tokens and verifying them in parallel, without changing the output distribution?

**Loci:**

- Leviathan, Kalman & Matias, "Fast Inference from Transformers via Speculative Decoding", ICML 2023.
- Chen et al., "Accelerating Large Language Model Decoding with Speculative Sampling" (DeepMind, 2023) — proof of distribution preservation.
- Cai et al., "Medusa" (2024) — multiple decoding heads.
- Li et al., "EAGLE" (2024) and "EAGLE-3" (2025) — feature-level drafting.

**Controversy:** Gains shrink at large batch because decode stops being memory-bound; later work argues gains return for long contexts. Be able to state when speculation helps.

**Cross-refs:** 1, 4, 14 (acceptance-rate leakage).

**Reconstruct:** Implement speculative sampling with a small draft model; verify empirically that output token frequencies match the target model.

### 7. Parallelism and communication

**Question:** How is one model split across many devices without communication eating the gains?

**Loci:**

- Shoeybi et al., "Megatron-LM" (2019) — §3 tensor-parallel transformer layers. [I]
- Pope et al. (MLSys 2023) — §3 partitioning layouts for feedforward and attention. [I]
- DeepSeek-V3 technical report (2024) — "Inference and Deployment" section: expert parallelism, separate prefill and decode configurations. [I]
- *How to Scale Your Model* — "Serving LLaMA 3-70B" chapter. [I]

**Controversy:** Tensor parallelism minimises latency but scales poorly across nodes; pipeline and expert parallelism trade latency for throughput.

**Cross-refs:** 8, 10.

**Reconstruct:** Compute all-reduce volume per token for tensor parallelism of degree 2, 4, 8 on a 70B model; compare to NVLink and InfiniBand bandwidth.

### 8. Conditional computation (MoE, sparsity)

**Question:** Activating fewer parameters cuts FLOPs. Does it cut serving cost when every expert's weights must still be resident and fed?

**Loci:**

- Fedus et al., "Switch Transformers", JMLR 2022 — routing and capacity factor.
- Rajbhandari et al., "DeepSpeed-MoE", ICML 2022 — MoE inference system design. [R]
- DeepSeek-V3 technical report — "Inference and Deployment" section (expert load balancing, redundant experts). [I]
- Frantar & Alistarh, "SparseGPT" (2023); Sun et al., "Wanda" (2023) — one-shot pruning.

**Controversy:** MoE is cheap per token at scale but memory-heavy and awkward at small batch; unstructured sparsity rarely yields wall-clock speedup on GPUs.

**Cross-refs:** 1, 7, 13.

**Reconstruct:** For an MoE model of your choice, compute bytes moved per decode step at batch 1 vs batch 256, accounting for expert activation probability.

### 9. Kernels and compilation

**Question:** Where should the abstraction boundary sit: hand-written kernels, DSLs like Triton, or graph compilers?

**Loci:**

- Dao et al., "FlashAttention", NeurIPS 2022 — §3 tiling and recomputation, IO-complexity analysis. [R]
- Dao, "FlashAttention-2" (2023); Shah et al., "FlashAttention-3" (2024) — Hopper asynchrony, FP8. [HW]
- Dao et al., "Flash-Decoding for long-context inference" (2023 blog) — split-KV parallelism for decode.
- Tillet, Kung & Cox, "Triton", MAPL 2019. [T]
- Chen et al., "TVM", OSDI 2018. [T]
- Ansel et al., "PyTorch 2", ASPLOS 2024 — TorchDynamo and TorchInductor. [T]
- PMPP Chs. 4–6. [HW]

**Controversy:** Compilers promise portability; frontier performance on each new GPU generation still comes from hand-tuned kernels for months.

**Cross-refs:** 1, 5, 12.

**Reconstruct:** Write tiled attention in Triton, then in CUDA; measure each against PyTorch's scaled dot-product attention.

### 10. Disaggregation and system architecture

**Question:** Should prefill and decode run on separate pools of machines, joined by a KV-cache transfer layer?

**Loci:**

- Zhong et al., "DistServe", OSDI 2024 — goodput-optimal disaggregation. [I]
- Patel et al., "Splitwise", ISCA 2024 — phase splitting across heterogeneous hardware. [I]
- Qin et al., "Mooncake", FAST 2025 — KV-cache-centric architecture. [I]
- Agrawal et al., "Sarathi-Serve", OSDI 2024 — the co-location counter-position. [R]

**Controversy:** The clearest live debate in the field: disaggregation vs co-location with chunked prefill. Read DistServe and Sarathi-Serve side by side.

**Cross-refs:** 2, 3, 4, 7.

**Reconstruct:** Extend the idea-4 simulator with a disaggregated mode and KV transfer cost; find the crossover workload.

### 11. Measurement and SLOs

**Question:** What does "fast" mean, and for whom?

**Loci:**

- Reddi et al., "MLPerf Inference Benchmark", ISCA 2020 — scenarios (single-stream, server, offline). [T]
- Dean & Barroso, "The Tail at Scale", *CACM* 2013.
- Kleppmann, DDIA Ch. 1 — percentiles.
- Gregg, *Systems Performance* Ch. 2 — USE method.
- Harchol-Balter — Little's Law.

**Controversy:** Vendor benchmarks pick favourable scenarios; goodput under a stated SLO is the only fair comparison.

**Cross-refs:** all ideas; see [Lexicon](#lexicon-bringing-the-authors-to-terms).

**Reconstruct:** Benchmark one engine at three load levels; report TTFT and TPOT at p50 and p99, plus goodput for a stated SLO.

### 12. Determinism and fidelity

**Question:** Is the served model actually the model you think you are serving?

**Loci:**

- Horace He and Thinking Machines Lab, "Defeating Nondeterminism in LLM Inference" (Sept 2025) — batch invariance as the root cause.

**Controversy:** Batch-invariant kernels cost throughput; how much determinism is worth paying for?

**Cross-refs:** 4, 5, 9, 14.

**Reconstruct:** Send the same prompt at temperature 0 under varying concurrent load; measure output divergence.

### 13. Economics

**Question:** What is the cost per useful token, and how should model size trade against inference spend?

**Loci:**

- Sardana et al., "Beyond Chinchilla-Optimal: Accounting for Inference in Language Model Scaling Laws", ICML 2024.
- Snell et al., "Scaling LLM Test-Time Compute Optimally can be More Effective than Scaling Model Parameters" (2024).
- Samsi et al., "From Words to Watts", IEEE HPEC 2023 — energy per token.
- Kiely, Ch. 7 Production. [I]

**Controversy:** Test-time compute shifts cost from training to inference; whether that is cheaper depends on query volume.

**Cross-refs:** 5, 8, 11.

**Reconstruct:** Build a cost model: dollars per million output tokens for a 70B model on H100 at three batch sizes, from GPU hourly price and measured throughput.

### 14. Trust and security of inference

**Question:** What do serving optimisations leak, and can inference be verified?

**Loci:**

- Trail of Bits, "LeftoverLocals" (Jan 2024, CVE-2023-4969) — GPU local memory leaking across processes. [HW]
- Gu et al., "Auditing Prompt Caching in Language Model APIs" (2025) — cache timing as a side channel. [R]
- Carlini et al., "Stealing Part of a Production Language Model", ICML 2024 — API-level extraction.
- Side-channel work on speculative decoding (2024–25 preprints; verify titles). [R]
- Sun, Li & Zhang, "zkLLM", ACM CCS 2024 — zero-knowledge proofs of LLM inference.
- Ong et al., "TOPLOC" (Prime Intellect, 2025) — locality-sensitive hashing for verifiable inference.

**Controversy:** Every performance trick creates a surface — prefix caching enables timing attacks, speculation leaks data-dependent acceptance rates, batching breaks the determinism verification relies on. Few inference engineers read this cluster.

**Cross-refs:** 3, 6, 12.

**Reconstruct:** Against a local vLLM instance with prefix caching on, measure whether TTFT distinguishes a cached from an uncached prompt prefix.

## Lexicon: bringing the authors to terms

Papers use these terms inconsistently; normalise to this column before comparing results. Check each paper's own definition and note deviations in the tracker.

| Term | Working definition | Common confusion |
| --- | --- | --- |
| TTFT | Time from request arrival to first output token, including queueing | Some papers exclude queue time, flattering results |
| TPOT | Mean time per output token after the first | Often conflated with ITL |
| ITL | Time between consecutive output tokens, as a distribution | Means hide stalls caused by prefill interference |
| E2E latency | Network + queue + prefill + all decode steps | Benchmarks often report engine time only |
| Throughput | Tokens per second across all requests | Input vs output tokens, per GPU vs per node — always state which |
| Goodput | Throughput counting only requests that meet the stated SLO | Meaningless without the SLO thresholds |
| Arithmetic intensity | FLOPs per byte moved from memory | Per-operator vs per-step values differ greatly |
| MFU / MBU | Model FLOPs / bandwidth utilisation against hardware peak | Peak figures for sparse or FP8 inflate the denominator |
| Acceptance rate | Fraction of draft tokens accepted in speculation | Per-token vs mean accepted length per step |
| Fidelity | Agreement of optimised outputs with the reference model | Perplexity vs task accuracy vs token-level match |

## Tracker, caveats and maintenance

Record every reading in a tracker with one row per locus, not per source:

| Column | Contents |
| --- | --- |
| Idea | 1–14 |
| Topic | Sub-question within the idea |
| Source | Full citation with link |
| Locus | Section, figure or page |
| Position | What the source claims on the idea's question |
| Evidence type | Vendor-measured, independent replication, analytical, anecdotal |
| Hardware era | Ampere, Hopper, Blackwell, TPU |
| Stack layer | Runtime, infrastructure, tooling, hardware |
| Superseded by | Later work that displaces it |
| Reconstruction | Exercise and status |

**Caveats:**

- The canon is mostly conference papers with vendor-run benchmarks. Without the evidence-type column the syntopicon encodes marketing.
- Paper-level citations here are reliable; section numbers in recent technical reports and the security preprints are marked "verify" or should be checked on first read.
- Adler's *Syntopicon* was criticised as obsolete on arrival. Avoid the same fate by reviewing "Superseded by" quarterly and rewriting an idea's essay when its controversy resolves.

**Maintenance cadence:** quarterly sweep of OSDI, SOSP, MLSys, ISCA, ASPLOS, FAST and NeurIPS systems tracks, plus engine release notes (vLLM, SGLang, TensorRT-LLM); add new loci only where they take a new position on an existing idea.

## Sources

- [Inference Engineering — Baseten](https://www.baseten.co/inference-engineering/)
- [Inference Engineering book overview](https://www.beri.net/learning/baseten-inference-engineering-book)
