# 8-Week Learning Plan: Foundations of AI Evaluation & RAG Reliability

**Time commitment:** 10–12 hours/week
**Total:** approximately 80–96 hours
**Practical objective:** Build a small, reproducible **RAG Evaluation Laboratory inside Corpus Studio**.

## Phase 1 North Star

By the end of Week 8, you will have a reproducible experiment that answers:

> **How do different chunking strategies affect retrieval performance and answer quality for the same corpus, queries, embedding model, and LLM configuration?**

The final laboratory should allow you to:

* ingest a controlled corpus;
* generate multiple chunking configurations;
* create embeddings and vector indexes;
* run a fixed evaluation dataset;
* measure retrieval quality;
* evaluate answer quality;
* inspect failures;
* compare experiments;
* detect regressions;
* reproduce results from recorded configurations.

---

# 1. Operating Principles

This plan deliberately treats your QA Automation background as an advantage.

You are **not learning to become an ML researcher or model trainer**. You are learning to approach AI systems as systems that require:

> **measurement → controlled experimentation → failure analysis → regression protection**

The recurring engineering loop throughout the eight weeks is:

```text
Corpus
   ↓
Chunking configuration
   ↓
Embeddings + Index
   ↓
Retrieval
   ↓
LLM answer generation
   ↓
Evaluation
   ↓
Metrics + failure analysis
   ↓
Experiment comparison
   ↓
Regression baseline
```

---

# 2. Weekly Structure

A recommended weekly allocation:

| Activity                      |     Hours |
| ----------------------------- | --------: |
| Concepts and targeted reading |       2–3 |
| Hands-on implementation       |       5–6 |
| Experimentation               |         2 |
| Documentation and reflection  |         1 |
| **Total**                     | **10–12** |

The priority is always:

**Understand enough → implement → measure → inspect failures.**

Avoid spending excessive time consuming tutorials.

---

# Week 1 — LLM Fundamentals and the AI System Mental Model

### Goal

Build enough understanding of LLM-based systems to reason about their behavior and evaluate them.

### Learn

Focus on:

* what an LLM does at inference time;
* prompts, context windows, and tokens;
* deterministic vs probabilistic behavior;
* temperature and generation variability;
* hallucination;
* context grounding;
* why identical prompts can produce different outputs;
* system inputs and configuration as part of the system under test.

### Do not prioritize

Skip:

* transformer mathematics;
* backpropagation;
* attention derivations;
* model training;
* GPU architecture.

### Practical work

Inside **Corpus Studio**, create the initial structure for the RAG Evaluation Laboratory.

Suggested conceptual structure:

```text
corpus-studio/
│
├── corpus/
├── datasets/
├── experiments/
├── configs/
├── results/
├── reports/
├── notebooks/
└── tests/
```

Create a first experiment record containing:

```text
experiment_id
date
corpus_version
chunking_strategy
chunk_size
chunk_overlap
embedding_model
retrieval_k
llm_model
generation_parameters
evaluation_dataset_version
```

### Deliverable

**Experiment 0: System Baseline Specification**

A short document answering:

* What are the inputs?
* What configuration can affect results?
* What outputs will be measured?
* What behavior would count as failure?

### Capability developed

✅ LLM fundamentals
✅ AI system thinking
✅ Experimental configuration awareness

---

# Week 2 — RAG Fundamentals and System Decomposition

### Goal

Understand RAG as an observable pipeline rather than a black box.

### Learn

Study the major components:

```text
Documents
    ↓
Parsing
    ↓
Chunking
    ↓
Embedding
    ↓
Vector Store
    ↓
Query Embedding
    ↓
Retrieval
    ↓
Context Construction
    ↓
LLM
    ↓
Answer
```

Understand the distinction between:

### Retrieval failure

```text
The correct information was not retrieved.
```

### Generation failure

```text
The correct information was retrieved, but the answer was poor.
```

This distinction is central to AI Reliability.

### Practical work

Build the smallest possible RAG pipeline.

Use:

* one controlled corpus;
* one embedding approach;
* one chunking strategy;
* a small set of manual questions.

For every query, store:

```text
query
retrieved_chunks
retrieval_scores
expected_source
generated_answer
```

### Deliverable

**RAG Pipeline v0.1**

The system should be able to execute:

```text
question → retrieval → context → answer
```

And preserve intermediate artifacts.

### Reliability question of the week

> When the final answer is wrong, how can I determine which component caused the failure?

### Capability developed

✅ RAG fundamentals
✅ System decomposition
✅ Observability fundamentals

---

# Week 3 — Embeddings and Vector Retrieval

### Goal

Understand what semantic retrieval is actually doing and how to measure whether it works.

### Learn

Focus on:

* embeddings as vector representations;
* semantic similarity;
* vector search;
* nearest-neighbor retrieval;
* cosine similarity conceptually;
* top-k retrieval;
* why embedding quality and chunking interact.

Do **not** spend time implementing vector databases from scratch.

### Practical work

Create a controlled retrieval experiment.

For approximately **20–30 queries**, define the expected relevant document or chunk.

Your evaluation dataset begins to look like:

```text
query_id
question
expected_document_id
expected_chunk_or_source
category
difficulty
```

Run retrieval without answer generation first.

This is important:

> **Evaluate retrieval independently before evaluating the full RAG system.**

### Introduce retrieval metrics

Start with:

* **Hit Rate / Recall@k**
* **MRR**
* optionally Precision@k

The initial question:

> Did the relevant information appear in the top-k retrieved results?

### Deliverable

**Retrieval Evaluation v0.1**

A script or workflow that:

```text
Evaluation Dataset
        ↓
Run Queries
        ↓
Retrieve Top-k
        ↓
Compare Against Expected Sources
        ↓
Calculate Metrics
```

### Capability developed

✅ Embeddings
✅ Vector retrieval
✅ Retrieval metrics
✅ Separation of retrieval from generation

---

# Week 4 — Evaluation Datasets and Ground Truth

### Goal

Learn how evaluation quality depends on the quality of the evaluation dataset.

### Learn

Study:

* evaluation datasets;
* representative test cases;
* golden datasets;
* ground truth;
* expected answers vs expected sources;
* difficult cases;
* ambiguity;
* dataset bias;
* dataset versioning.

### Build your dataset intentionally

Expand to approximately:

**40–60 evaluation queries**

Organize them into categories such as:

```text
Easy factual retrieval
Multi-part questions
Terminology questions
Questions requiring specific details
Ambiguous questions
Negative / unanswerable questions
```

For each case, record:

```text
id
question
expected_sources
expected_answer_or_facts
category
difficulty
notes
dataset_version
```

### Important reliability principle

Your evaluation dataset is the equivalent of a **test suite for an AI system**.

But unlike ordinary software assertions, some expected behavior may be:

* fuzzy;
* semantic;
* partially correct;
* context dependent.

### Practical work

Perform a dataset review.

Ask:

* Are all questions too easy?
* Are they representative?
* Are there known difficult cases?
* Are failure cases included?
* Could changes artificially improve the metric without improving the real system?

### Deliverable

**Evaluation Dataset v1**

A documented and versioned evaluation dataset.

### Capability developed

✅ Evaluation datasets
✅ Ground truth design
✅ Dataset quality awareness

---

# Week 5 — Answer Quality Evaluation

### Goal

Measure the full RAG system, not just retrieval.

### Learn

Separate answer quality into dimensions.

Suggested dimensions:

| Dimension                   | Question                               |
| --------------------------- | -------------------------------------- |
| Correctness                 | Is the answer factually correct?       |
| Groundedness                | Is it supported by retrieved context?  |
| Completeness                | Does it answer the important parts?    |
| Relevance                   | Does it address the question?          |
| Citation/source correctness | Does it point to appropriate evidence? |

### Practical work

Create a simple evaluation framework.

Start with two approaches:

### 1. Deterministic evaluation

Where possible:

```text
Expected source retrieved?
Required fact present?
Forbidden claim present?
```

### 2. Structured qualitative evaluation

For each answer:

```text
Correct: yes/no/partial
Grounded: yes/no
Complete: 1–5
Failure category
Notes
```

Do not initially over-engineer an automated "LLM-as-a-judge" system.

First learn to inspect results manually.

### Run your first end-to-end baseline

```text
Dataset v1
   +
Chunking Strategy A
   +
Embedding Model X
   +
Fixed Retrieval Configuration
```

Store all results.

### Deliverable

**Baseline Experiment A**

Including:

* retrieval metrics;
* answer quality metrics;
* failure examples.

### Capability developed

✅ AI evaluation
✅ Answer quality evaluation
✅ Retrieval vs answer quality distinction

---

# Week 6 — Chunking Experiment Design

## The Core Experiment Begins

### Goal

Design a controlled experiment comparing chunking strategies.

### Select 3 strategies

For example:

### Strategy A — Fixed-size chunks

```text
Chunk size: X
Overlap: Y
```

### Strategy B — Smaller chunks

```text
Chunk size: smaller
Overlap: adjusted
```

### Strategy C — Structure-aware or larger chunks

Depending on Corpus Studio capabilities and corpus structure.

The exact strategies are less important than experimental discipline.

### Control variables

Keep constant:

```text
Corpus
Evaluation dataset
Embedding model
Vector retrieval method
Top-k
LLM
Prompt
Generation parameters
```

Change:

```text
Chunking strategy
```

### Formulate hypotheses

For example:

> Smaller chunks may improve retrieval precision for highly specific questions but reduce context completeness.

> Larger chunks may improve answer completeness but introduce irrelevant context.

### Practical work

Create experiment configuration files.

Conceptually:

```yaml
experiment: chunking_A
corpus_version: v1
dataset_version: v1

chunking:
  strategy: fixed
  size: 500
  overlap: 50

embedding:
  model: X

retrieval:
  top_k: 5
```

Create equivalent configurations for B and C.

### Deliverable

**Experiment Protocol v1**

This should answer:

> Could another engineer reproduce this experiment from the recorded configuration?

### Capability developed

✅ Experimental design
✅ Controlled variables
✅ Reproducible experimentation

---

# Week 7 — Failure Analysis and Comparative Evaluation

### Goal

Run the experiment and learn from failures rather than metrics alone.

### Run

Execute all chunking strategies against the same evaluation dataset.

Produce a comparison table:

| Metric             | Strategy A | Strategy B | Strategy C |
| ------------------ | ---------: | ---------: | ---------: |
| Hit Rate@k         |            |            |            |
| MRR                |            |            |            |
| Answer Correctness |            |            |            |
| Groundedness       |            |            |            |
| Completeness       |            |            |            |

### Failure analysis

Create a taxonomy.

Suggested categories:

```text
RETRIEVAL_MISS
RETRIEVAL_WRONG_DOCUMENT
RETRIEVAL_PARTIAL_CONTEXT
CHUNK_TOO_SMALL
CHUNK_TOO_LARGE
CONTEXT_INCOMPLETE
GENERATION_HALLUCINATION
ANSWER_INCOMPLETE
AMBIGUOUS_QUERY
UNANSWERABLE_QUERY
```

Review failures manually.

For each interesting failure, answer:

1. What was expected?
2. What was retrieved?
3. What was generated?
4. Where did the failure originate?
5. Did chunking contribute?
6. Would the metric alone have revealed the problem?

### Deliverable

**Failure Analysis Report**

Include:

* top failure categories;
* representative examples;
* comparison between strategies;
* hypotheses for observed behavior.

### Capability developed

✅ Failure analysis
✅ Root-cause reasoning
✅ Qualitative evaluation
✅ Reliability engineering mindset

---

# Week 8 — Regression Testing and Reproducibility

### Goal

Turn the experiment into a small reliability laboratory rather than a one-off notebook.

## Build a regression baseline

Choose a baseline configuration.

For example:

```text
Baseline:
Chunking Strategy B
Embedding Model X
Top-k = 5
Dataset v1
```

Define acceptable regression thresholds.

Example:

```text
Recall@5 must not decrease by > 5%
MRR must not decrease by > 5%
Critical query failures must remain 0
Groundedness must not decrease
```

The exact thresholds should initially be treated as experimental policy, not universal truth.

### Add regression tests

Your laboratory should support something conceptually like:

```text
Run evaluation
      ↓
Compare with baseline
      ↓
Detect significant degradation
      ↓
Report regression
```

### Reproducibility checklist

Every experiment should preserve:

```text
✓ Corpus version
✓ Dataset version
✓ Chunking configuration
✓ Embedding model
✓ Retrieval parameters
✓ LLM configuration
✓ Prompt version
✓ Code version
✓ Timestamp
✓ Results
```

### Final practical work

Run the complete experiment from a clean or controlled starting point.

Verify:

> Can the experiment be executed again and produce a comparable result?

---

# Final Deliverable: Corpus Studio RAG Evaluation Laboratory v1

By the end of Week 8:

```text
Corpus Studio
│
├── corpus/
│   └── versioned source corpus
│
├── datasets/
│   └── evaluation_dataset_v1
│
├── configs/
│   ├── chunking_A
│   ├── chunking_B
│   └── chunking_C
│
├── experiments/
│   └── reproducible experiment definitions
│
├── results/
│   ├── retrieval_metrics
│   ├── answer_evaluations
│   └── regression_comparisons
│
├── failure_analysis/
│   └── categorized failures
│
├── reports/
│   └── chunking_comparison_report
│
└── tests/
    └── regression checks
```

---

# Expected Final Experiment

## Research Question

> **How do different chunking strategies affect retrieval performance and answer quality in a controlled RAG system?**

## Independent Variable

```text
Chunking strategy
```

## Controlled Variables

```text
Corpus
Evaluation dataset
Embedding model
Retriever
Top-k
Prompt
LLM configuration
```

## Dependent Variables

```text
Retrieval Hit Rate / Recall@k
MRR
Answer correctness
Groundedness
Completeness
Failure distribution
```

---

# Capability Progression

| Week | Primary Capability                      |
| ---- | --------------------------------------- |
| 1    | LLM fundamentals                        |
| 2    | RAG fundamentals                        |
| 3    | Embeddings + vector retrieval + metrics |
| 4    | Evaluation datasets                     |
| 5    | AI evaluation                           |
| 6    | Reproducible experimentation            |
| 7    | Failure analysis                        |
| 8    | Regression testing                      |

By the end, all required Phase 1 capabilities will have been exercised in one integrated system.

---

# Recommended Success Criteria

Phase 1 should be considered successful if you can independently explain and demonstrate:

### LLMs

* why output variability happens;
* how configuration affects behavior;
* why reproducibility is harder than conventional software testing.

### RAG

* how retrieval and generation failures differ;
* how embeddings influence retrieval;
* why chunking affects system behavior.

### Evaluation

* how to construct an evaluation dataset;
* how to measure retrieval;
* how to evaluate answer quality;
* why aggregate metrics are insufficient without failure inspection.

### Reliability

* how to design controlled experiments;
* how to preserve experiment configurations;
* how to compare results;
* how to establish a regression baseline.

---

# Portfolio-Level Outcome

The most valuable artifact from these eight weeks is **not simply “a RAG application.”**

It is:

> **A reproducible RAG evaluation laboratory demonstrating systematic experimentation, retrieval measurement, answer evaluation, failure analysis, and regression detection.**

That positioning is significantly more aligned with your intended transition toward:

**AI Evaluation → AI Reliability → Knowledge Quality Engineering → Agent Evaluation.**

## Recommended next step

After completing this plan, Phase 2 should naturally move toward **more rigorous evaluation frameworks, automated evaluation pipelines, experiment tracking, retrieval diagnostics, and increasingly realistic AI reliability problems**.
