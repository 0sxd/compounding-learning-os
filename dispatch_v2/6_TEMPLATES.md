# 6_TEMPLATES.md

Empty scaffolds. Copy-paste these into your project as starting state. Each is one section below.

---

## scaffold 1: spec.md

```markdown
# spec.md | CANONICAL HANDOFF & COM. STREAM

<zero_bloat_protocol>
Assume each turn is terminal. Do not retain chat history.
Execute all state-saves directly to spec.md using strict structured fields.
Maintain 3-tier memory architecture:
  1. HOT_CACHE: max 500 words. Immediate next actions + active vars only.
  2. GRAPH_LINKS: minimalist pointers to external files/skills. No inline content.
  3. COMPACTION_LEDGER: record of hard-pruned context. Zero token leakage.
Main chat output: cave-man syntax only.
</zero_bloat_protocol>

---

## HOT_CACHE
<!-- max 500 words | next actions + active vars | overwrite each turn -->

STATUS: initialized.
SESSION_TYPE: project bootstrap.
ACTIVE_TASK: none.
NEXT_ACTION: await first task intake.

ACTIVE_VARS:
- (empty)

CONFIDENCE: TRUE=1 for empty-state initialization. FALSE=0 on any task-specific verdict until first task arrives.

---

## GRAPH_LINKS
<!-- pointers only, no inline content -->

- protocol_canon: project://1_INSTALL.md
- skill_tree: project://skills.md
- wiki_log: project://Wiki_Log.md
- metrics_ledger: project://metrics_ledger.md

---

## COMPACTION_LEDGER
<!-- record of pruned content with replacement pointer -->

- (empty)

---

## TASK_QUEUE
- (empty)

---

## INSIGHTS_LEDGER
<!-- 1 pattern minimum per turn. Promote to skills.md when 2+ tasks confirm OR 1 hard-fail. -->

- (empty)

---

## OPEN_Q
- (empty)

---

## RULES

### protocol (from 1_INSTALL.md v1.0)
- (rewrite with your domain rules)

### pre-submit gate rules
- (start empty; each hard-fail adds a rule)

### coverage rules
- (workstream-specific intake rules)

---

## file registry

<canon_read_only>
- (your canon files)
</canon_read_only>

<mutable_self_evolving>
- state: spec.md (this file)
- skill_tree: skills.md
- wiki_log: Wiki_Log.md
- protocol_canon: 1_INSTALL.md
- telemetry: metrics_ledger.md
</mutable_self_evolving>

---

## user preferences

<user_preferences>
- No emdashes. Hyphens, commas, line breaks only.
- Remember Protocol and Goal.
</user_preferences>

---

## first move every new chat

<first_move>
1. project_knowledge_search "spec.md HOT_CACHE" to load current state.
2. Read skills.md tree-index. Load only the sub-skill relevant to the turn.
3. Pre-output eval: TRUE=1 acts, FALSE=0 asks up to 3 Qs.
4. If session is sonnet and task looks structural, self-assess. Recommend opus if confidence under 100%.
</first_move>

---

## goal

<goal>
(your domain-specific goal: target task count, deadline, success rate)
</goal>

END_SPEC
```

---

## scaffold 2: skills.md

```markdown
# skills.md | <workstream-name> skill tree
# POINTERS ONLY. NO INLINE CONTENT.

## read_protocol (mandatory)
1. Read THIS file first to discover available sub-skills.
2. Load only the sub-skill relevant to the current move. Do NOT preload.
3. Max 1 sub-skill per turn unless user explicitly requests more.
4. If sub-skill is STATUS: pending, note in spec.md OPEN_Q, do not invent content.
5. After task closes, promote new patterns via insight_promotion rule (2+ tasks OR 1 hard-fail).

## status legend
- live: file exists in project, content ready.
- pending_draft: registered but not yet written. Do not hallucinate.
- pending_extraction: content lives in canon, needs distillation to its own .md.
- analysis_ready: inputs staged, awaiting processing.

## tree

### core
| slug | summary | path | status |
|---|---|---|---|
| (empty) | | | |

### analysis
| slug | summary | path | status |
|---|---|---|---|
| (empty) | | | |

### formatting
| slug | summary | path | status |
|---|---|---|---|
| (empty) | | | |

### ops (UI / tool / workflow procedures)
| slug | summary | path | status |
|---|---|---|---|
| (empty) | | | |

### reverse_engineering
| slug | summary | path | status |
|---|---|---|---|
| (empty) | | | |

### session_ops
| slug | summary | path | status |
|---|---|---|---|
| (empty) | | | |

## registry rules
- New sub-skill = new row here + new <snake_case>.md file at project root.
- Row fields: slug, summary (<=12 words), path, status.
- Slug = snake_case, matches filename without .md.
- No inline content in this file.
- Status transitions: pending_draft -> live (on file write).
- Deprecate: move obsolete row to archive section at bottom.

## archive
- (none)

END_SKILLS
```

---

## scaffold 3: Wiki_Log.md

```markdown
# Wiki_Log.md

Chronological append-only record. Most recent at bottom.

## [DATE] init | <workstream-name> bootstrapped
Cloned from compounding-learning OS dispatch bundle. domain_rules rewritten for <workstream>. pre_submit_gate empty. canon dropped in.

## [pending] first task intake
Trigger: first user task arrives.

END_WIKI_LOG
```

---

## scaffold 4: metrics_ledger.md

```markdown
# metrics_ledger.md | silent telemetry | zero canon weight
# Append-only. Purpose: trend output_tokens per task + sonnet:opus ratio.

## legend

- turn_ts: ISO timestamp.
- task_id: numeric task ID.
- turn_number: 1-indexed within the task's chat.
- model: opus | sonnet | haiku.
- input_tokens_est: chars(input) / 4.
- output_tokens_est: chars(Claude output) / 4.
- out_in_ratio: output / input.
- outcome: TRUE1 | FALSE0 | PENDING | ITER-N | APPROVED | SENTBACK.
- tier_recommend: opus_gate | sonnet_exec.
- notes: free-text key signals.

## success-eval rule
Rolling avg last 3 completed tasks' output_tokens vs prior 3.
Trending down + approval stable-or-rising = TRUE=1 compounding.
Flat-or-rising = FALSE=0, audit non-reducing skill or wiki bloat.
Sonnet:Opus target ratio >= 3:1.

---

## rows

| turn_ts | task_id | turn_number | model | input_tokens_est | output_tokens_est | out_in_ratio | outcome | tier_recommend | notes |
|---|---|---|---|---|---|---|---|---|---|
| (first row appended at first turn) | | | | | | | | | |

END_LEDGER
```

---

## scaffold 5: Wiki_Index.md (optional but recommended)

```markdown
# Wiki_Index.md

Updated: [DATE]

## Protocol (canon)
- [[1_INSTALL.md]] paste-ready protocol for Claude Project settings.
- [[2_PLAYBOOK.md]] architecture + per-task workflow.
- (your domain canon files)

## State (mutable)
- [[spec.md]]
- [[skills.md]]
- [[metrics_ledger.md]]

## Skills (live)
- (populated as skills promote)

## Tasks
- (populated as tasks complete)

## Log
- [[Wiki_Log.md]]

END_WIKI_INDEX
```

---

## installation order

1. Create the 5 files above in your project's root.
2. Drop your canon reference material into a `canon/` folder.
3. Open Claude Project settings, paste 1_INSTALL.md code block, save.
4. Start chat. First-move: `project_knowledge_search "spec.md HOT_CACHE"`. Empty state loads.
5. Begin first task.

END_TEMPLATES
