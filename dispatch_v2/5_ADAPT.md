# 5_ADAPT.md

How to fork this operating system to a different workstream. The architecture is domain-agnostic; only canon and `domain_rules` are domain-specific.

## what stays unchanged (the invariants)

Copy verbatim from 1_INSTALL.md:
- The XML directive tags: rapid_task_submission, MULTI_TURN_CHAT_QUESTIONING, Always_ask_to_double_check, LEARN_PROTOCOL, TONE_SYNTAX, SEEK_INSIGHT, ACQUIRE_SKILLS, ACCUMULATE, OFFER_WRITE_HANDOFF, ZERO_ASSUMPTIONS, SPEC.MD, skills.md, first_move, goal.
- The mutable_state pattern: spec.md (HOT_CACHE + GRAPH_LINKS + COMPACTION_LEDGER + TASK_QUEUE + INSIGHTS_LEDGER + OPEN_Q + RULES) and skills.md (POINTERS ONLY tree-index).
- The promotion rule: 2+ tasks confirm OR 1 hard-fail = promote.
- The pre-submit gate evolution rule: each hard-fail produces a new rule.
- The metrics ledger schema (turn_ts, task_id, model, outcome, tier_recommend at minimum).
- Three-tier memory: HOT_CACHE / GRAPH_LINKS / COMPACTION_LEDGER.
- Caveman tone, TRUE=1/FALSE=0 turn-ending verdict.

## what you rewrite (the domain layer)

### 1. domain_rules block in 1_INSTALL.md
Replace the rubrics-specific 6 rules with your domain's rules. Examples:

**Code review workstream**:
```
- Test coverage > stylistic preference.
- Atomic commit per change. Multi-concern commits split.
- No force-push on shared branches.
- Reviewer Trust Levels: junior comments = suggestions, senior = blocking.
- CI green > human green. Conflict = block.
```

**Content moderation workstream**:
```
- Policy > user intent.
- Context-class classification before action. Ambiguous class = escalate.
- Two-reviewer concurrence for permanent removals.
- Appeal pathway preserved at every action.
- Audit log entry per decision, immutable.
```

**Customer support workstream**:
```
- Customer stated need > inferred need.
- Verify identity before account action. No exceptions.
- Log every action with timestamp + agent ID.
- Escalate on regulatory keywords (breach, lawsuit, harm).
- Resolve in single thread when possible. Multi-thread = handoff doc required.
```

### 2. canon (read-only reference material)
Replace with your domain's reference docs:
- Domain onboarding / style guide.
- Source-of-truth specification.
- Approved exemplars (1+ per task-type variant).
- Visual framework / protocol image if applicable.

### 3. skills tree
Start empty. Populate as work surfaces patterns. The 9 rubrics-specific sub-skills are NOT portable, but the META-PATTERN is:
- Analysis skills (the coverage_map_method pattern): map all inputs systematically before acting.
- Formatting skills (the cutpaste_row_format pattern): standardize output artifact shape.
- UI-ops skills (the studio_edit_verification pattern): catch interface-level edit gotchas.
- Reverse-engineering skills (the qc_v2_reverse_graph pattern): decode opaque evaluator outputs.
- Decision-tree skills (the atomic_split_decision pattern): codify recurring judgment calls.
- Conflict-resolution skills (the qc_rubric_suggestions_priority pattern): priority rules between disagreeing evaluators.

### 4. pre_submit_gate
Start with empty rules. Each hard-fail you encounter produces a new rule. Bump version each time.

### 5. tasks folder
Start with one approved exemplar per task-type variant. Grow as you complete tasks.

## the 9-step adaptation

### step 1 - clone the skeleton
```
mkdir -p new_workstream/{mutable_state,skills,tasks,canon,session}
cp README.md new_workstream/
cp 2_PLAYBOOK.md new_workstream/
cp 5_ADAPT.md new_workstream/
cp 6_TEMPLATES.md new_workstream/
```

### step 2 - drop empty scaffolds
From 6_TEMPLATES.md, copy the 4 empty scaffolds into new_workstream/mutable_state/:
- spec.md (empty HOT_CACHE, empty INSIGHTS_LEDGER, empty TASK_QUEUE).
- skills.md (empty tree).
- Wiki_Log.md (empty entries).
- metrics_ledger.md (header rows only).

### step 3 - rewrite domain layer in 1_INSTALL.md
- Replace `domain_rules` block.
- Empty `pre_submit_gate` (or carry over architecture-generic rules only).
- Update `goal` (your target number / deadline).
- Save as `new_workstream/1_INSTALL.md`.

### step 4 - install protocol into Claude Project
1. Open Claude Project settings for the new workstream.
2. Paste the code block from `new_workstream/1_INSTALL.md` into "Set project instructions". Save.
3. Upload all `new_workstream/` files into the project so they appear at `/mnt/project/`.

### step 5 - drop in canon
Place your domain reference material into `new_workstream/canon/`. Do not edit.

### step 6 - run first task
1. Start a new chat. First move: `project_knowledge_search "spec.md HOT_CACHE"`. Empty state loads.
2. User provides first task.
3. Run domain-adapted intake (mirror the coverage_map_method pattern if applicable).
4. Mine 1+ insight per turn. Append to spec.md INSIGHTS_LEDGER.
5. End turn TRUE=1 or FALSE=0.

### step 7 - promote first sub-skill (after task 2 or first hard-fail)
1. Insight confirmed by 2+ tasks OR 1 hard-fail surfaces.
2. Create `new_workstream/<snake_case>.md` with full content.
3. Add row to skills.md tree.
4. Reference from pre_submit_gate or workflow checkpoint if applicable.

### step 8 - grow the pre-submit gate
1. Each hard-fail root cause becomes a new pre_submit_gate rule.
2. Bump protocol version (v2.1, v2.2, ...).
3. Regenerate the cutpaste in 1_INSTALL.md.
4. Re-paste into Claude Project settings.
5. Log in spec.md COMPACTION_LEDGER.

### step 9 - verify compounding at task 5
- Check metrics_ledger trend: output_tokens per task should be flat or decreasing.
- Check Sonnet:Opus ratio: should be approaching 3:1.
- Check first-try-approval rate: should be rising.
- If trend is flat or rising with low approval, audit. Likely causes: skills too narrow, pre_submit_gate missing rules, domain_rules underspecified.

## common adaptation mistakes

1. **Inlining content into skills.md**. Defeats context-overload prevention. Always pointers.
2. **Skipping the 75% handoff**. Session boundaries are hard. Context does not persist without explicit handoff files.
3. **Filling pre_submit_gate prematurely with untested rules**. Each rule must be derived from a real hard-fail. Speculative rules produce false-positive blocks.
4. **Using emdashes or non-caveman tone in main chat**. Tone invariant. Violations compound into bloated chats.
5. **Skipping metrics_ledger**. Without telemetry, you cannot verify compounding.
6. **Modifying canon files**. They are source of truth. Disagreements go in spec.md OPEN_Q or a new sub-skill.
7. **Ending a turn without TRUE=1 or FALSE=0**. Ambiguous verdicts accumulate into ambiguous state.
8. **Letting an insight sit past the promotion trigger**. If 2+ tasks confirm or 1 hard-fail surfaces, promote immediately.

## cross-workstream dispatch coordination

Dispatch agents managing multiple parallel workstreams:

**Shared (propagate across workstreams)**:
- XML directive tag set.
- Three-tier memory pattern.
- Promotion rule.
- Pre-submit gate evolution rule.
- Metrics ledger schema.
- First-move sequence.
- TRUE=1 / FALSE=0 invariant.

**Workstream-local (do NOT propagate)**:
- canon contents.
- domain_rules block.
- Specific pre_submit_gate rule contents (each workstream's gate grows from its own hard-fails).
- Task exemplars.
- Sub-skill libraries.

**Update propagation workflow**:
1. Identify workstreams that should receive the update.
2. Bump protocol version in the shared template.
3. For each target: copy new shared layer, preserve their domain_rules block, regenerate their cutpaste, owner re-pastes into Project settings, log update.
4. Audit at 2 weeks: compare metrics_ledger trend before/after to confirm update produced compounding, not regression.

## the philosophy

This system is not magic. It is discipline encoded in files. Compounding comes from:
1. Every insight captured in writing (no memory-only knowledge).
2. Every hard-fail upgraded to a pre_submit gate rule (mistakes become immune systems).
3. Every skill written as a pointer-referenced standalone (context stays lean).
4. Every turn ending with a hard verdict (no drift).
5. Every session boundary handled with explicit handoff (no amnesia).

Copy the discipline, not just the files.

END_ADAPT
