# The Complete AI Prompting Framework: 6-Step Formula for 10× Better Results

> **Based on:** [How To Prompt ChatGPT The RIGHT WAY In 2025 (you're doing it wrong)](https://www.youtube.com/watch?v=pv_sAnH_P8Q)  
> **Authored in the style of Andrej Karpathy** — systems thinker, code-first, zero fluff, maximal signal.

---

> **Most people are using LLMs wrong.**  
> They treat them like Google: short queries, new sessions, zero memory, no structure.  
> This is like compiling C code with `-O0` and no type system — it *runs*, but you’re leaving 10× performance on the table.

This is the **complete, production-grade prompting framework** that turns stochastic token generators into **reliable cognitive engines**.

It works on **any frontier LLM** (GPT-4o, Claude 3.5, Gemini 1.5, Grok 4, Llama 3.1) because it’s built on **first principles** of how autoregressive transformers actually work.

---

## Why Prompting Skills Are the New Programming

In 2025:
- **Doctors** use LLMs to surface rare differential diagnoses
- **Engineers** prompt for root-cause analysis of distributed system failures
- **Lawyers** extract contract risk vectors in seconds

> **The best AI users won’t be replaced — they’ll be augmented.**  
> The rest will be automated.

---

## The 6-Part Prompting Framework

Think of this as **structured input to a massive function**:
```python
output = LLM(command, context, logic, role, format, questions)
```
Each argument is **non-optional** for high-stakes tasks.

---

### 1. **COMMAND**: Start with a Strong Verb (No Wishy-Washy Requests)

**Problem**: Vague imperatives → high entropy output  
**Solution**: Use **imperative, specific, action-oriented verbs**

#### Bad:
```text
Give me investing advice
```

#### Good:
```text
Recommend a diversified, tax-efficient investment strategy for a moderate-risk investor targeting a $400k home down payment in 5 years
```

#### Action Verb Lexicon (use these):
| Domain       | Verbs                          |
|--------------|--------------------------------|
| Analysis     | `Analyze`, `Diagnose`, `Compare`, `Evaluate` |
| Synthesis    | `Design`, `Build`, `Generate`, `Synthesize`  |
| Decision     | `Recommend`, `Prioritize`, `Rank`, `Decide`   |
| Execution    | `Write`, `Implement`, `Deploy`, `Execute`     |

> **Rule**: If your command doesn’t contain a verb from this list, rewrite it.

---

### 2. **CONTEXT**: Constrain the Conditional Distribution

LLMs are **next-token predictors**. Your prompt defines:
\[
P(\text{next token} \mid \text{past tokens})
\]

**More relevant context → tighter distribution → better samples**

#### The Rule of Three:
```text
Who  → demographic, role, experience, constraints
What → goal, requirements, edge cases
When → timeline, urgency, milestones
```

#### Example:
```text
You are advising a 32-year-old software engineer in SF (TC: $220k, expenses: $90k/yr). 
They have $25k cash, $15k in BTC, no debt, and want to buy a $1.2M home in 5 years 
while preserving upside for early retirement.
```

#### Context Scaling Law:
| Task Complexity       | Context Investment |
|-----------------------|--------------------|
| Restaurant pick       | 1 sentence         |
| Business plan         | 5–10 paragraphs    |
| Life decision         | Full financial model + voice memo answers |

---

### 3. **LOGIC**: Define the Reasoning Trace and Output Schema

**Without logic, the model improvises.**  
**With logic, it follows a deterministic reasoning path.**

#### Basic:
```text
For each asset class: list name, allocation %, justification, and 1–2 example funds/ETFs
```

#### Advanced (JSON Schema):
```text
Return valid JSON:
{
  "summary": str,
  "allocation": [{"asset": str, "pct": float, "rationale": str, "vehicles": [str]}],
  "risks": [str],
  "timeline": [{"year": int, "action": str}]
}
```

#### Output Format Primitives:
| Format             | Use Case                           |
|--------------------|------------------------------------|
| `Table`            | Comparisons, data                  |
| `Numbered Steps`   | Processes, onboarding              |
| `Bullet Points`    | Equal-weight items                 |
| `H1/H2 Sections`   | Reports, documentation             |
| `Copy-Paste Block` | Emails, code, messages             |
| `Apple Notes Style`| Screenshotable, clean              |

---

### 4. **ROLEPLAY**: Activate Latent Expert Personas

LLMs are **ensembles of simulated experts**.  
Your role prompt **routes to the right sub-network** (especially in MoE models).

#### Template:
```text
You are a [certification] [role] with [N] years specializing in [domain] for [audience]
```

#### Field-Specific Roles:
| Field       | Role Prompt                                                                 |
|-------------|-----------------------------------------------------------------------------|
| Finance     | `Certified CFP with 15 years in personal finance for tech employees`        |
| Engineering | `Senior staff ML engineer at FAANG, ex-DeepMind, PhD in systems`            |
| Legal       | `Corporate M&A lawyer, 12 years at AmLaw 10, Harvard JD`                    |
| Marketing   | `Growth lead at Series C startup, ex-FB ads, $100M+ managed spend`          |

#### Tone Modifiers:
```text
Be conservative and cite tax implications
Take a first-principles approach
Prioritize simplicity over optimization
```

---

### 5. **FORMATTING**: Structure for Immediate Usability

**Goal**: Output should be **zero-friction to consume or forward**

#### Example:
```text
Structure response as:

## Executive Summary
[2–3 sentences]

## Asset Allocation
| Asset | % | Rationale | Vehicles |
|-------|---|---------|----------|

## Implementation Timeline
1. [Month 1]: Open brokerage...
2. ...

## Risk Dashboard
- [ ] Market crash → rebalance?
- [ ] Job loss → emergency fund?
```

#### Pro Formats:
- `Markdown table` → GitHub, Notion
- ````json` block` → API, scripts
- `> Quote` → email threads
- `TODO checklist` → task handoff

---

### 6. **QUESTIONS**: Iterative Refinement via Active Probing

This is the **secret sauce**.  
You’re not just prompting — you’re **co-designing with the model**.

#### Core Prompt:
```text
Ask me 10 clarifying questions to make this strategy 10x more precise.
Prioritize gaps in tax, liquidity, and behavioral risk.
```

#### The 3-Round Protocol:
```text
Round 1 → 10 broad questions
Round 2 → 10 follow-ups on your answers
Round 3 → 10 deep technical/behavioral questions
Stop when questions repeat
```

#### Pro Tips:
- **Use voice memos** (transcribe via Whisper)
- **For $1M+ decisions**: go to 30+ questions
- **For daily tasks**: 3–5 is enough

---

## Full Framework Example (Copy-Paste Ready)

```text
**COMMAND**
Recommend a tax-efficient, diversified investment strategy

**CONTEXT**
for a 32-year-old staff software engineer in San Francisco (TC: $220k, expenses: $90k/yr), 
with $25k cash, $15k BTC, no debt, saving for $1.2M home in 5 years 
while preserving early retirement optionality

**LOGIC**
For each asset: name, target %, rationale, tax implications, 1–2 example funds/ETFs.
Include rebalancing rules and liquidity plan.

**ROLEPLAY**
You are a Certified Financial Planner (CFP) with 15 years experience 
advising Bay Area tech professionals on mid-term wealth accumulation. 
You are conservative, tax-aware, and behavioral-coach trained.

**FORMATTING**
Structure as:
1. Executive Summary (3 sentences)
2. Asset Allocation Table (Markdown)
3. Implementation Timeline (numbered)
4. Risk & Contingency Plan (checklist)
5. Tax Optimization Notes

**QUESTIONS**
Ask me 10 questions to refine this further — focus on:
- Tax situation (RSUs, cap gains, 401k)
- Behavioral risk tolerance
- Family/fiancé financial alignment
- Liquidity needs
```

---

## Best Practices & Pro Tips

| Principle               | Implementation                                      |
|-------------------------|-----------------------------------------------------|
| **Model Selection**     | GPT-4o / Claude 3.5 / Gemini 1.5 Pro → best fidelity |
| **Session Continuity**  | Use chat memory or inject prior context             |
| **Voice Input**         | Speak → Whisper → paste → iterate                   |
| **Iteration Loop**      | Prompt → Questions → Answer → Refine → Final       |
| **Version Control**     | Save prompts as `.prompt.md` in Git                 |

---

## Common Failure Modes (Avoid These)

| Mistake                     | Symptom                                  | Fix                                   |
|----------------------------|------------------------------------------|---------------------------------------|
| Weak command               | Generic, rambling output                 | Use strong verb + specificity         |
| No context                 | "Applies to anyone" advice               | Apply Rule of Three                   |
| No schema                  | Wall of text                             | Define table/JSON upfront             |
| Generic role               | Surface-level insights                   | Use certified + years + niche         |
| No questions               | 7/10 result                              | Force 10+ clarifying questions        |

---

## Advanced Applications

| Domain         | Framework Adaptation                              |
|----------------|---------------------------------------------------|
| **Engineering** | Add `CoT` + `ReAct` + tool calling (browser, code) |
| **Legal**       | Attach contract PDFs + `cite section X.Y`         |
| **Creative**    | Heavy roleplay + `temperature=0.9` + few-shot    |
| **Education**   | `Socratic mode` + question loops                  |

---

## Conclusion: Prompting Is the New Programming

> **The LLM is your compiler.**  
> **Your prompt is the source code.**

Write clean, typed, well-documented prompts — and you’ll get **deterministic, debuggable, 10× better results**.

Start today:
1. Pick one recurring task
2. Apply the 6-part framework
3. Iterate with questions until output is *immediately usable*

The future belongs to those who **prompt like engineers**.

---

```
