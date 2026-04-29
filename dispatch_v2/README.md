# README.md

Compounding-learning operating system for iterative task workflows. Portable. Domain-agnostic core.

Origin: Mercor Rubrics Correction project, captured 2026-04-21 after 4 tasks (2 approved, 2 submitted, 2 hard-fail-then-recovery cycles).

## what this is

7 files. Total under 50 KB. Read in order. Each teaches one aspect.

```
README.md        you are here. 5 min read.
1_INSTALL.md     the protocol cutpaste block + where to paste it.
2_PLAYBOOK.md    architecture, per-task workflow, pre-submit gate, failure recovery.
3_SKILLS.md      9 reusable sub-skills, consolidated.
4_EXEMPLARS.md   3 compressed task examples + 14 insights mined to date.
5_ADAPT.md       9-step fork to other workstreams.
6_TEMPLATES.md   empty scaffolds for spec, skills, wiki_log, metrics.
```

## quick start (adopt as-is)

1. Read 2_PLAYBOOK.md. Understand the loop.
2. Open Claude Project settings. Paste the code block from 1_INSTALL.md into "Set project instructions". Save.
3. Drop empty scaffolds from 6_TEMPLATES.md into your project as `spec.md`, `skills.md`, `Wiki_Log.md`, `metrics_ledger.md`. Or copy your existing ones if continuing.
4. Start chat. First move: `project_knowledge_search "spec.md HOT_CACHE"`. State loads.
5. Run task per playbook. End every turn TRUE=1 or FALSE=0.

## quick start (fork to a new domain)

1. Read 5_ADAPT.md.
2. Keep the invariant architecture (XML directive tags, mutable_state pattern, pre_submit_gate evolution rule).
3. Rewrite the `domain_rules` block in 1_INSTALL.md for your domain.
4. Replace the rubrics-specific examples with your own.
5. Start with empty pre_submit_gate. Each hard-fail adds a rule.

## the philosophy in 5 lines

1. Every turn ends TRUE=1 (ship) or FALSE=0 (ask, block).
2. Caveman in chat. Full content in .md files.
3. Insights captured every turn, promoted to skills on 2 confirms or 1 hard-fail.
4. Pre-submit gate grows incrementally: each hard-fail produces a new rule.
5. Skills tree holds POINTERS only, never inline content. Context stays lean.

## what good looks like at 100 tasks

- 15+ live sub-skills. Pre-submit gate at v3.x with 6-8 rules.
- output_tokens per task trending down 40 percent from baseline.
- Sonnet:Opus ratio above 3:1.
- First-try-approval rate above 85 percent.

END_README
