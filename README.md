# academic-deai-writing

English | [中文](README.cn.md) · [Research Skillbox](https://github.com/windyvictor/research-skillbox)

A research-writing revision skill that removes boilerplate, repetition, and template-like phrasing while preserving scientific meaning, evidence strength, and the author's voice.

## Why this skill

Academic prose often sounds machine-made because the argument has been flattened: background expands, technical decisions disappear, and every result receives the same confident tone. Replacing a few words does not fix that. This skill reconstructs the path from **claim → evidence → interpretation → boundary**, then revises the language around that path.

### What you get

- A clean revised draft, not a list of generic style tips
- Preserved numbers, negation, comparisons, citations, conditions, and uncertainty
- Section-aware treatment for Introduction, Results, Discussion, contributions, grants, and English prose
- An optional fidelity audit showing whether the revision changed scientific meaning
- An optional pre-edit diagnosis report (findings, examples, proposed fixes, exclusions) before any rewrite
- A false-positive guard so section numbers, terminology, hedges, and necessary transitions survive

**Workflow:** diagnose the real problem → protect factual anchors → rebuild the argument → revise the prose → compare before and after.

## Use it for

- Revising papers, theses, grant proposals, and research plans
- Cleaning up vague or inflated academic prose
- Rebalancing background and technical explanation
- Revising an Introduction, Results, Discussion, or contribution statement
- Editing English scholarly prose without inventing evidence

This skill does not promise a lower AI-detector score. It evaluates the revision by factual preservation, argument quality, and natural expression. Rewriting does not replace disclosure: ICMJE, COPE, WAME, and the Chinese Academy of Sciences guidance require authors to declare the tools, versions, dates, and purposes of AI use and to take responsibility for the whole manuscript. See `references/evidence-and-policy.md` for sources.

## Contents

- `SKILL.md`: routing, constraints, and delivery rules
- `references/prompts-core.md`: general and constrained revision prompts
- `references/prompts-sections.md`: section-specific workflows
- `references/prompts-english.md`: English academic revision
- `references/preservation-and-evaluation.md`: before/after fidelity checks
- `references/self-check.md`: internal review checklist
- `references/false-positive-guard.md`: disproved "AI tells" and genre exceptions
- `references/diagnosis-protocol.md`: optional pre-edit report, confirmation gate, retest
- `references/evidence-and-policy.md`: detector studies, vocabulary research, disclosure policies
- `evals/`: round-two and round-three behavioral cases

## Core rule

Keep all data, comparisons, negation, conditions, citations, terminology, time status, and uncertainty. Do not turn correlation into causation, a plan into a completed result, or a tentative mechanism into a fact.

## Install

```bash
git clone https://github.com/windyvictor/academic-deai-writing.git
ln -s "$PWD/academic-deai-writing" ~/.agents/skills/academic-deai-writing
```

Use the equivalent skills directory for your agent host.

## Sources and license

MIT. Methodological findings adapted from `lieflat-less-ai-tone` (shiujan, CC BY-NC 4.0) are restated for academic writing; no corpus, scripts, or rule text was copied. Full attribution and external sources are listed in `README.cn.md` and `references/evidence-and-policy.md`. Third-party quotations and source materials remain the property of their respective rights holders.

