# LLM Benchmark: Cross-Timezone Meeting-Time Reasoning

## Overview

This benchmark evaluates how six candidate LLM responses answered the prompt below, and how three evaluator models ranked those responses. See [readme.md](readme.md) for the first benchmark.

> **Prompt**  
> "Find the most optimal meeting time that works across Brisbane (Australia), New York (USA), and London (UK), ideally falling within business hours for all three cities, or as close to business hours as possible."

### Candidate response models
- Gemma 4 31B
- Gemini 3.1 Flash Lite
- Qwen 3.6 Plus
- GLM-5V Turbo
- GLM-5 Turbo
- Claude Code + Opus 4.6 1M with `timezones.centminmod.com/llms.txt` tool setup. Timezones Scheduler web app <https://timezones.centminmod.com/> supports both web and CLI/API/MCP for AI agents.

### Evaluator models
- GPT-5.4
- Claude Opus 4.6
- Gemini 3.1 Pro

---

## Benchmark objective

The purpose of this benchmark is to compare:

1. **Response quality** across candidate LLMs
2. **Ranking behavior** across evaluator LLMs
3. **Tradeoffs** among correctness, practicality, polish, and cost

This is not only a benchmark of timezone reasoning. It is also a benchmark of how evaluators interpret the word **optimal**.

---

## Ground truth and task constraints

### Core constraint
There is **no true 9:00 AM to 5:00 PM overlap** across Brisbane, London, and New York.

### Why
Depending on season:

- **Brisbane**: UTC+10 year-round
- **London**: UTC+1 in BST, UTC+0 in GMT
- **New York**: UTC-4 in EDT, UTC-5 in EST

That creates a Brisbane to New York spread of:

- **14 hours** during Northern Hemisphere summer
- **15 hours** during Northern Hemisphere winter

So a perfect three-way standard-business-hours overlap is impossible.

### Two valid interpretations of “optimal”
The benchmark revealed two defensible interpretations:

1. **Strict business-hours maximization**  
   Maximize how many participants are inside standard business hours first, then break ties by choosing the least-bad off-hours option.  
   Under this objective, **9 AM NY / 2 PM London / 11 PM Brisbane** is highly defensible because it achieves the ceiling of **2 of 3 participants inside business hours**.

2. **Balanced compromise**  
   Minimize the worst inconvenience across all three participants, even if that means fewer participants are inside strict business hours.  
   Typical answer corridor: **6 AM NY / 11 AM London / 8 PM Brisbane** to **8 AM NY / 1 PM London / 10 PM Brisbane**

A strong response should either:
- distinguish these interpretations clearly, or
- justify which optimization goal it selected

---

## Evaluation rubric

All evaluator judgments are normalized against this shared rubric.

| Criterion | Description |
|---|---|
| **Timezone correctness** | Correct offsets, DST handling, and recognition that no 9 to 5 overlap exists |
| **Optimization quality** | Whether the answer chooses, explains, and consistently applies a sensible definition of “optimal” |
| **Practical usefulness** | Whether the recommendation is realistic for human scheduling |
| **Presentation quality** | Clarity, structure, tradeoff explanation, and actionable output |
| **Cost efficiency** | Quality delivered relative to token usage and cost |

---

## Candidate model response summary

| Model | Primary recommendation | Main strength | Main weakness |
|---|---|---|---|
| **Gemma 4 31B** | 8 AM NY / 1 PM London / 10 PM Brisbane | Strong math and very low cost | Treats one optimization target as universal |
| **Gemini 3.1 Flash Lite** | 8 AM NY / 1 PM London / 10 PM Brisbane | Concise and technically clear | Less complete than top-tier answers |
| **Qwen 3.6 Plus** | 5 AM NY / 10 AM London / 7 PM Brisbane | Strong DST and UTC-anchor framing | Main recommendation is too harsh on New York |
| **GLM-5V Turbo** | 6 AM NY / 11 AM London / 8 PM Brisbane | Best balanced-compromise framing and polished structure | Expensive, plus a BST season-label flaw |
| **GLM-5 Turbo** | 7 AM NY / 12 PM London / 9 PM Brisbane | Strong practical compromise and clean structure | Less explicit than GLM-5V on optimization framing |
| **Claude Code + Opus 4.6 1M tool setup** | 9 AM NY / 2 PM London / 11 PM Brisbane | Explicit scoring function and strongest strict business-hours optimization | Less balanced for human comfort than compromise-oriented answers |

### Additional note on the tool-assisted Claude Code response
The tool-assisted response introduces an explicit overlap-scoring framework, reporting a best overlap score of **6/9 (67%)** and selecting the earliest slot among a set of tied high-scoring candidates. This is methodologically important because it makes the optimization function visible instead of leaving it implicit. Under a **strict business-hours maximization** objective, the selected recommendation, **11 PM Brisbane / 2 PM London / 9 AM New York**, is one of the strongest answers in the set because it achieves the maximum feasible outcome of **2 of 3 participants inside business hours** while keeping the off-hours participant as early as possible within the tied top-scoring group.


---

## Response metrics

### Cost and throughput metrics by candidate response

| Model | Prompt tokens | Completion tokens | Reasoning tokens | Total visible output basis | Tokens/sec | First token latency | Final cost |
|---|---:|---:|---:|---:|---:|---:|---:|
| **Gemini 3.1 Flash Lite** | 184 | 879 | 0 | 1,063 | 172.9 | 1.97s | $0.00136 |
| **GLM-5V Turbo** | 187 | 2,807 | 1,244 | 2,994 | 102.0 | 0.88s | $0.0114 |
| **Gemma 4 31B** | 213 | 1,943 | 947 | 2,156 | 41.2 | 0.41s | $0.000807 |
| **GLM-5 Turbo** | 186 | 2,669 | 1,887 | 2,855 | 57.2 | 0.73s | $0.0108 |
| **Qwen 3.6 Plus** | N/A | N/A | N/A | N/A | N/A | N/A | N/A |
| **Claude Code + Opus 4.6 1M tool setup** | N/A | N/A | N/A | N/A | N/A | N/A | N/A |

### Metric notes
- “Total visible output basis” here is prompt plus completion tokens.
- Reasoning tokens were only reported for some models.
- No metric block was provided for Qwen 3.6 Plus.
- No metric block was provided for the Claude Code + Opus 4.6 1M tool-assisted response.

---

## Evaluator rankings

## 1. GPT-5.4 ranking

| Rank | Model | Rationale |
|---|---|---|
| **1** | **Claude Code + Opus 4.6 1M tool setup** | Best strict business-hours optimization, explicit scoring rule, and clear tie-breaking logic |
| **2** | **GLM-5V Turbo** | Best balanced-compromise framing, strongest scenario breakdown, most decision-useful output |
| **3** | **GLM-5 Turbo** | Strong practical recommendation and clear seasonal treatment |
| **4** | **Gemma 4 31B** | Excellent factual quality and best value, but less nuanced on optimization goals |
| **5** | **Gemini 3.1 Flash Lite** | Good concise answer with useful alternatives |
| **6** | **Qwen 3.6 Plus** | Reasonable math but least practical main recommendation |

### GPT-5.4 interpretation
GPT-5.4 weights **optimization quality** most heavily and now treats **strict business-hours maximization** as the primary reading of the prompt, with balanced human usability as a secondary lens.

---

## 2. Claude Opus 4.6 ranking

| Rank | Model | Rationale |
|---|---|---|
| **1** | **Claude Code + Opus 4.6 1M tool setup** | Best strict business-hours optimizer, transparent scoring method, and strongest fit to the stated objective |
| **2** | **GLM-5 Turbo** | Best practical compromise when comfort-balancing matters more than strict in-hours maximization |
| **3** | **Gemma 4 31B** | Strong mathematical justification and by far the best cost-to-quality ratio |
| **4** | **Gemini 3.1 Flash Lite** | Correct and efficient, but thinner than the top group |
| **5** | **GLM-5V Turbo** | Richest formatting and broadest coverage, but penalized for BST date-label error and a balance-first framing |
| **6** | **Qwen 3.6 Plus** | DST-aware, but too punishing on New York with a 5 AM slot |

### Claude Opus 4.6 interpretation
Claude weights **objective adherence**, **factual cleanliness**, and **cost-to-quality** more strongly than surface polish.

---

## 3. Gemini 3.1 Pro ranking

Gemini 3.1 Pro did not provide a clean numbered ranking for all five models, but its evaluation implies the following order:

| Implied rank | Model | Rationale |
|---|---|---|
| **1** | **Claude Code + Opus 4.6 1M tool setup** | Explicit score-based method, strong grounding, and best fit if maximizing strict business-hours coverage is the goal |
| **2** | **GLM-5V Turbo** | Best professional formatting, best end-user presentation, strongest “executive” feel |
| **3** | **Gemma 4 31B** | Best value and strongest mathematical logic for the price |
| **4** | **Gemini 3.1 Flash Lite** | Best brevity plus technical clarity |
| **5** | **Qwen 3.6 Plus** | Useful UTC-anchor and DST mismatch framing, but harsher recommendation |
| **6 / omitted** | **GLM-5 Turbo** | Not properly included in the main comparison despite being one of the strongest actual responses |

### Gemini 3.1 Pro interpretation
Gemini 3.1 Pro appears to weight **optimization explicitness**, **presentation polish**, and **document readiness** most heavily under the business-hours-first reading.

---

## Side-by-side evaluator comparison

| Model | GPT-5.4 | Claude Opus 4.6 | Gemini 3.1 Pro |
|---|---:|---:|---:|
| **Claude Code + Opus 4.6 1M tool setup** | **1** | **1** | **1** |
| **GLM-5V Turbo** | 2 | 5 | 2 |
| **GLM-5 Turbo** | 3 | 2 | 6 / omitted |
| **Gemma 4 31B** | 4 | 3 | 3 |
| **Gemini 3.1 Flash Lite** | 5 | 4 | 4 |
| **Qwen 3.6 Plus** | 6 | 6 | 5 |

---

## Agreement analysis

| Model | Agreement level | Shared evaluator view | Main source of disagreement |
|---|---|---|---|
| **Claude Code + Opus 4.6 1M tool setup** | High | Explicit scoring, strong grounding, and best strict business-hours fit | Little disagreement once the prompt is read as business-hours-first |
| **GLM-5V Turbo** | Medium | Rich, polished, detailed, high utility | Whether balance-first optimization should outrank strict in-hours maximization |
| **GLM-5 Turbo** | Low to medium | Strong practical answer | Claude likes it more than GPT-5.4 and Gemini because it rewards pragmatic balance |
| **Gemma 4 31B** | High | Strong logic, high accuracy, excellent value | Whether it is just best value or near-best overall |
| **Gemini 3.1 Flash Lite** | High | Correct, concise, efficient | Mostly differences in completeness weighting |
| **Qwen 3.6 Plus** | High | DST-aware but least practical | All evaluators see it as the weakest primary recommendation |

---

## Rank spread analysis

To show evaluator variance more clearly:

| Model | Best rank | Worst rank | Rank spread | Interpretation |
|---|---:|---:|---:|---|
| **Claude Code + Opus 4.6 1M tool setup** | 1 | 1 | 0 | Most stable winner under the chosen benchmark objective |
| **GLM-5V Turbo** | 2 | 5 | 3 | Polarizing because of balance-first framing and a label error |
| **GLM-5 Turbo** | 2 | 6 | 4 | Strong answer but underrepresented by Gemini and not optimized for strict in-hours coverage |
| **Gemma 4 31B** | 3 | 4 | 1 | Most stable high performer after the top winner |
| **Gemini 3.1 Flash Lite** | 4 | 5 | 1 | Consistently good, rarely top |
| **Qwen 3.6 Plus** | 5 | 6 | 1 | Consistently weakest practical recommendation |

---

## Consensus and adjudicated view

### Simple consensus view
Across evaluators:

- **Claude Code + Opus 4.6 1M tool setup** is the clearest winner when the prompt is read as maximizing strict business-hours alignment
- **Gemma 4 31B** is the most consistently strong non-tool-assisted model
- **GLM-5V Turbo** and **GLM-5 Turbo** remain strong alternatives when balanced human comfort is prioritized
- **Gemini 3.1 Flash Lite** is consistently solid but not best-in-class
- **Qwen 3.6 Plus** is consistently weakest overall

### Adjudicated benchmark interpretation
If all three evaluator perspectives are combined:

| Final category | Model | Reason |
|---|---|---|
| **Best strict business-hours optimizer** | **Claude Code + Opus 4.6 1M tool setup** | Best objective fit, explicit scoring rule, and strongest 2-of-3 in-hours solution |
| **Best overall value** | **Gemma 4 31B** | Most stable ranking and strongest cost efficiency |
| **Best practical scheduling answer** | **GLM-5 Turbo** | Best real-world compromise when comfort balancing matters more than strict in-hours count |
| **Best polished and most detailed answer** | **GLM-5V Turbo** | Strongest structure and best balanced-compromise framing |
| **Best concise low-cost answer** | **Gemini 3.1 Flash Lite** | Good answer quality at low cost with strong speed |
| **Weakest main recommendation** | **Qwen 3.6 Plus** | Strong supporting analysis undermined by a poor primary meeting slot |

---

## Discussion

### 1. Accuracy was not the biggest differentiator
Most candidate models correctly concluded that a full business-hours overlap is impossible. The larger difference came from how they framed the optimization target.

### 2. The prompt is best read as business-hours-first
The phrase “ideally falling within business hours for all three cities, or as close to business hours as possible” can reasonably be read as:

1. maximize the number of participants inside business hours
2. then choose the least-bad off-hours option among ties

Under that reading, the Claude Code + Opus 4.6 1M tool-assisted response is the strongest objective fit.

### 3. Balanced-compromise answers remain valuable
Even if they no longer rank first under the main benchmark objective, answers from **GLM-5V Turbo** and **GLM-5 Turbo** remain useful because they optimize for human comfort and burden-sharing rather than strict business-hours count.

### 4. Cost did not correlate strongly with quality
The strongest value signal came from **Gemma 4 31B**, not from the most expensive models.

### 5. Evaluator behavior itself is benchmarkable
This mini-study shows that evaluator LLMs are not neutral graders. They import their own preferences:
- GPT-5.4 favors explicit objective matching plus decision-useful optimization framing
- Claude Opus 4.6 favors objective adherence, factual cleanliness, and practical reasoning
- Gemini 3.1 Pro favors optimization explicitness, polished presentation, and document readiness

---

## Key takeaways

1. **No perfect overlap exists** for Brisbane, London, and New York within standard business hours.
2. The prompt is most naturally benchmarked as a **business-hours-first optimization task**.
3. Under that objective, **11 PM Brisbane / 2 PM London / 9 AM New York** is the strongest answer because it maximizes in-hours participation at **2 of 3**.
4. **Claude Code + Opus 4.6 1M tool setup** is therefore the strongest objective-fit response in the set.
5. **Gemma 4 31B** is the strongest all-around value performer among the standalone LLM responses.
6. **GLM-5 Turbo** is the best practical scheduling answer when comfort balancing matters more than strict in-hours count.
7. **GLM-5V Turbo** is the best polished and most analytically complete balance-first answer.
8. **Qwen 3.6 Plus** is the least practical despite strong DST awareness.
9. Evaluator rankings vary meaningfully depending on what they reward.

---

## Final summary

This benchmark demonstrates that even on a relatively simple scheduling task, model evaluation is not just about factual correctness. The central challenge is objective selection: what does “most optimal” actually mean?

Once the task is viewed through that lens, the candidate responses separate into three tiers:

- **Top tier:** Claude Code + Opus 4.6 1M tool setup, Gemma 4 31B, GLM-5 Turbo, GLM-5V Turbo
- **Middle tier:** Gemini 3.1 Flash Lite
- **Lower tier:** Qwen 3.6 Plus

Across the three evaluators, **Claude Code + Opus 4.6 1M tool setup** emerges as the strongest objective-fit model under a business-hours-first reading, **Gemma 4 31B** as the most consistently strong standalone value model, **GLM-5 Turbo** as the best pragmatic scheduler, and **GLM-5V Turbo** as the best polished long-form response.

In short, this was less a benchmark of timezone math than a benchmark of **objective selection, evaluator preference, and practical judgment**.
