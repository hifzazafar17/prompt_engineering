# prompt_engineering

# Prompt Engineering for Beginners: A Comprehensive Guide to Effective AI Communication

**Key Takeaways**  
- With **46.59B visits**, **ChatGPT** accounts for **>83%** of total traffic among the top 10 chatbots.  
- **DeepSeek** (2nd place) has only **~6%** of ChatGPT’s traffic (2.74B visits).  
- Traffic is highly concentrated, but includes U.S., Chinese, and European players.

---

## How LLMs Work  
[How LLMs Work: Top 10 Executive-Level Questions](https://sloanreview.mit.edu/article/how-llms-work/)

---

## Understand the Power of Prompts  
### Context Engineering for Agentic AI, Image/Video Generation, UX/UI Design & Development  

Master prompt and context engineering with these hands-on tutorials:  
* **[Complete Guide to Context Engineering for AI Agents](https://github.com/panaversity/learn-n8n-agentic-ai/blob/main/00_prompt_engineering/context_engineering_tutorial.md)**  
* **[Nano Banana Tutorial – Image Generation](https://github.com/panaversity/learn-low-code-agentic-ai/blob/main/00_prompt_engineering/image_generation/readme.md)**  
* **[Google's Veo 3: A Guide With Practical Examples](https://github.com/panaversity/learn-low-code-agentic-ai/blob/main/00_prompt_engineering/video_generation/readme.md)**  
* **[UX Design by Prompting](https://github.com/panaversity/learn-low-code-agentic-ai/tree/main/00_prompt_engineering/ux_design)**  
* **[UI Development by Prompting](https://github.com/panaversity/learn-low-code-agentic-ai/tree/main/00_prompt_engineering/ui_development)**  

---

## Which is the Best LLM?  
See real-time head-to-head comparisons across **text, image, vision, and multimodal** tasks:  
[https://lmarena.ai/leaderboard](https://lmarena.ai/leaderboard)

---

## Use These Prompt Engineering Tools to Learn  
- [OpenAI Chat Playground](https://platform.openai.com/chat/)  
- [Google AI Studio](https://aistudio.google.com/)  
- [Anthropic Console](https://console.anthropic.com/)  

---

## Prompt Coach  
> A reusable **meta-prompt** to turn messy ideas into polished, high-performance prompts.

```text
You are my Prompt Coach. I will give you a rough or unclear prompt.
Your task is to:
1. Clarify it
2. Add missing context
3. Structure it for best results
4. Suggest 2–3 alternative versions (simple, detailed, structured)
Here’s my rough prompt: [INSERT YOUR PROMPT HERE]
```

---

## Table of Contents  
1. [What is Prompt Engineering?](#what-is-prompt-engineering)  
2. [Understanding Large Language Models](#understanding-large-language-models)  
3. [Essential Configuration Settings](#essential-configuration-settings)  
4. [Fundamental Prompting Techniques](#fundamental-prompting-techniques)  
5. [Advanced Prompting Strategies](#advanced-prompting-strategies)  
6. [Best Practices for Effective Prompts](#best-practices-for-effective-prompts)  
7. [Common Pitfalls and How to Avoid Them](#common-pitfalls-and-how-to-avoid-them)  
8. [Hands-On Examples](#hands-on-examples)  
9. [Testing and Iteration](#testing-and-iteration)  
10. [Resources and Next Steps](#resources-and-next-steps)  
11. [Mixture-of-Experts (MoE) and Prompt Engineering](#mixture-of-experts-moe-and-prompt-engineering)  
12. [The 6-Part Prompting Framework](https://github.com/panaversity/learn-low-code-agentic-ai/blob/main/00_prompt_engineering/readme.md#the-6-part-prompting-framework)  

---

## What is Prompt Engineering?  
**Prompt engineering** is the disciplined practice of designing input sequences to elicit precise, reliable, and efficient outputs from autoregressive language models. It is *inference-time programming* — no gradient updates required.

**Why it matters:**  
- No coding or fine-tuning needed  
- Can improve zero-shot performance by **20–50%** on GLUE, MMLU, etc.  
- Core skill for production LLM apps (RAG, agents, tools)  
- Iterative, measurable, versionable — treat prompts like code  

---

## Prompt Engineering vs. Context Engineering  

| Aspect              | **Prompt Engineering**                                  | **Context Engineering**                                  |
|---------------------|---------------------------------------------------------|----------------------------------------------------------|
| **Goal**            | Define *how* to behave and *what* to produce            | Provide *facts, examples, tools* to ground reasoning     |
| **Levers**          | Wording, roles, CoT, schema, few-shot                   | RAG, chunking, memory, APIs, state                       |
| **Example Change**  | “Return JSON only. Cite sources.”                       | Attach top-5 retrieved passages + policy PDF             |
| **Failure Mode**    | Wrong format, poor reasoning                            | Hallucinations, outdated info                            |
| **Ownership**       | Prompt designers, app devs                              | Data/ML engineers, platform teams                        |

> **One-liner**: *Prompt = how to think. Context = what to think about.*

---

### How They Work Together  
1. **Prompt** → Enforces schema, reasoning mode, citations  
2. **Context** → Supplies ground truth (docs, memory, tool outputs)  
3. **Eval** → Measure *prompt fidelity* and *context grounding* separately  

---

### Concrete Examples  

#### 1. Invoice → JSON Extractor  
- **Prompt**:  
  ```text
  Extract {vendor, date, total}. Return JSON only. Missing → null. Cite line numbers.
  ```  
- **Context**: RAG-retrieved vendor spec + 3 labeled examples  

#### 2. Policy Q&A Bot  
- **Prompt**:  
  ```text
  Answer using attached passages only. If unsure: “Not in policy.” Cite §ID.
  ```  
- **Context**: Vector store over policy repo (`dept=HR`, `valid_from>2024`)  

#### 3. Agentic Workflow  
- **Prompt**: ReAct loop with tool schemas  
- **Context**: Episodic memory + tool responses per turn  

---

### Practical Tips  
- **Prompt**: Short, schema-first, regex-testable  
- **Context**: 512-token chunks, hybrid BM25+cosine rank, cap at 60% window  
- **Eval**: LLM-as-judge + exact-match  

---

## Understanding Large Language Models  

### How LLMs Work (The Basics)  
LLMs are **next-token predictors** trained via self-supervised learning:  
\[
P(y_t | y_{<t}, x) \approx \theta^* = \arg\max_\theta \mathbb{E}[\log P(y | x; \theta)]
\]  
- Input: prompt \( x \)  
- Output: completion \( y \)  
- No “understanding” — just high-dimensional pattern matching  

### 2025 Frontier Architectures  
| Type       | Example         | Activation         | Context Window |
|------------|-----------------|--------------------|----------------|
| Dense      | Llama-3 70B     | 100% params/token  | 128k           |
| **MoE**    | **Grok 4**, DeepSeek-V3 | **~10–25%** active | 128k–1M        |
| Hybrid     | Mamba-inspired  | Recurrent state    | >1M            |

---

## Essential Configuration Settings  

### Temperature (0–1)  
\[
p_i = \frac{\exp(z_i / T)}{\sum \exp(z_j / T)}
\]  
| T     | Behavior             | Use Case                     |
|-------|----------------------|------------------------------|
| 0.0   | Greedy, deterministic| Math, JSON, code             |
| 0.7   | Balanced             | Reasoning, analysis          |
| 0.9+  | Creative, risky      | Poetry, brainstorming        |

### Top-p & Top-k  
- **Top-p (Nucleus)**: Sample from smallest set with prob ≥ p  
- **Top-k**: Hard limit to k candidates  

**Recommended Regimes**  
| Regime       | T    | Top-p | Top-k | Use Case                  |
|--------------|------|-------|-------|---------------------------|
| Deterministic| 0.0  | 1.0   | —     | Extraction, JSON          |
| Balanced     | 0.2  | 0.95  | 40    | Reasoning, analysis       |
| Creative     | 0.9  | 0.99  | 64    | Story, poetry             |

### Max Tokens  
- 2025: 128k → 1M+ (Gemini 2.5)  
- **Reserve 20%** for system + tools  

---

## Fundamental Prompting Techniques  

### 1. Zero-Shot  
```text
Classify: "The plot was predictable." → negative
```  

### 2. One-Shot  
```text
EN→FR: "Hello" → "Bonjour"
EN→FR: "Library?" →
```  

### 3. Few-Shot (3–8 examples)  
```text
Feedback → JSON:
"Great service, cold food" → {"service": "+", "food": "-"}
...
"Terrible staff" →
```  
> **Tip**: Use *diverse, consistent, high-quality* examples  

### 4. System Prompt  
```text
You are a concise analyst. Output JSON only. Never explain.
```  

### 5. Role Prompting  
```text
You are a compiler engineer optimizing CUDA kernels.
```  
> In MoE: may route to code/math experts  

### 6. Contextual Prompting  
```text
Context: Target = ML engineers new to CUDA.
Explain tensor cores in 200 words.
```  

---

## Advanced Prompting Strategies  

### Chain of Thought (CoT)  
```text
Q: If I was 6 when sister was 3, how old is she when I’m 40?
A: Let’s think step by step.
```  
> +30% on arithmetic/logic  

**CoT-SC**: Sample 8 paths → majority vote  

---

### Step-Back Prompting  
```text
First, recall Fitts’ and Hick’s laws.
Now redesign login flow using them.
```  

---

### ReAct (Reason + Act)  
```text
Thought: Need Tokyo population 2025
Action: web_search["Tokyo population 2025"]
Observation: 37.4M metro
...
Final Answer: Tokyo > NYC by ~13.8M
```  

---

### Tree of Thoughts (ToT)  
```text
Branch 1: Influencer campaign → 8/10
Branch 2: Pop-up events → 7/10
Synthesis: Hybrid strategy
```  
> **2025**: Graph-of-Thoughts (GoT) adds merging/backtracking  

---

## Best Practices for Effective Prompts  

1. **Be Specific**  
   Bad: `Write about AI`  
   Good: `Write 300-word explainer on MoE routing for CS undergrads`  

2. **Use Action Verbs**  
   `Analyze`, `Extract`, `Synthesize`, `Rank`  

3. **Schema-First**  
   ```json
   {"answer": "...", "confidence": 0.95}
   ```  

4. **Delimiters**  
   Use ```, """, or XML tags  

5. **Positive Instructions**  
   > "Be concise"  
   > "Don’t ramble"  

6. **Template Variables**  
   ```text
   Role: {expert}
   Task: Analyze {doc_type} for {audience}
   ```  

7. **Version Control Prompts Like Code**  

---

## Common Pitfalls and How to Avoid Them  

| Pitfall                | Symptom                  | Fix                              |
|------------------------|--------------------------|----------------------------------|
| Ambiguity              | Off-topic drift          | Add constraints                  |
| Contradictions         | Model apologizes         | Audit logic                      |
| Token Overflow         | Truncated output         | Use `tiktoken`                   |
| Over-Few-Shot          | Examples dominate        | Move to RAG                      |
| Temp Mismatch          | Hallucinations in facts  | T=0 for extraction               |

---

## Hands-On Examples  

### 1. Social Media Post  
```text
Role: Coffee sommelier
Task: Instagram caption for Pumpkin Spice Maple Latte
Audience: 25–40 urban professionals
Tone: Warm, sensory, subtle CTA
Constraints: ≤150 chars, 4 hashtags
Include aroma/taste
```  

### 2. Data Analysis  
```text
Analyze reviews [PASTE].
Output JSON:
{
  "sentiment": {"pos": %, "neg": %, "neu": %},
  "top_pos": [str],
  "top_neg": [str],
  "recs": [{"action": str, "prio": "high/med/low"}],
  "conf": "high/med/low"
}
```  

### 3. Code Generation  
```text
Python function sort_by_key(lst: list[dict], key: str, desc: bool)
- Missing keys → end
- Type hints + docstring
- Example + tests
```  

---

## Testing and Iteration  

### Prompt Testing Framework  
| Version | Goal           | Model   | T   | Metrics                     | Notes               |
|---------|----------------|---------|-----|-----------------------------|---------------------|
| v1.0    | JSON extraction| Grok-4  | 0.0 | 98% schema, 2% halluc       | Too verbose         |
| v1.1    | Same           | Grok-4  | 0.0 | 100% schema, 0% halluc      | Added "JSON only"   |

### A/B Testing  
Run 50 inferences per variant → measure:  
- Exact Match (schema)  
- BLEU/ROUGE (freeform)  
- LLM-as-Judge (relevance)  

### Evaluation Metrics  
- **Groundedness**: % claims with citation  
- **Latency**: ms/token  
- **Cost**: $ per 1k tokens  

---

## Advanced Tips for 2025  

1. **Structured Outputs** → JSON mode, Guidance  
2. **Context Compression** → Summarize prior turns  
3. **Multimodal**  
   ```text
   Image: [upload]
   Describe damage → JSON claim
   ```  
4. **Prompt Chaining**  
   Step 1: Research → Step 2: Outline → Step 3: Draft  

---

## Resources and Next Steps  

### Tools  
- OpenAI Playground, Anthropic Console, Google AI Studio  
- **DSPy**, **Guidance**, **LangChain**  

### Papers  
- Wei et al. (2022): *Chain-of-Thought Prompting*  
- Yao et al. (2023): *ReAct*  

### Practice Projects  
1. RAG QA Bot with citations  
2. Code Refactoring Agent (ToT)  
3. Multimodal Meme Generator  

### Prompt Library  
```bash
/prompts/extraction/json_invoice_v2.txt
/tests/invoice_*.json
```

---

## Mixture-of-Experts (MoE) and Prompt Engineering  

> **MoE = Sparse activation**: Total params >> Active params per token  

### Core Components  
1. **Experts**: Specialized FFNs (math, code, language)  
2. **Router**:  
   \[
   g_i = \text{softmax}(x W_g)_i \quad ; \quad y = \sum_{i \in \text{top-k}} g_i E_i(x)
   \]  
3. **Sparsity**: e.g., DeepSeek-V3: **671B total → 37B active**  

---

### 2025 Frontier MoE Status  

| LLM             | Developer  | MoE?       | Details                                      |
|-----------------|------------|------------|----------------------------------------------|
| GPT-5           | OpenAI     | Speculated | ~2T params, dynamic routing                  |
| **Grok 4**      | **xAI**    | **Yes**    | Multi-agent MoE, ~500B, strong ARC-AGI       |
| Gemini 2.5 Pro  | Google     | Yes        | 1M context, efficient scaling                |
| Claude 4        | Anthropic  | No         | Dense (~400B)                                |
| DeepSeek-V3     | DeepSeek   | Yes        | 671B/37B active, MLA, $5.6M training         |

---

### How MoE Changes Prompt Engineering  

| Change                      | Implication                                      | Tip                                      |
|----------------------------|--------------------------------------------------|------------------------------------------|
| **Router Sensitivity**     | Early tokens dominate expert selection           | **Front-load domain**                    |
| **Expert Elicitation**     | Explicit roles route to specialists              | `Role: Math Expert`                      |
| **Consistency**            | Stochastic top-k → variance                      | T=0 + ensemble runs                      |
| **Few-Shot = Router Training** | Examples bias gating                         | Use *in-domain* examples only            |

---

### Routing-Friendly Prompt Skeleton  
```text
Role: <domain expert>
Task: <crisp verb phrase>
Audience: <skill level>
Output: ```json
Steps:
1. <micro-step>
Examples: <1–2 tight>
Context: <RAG, ≤40% window>
Solve.
```

---

### Troubleshooting MoE  
| Issue                     | Fix                                              |
|---------------------------|--------------------------------------------------|
| Inconsistent answers      | Sharpen role + T=0 + short exemplar              |
| Wrong expert activated    | Add skill tag + in-domain example                |
| Mixed-topic output        | Split into chain or plan-first                   |

> **Bottom line**: MoE **amplifies the power of early, domain-specific signals** — your prompt selects which sub-networks fire.

---

## Conclusion  

**Prompt engineering is software engineering for the autoregressive era.**  

Master it by:  
1. Starting minimal → measure → iterate  
2. Versioning prompts like code  
3. Separating **instruction** (prompt) from **knowledge** (context)  
4. Leveraging **MoE routing** via domain anchors  
5. Automating evaluation  

> The model is a **distribution over token sequences**.  
> Your prompt **shapes that distribution**.  

**Craft ruthlessly. Test relentlessly. Ship reliable cognitive engines.**

---

```
```
