---
title: "AI and Developer Productivity"
theme: white
---

# AI and Developer Productivity  
### [Insights from a 2025 RCT Study](https://arxiv.org/pdf/2507.09089)

----

## Study Goal
- Measure the **real-world impact of AI tools** on developer productivity  
- Focus on **experienced open-source maintainers** in large projects  
- Compare:  
  - **AI allowed** (Cursor Pro + Claude 3.5/3.7)  
  - **AI disallowed**  
- Move beyond synthetic benchmarks → **field experiment in practice**  

----

## Study Setup
- 16 experienced open-source developers  
- 246 real issues in large, mature projects (Ø 5 years repo experience)  
- Expectation: 24–39% faster completion with AI  

----

## Main Results
- **Reality: +19% longer completion time with AI**  
- 75% of developers were slower, few saw small speedups  
- Both developers and experts overestimated benefits  
- Perception bias: even after the study, devs *believed* AI sped them up  

----

## Reasons for Slowdown
- **Over-optimism**: using AI even when not helpful  
- **Complexity**: millions of LOC, strict quality standards, many tacit rules  
- **Low reliability**: <44% of AI suggestions accepted  
- **Missing context**: AI lacked implicit repository knowledge  

----

## Key Takeaways
- Benchmarks ≠ Reality: real-world software is far more complex  
- Experts and developers significantly overestimate AI’s impact  
- AI adds extra overhead (review, correction, waiting)  
- Gains are more likely in:  
  - small/greenfield projects  
  - less experienced teams  
  - better-tailored AI tooling  

----

## Critical Reflections
- **Very specific setting**: senior maintainers in large OSS repos  
- **Short tasks (≤ 2h)**: not representative for all development work  
- **Incentives ($150/h)** may have shaped behavior  
- **AI tools** (Claude 3.5/3.7, Cursor Pro) are not the absolute frontier anymore  

----

## Study Criticism
- **Narrow scope**: highly experienced devs in large, mature projects – not generalizable  
- **Task design**: capped at 2h, bias toward “quick wins” where AI adds little  
- **Incentives**: paid by the hour → may reduce pressure to optimize for speed  
- **AI snapshot**: tools were strong in early 2025, but quickly outdated  
- **Experimental bias**: awareness of being in a study could affect AI usage patterns  

----

## Conclusion
- **Today**: AI can *slow down* experienced devs in complex projects  
- **Tomorrow**: with better models, scaffolding, and fine-tuning → real speedups possible  
- Lesson: **field experiments > lab benchmarks**  

----

## Personal Note
- AI is becoming an integral part of software engineering workflows  
- **Risk**: over-reliance on AI in unfamiliar codebases → weaker personal understanding  
- Developers may become **dependent on AI** for navigation and context instead of building deep expertise  
- Balance needed: use AI as *support*, not a crutch  