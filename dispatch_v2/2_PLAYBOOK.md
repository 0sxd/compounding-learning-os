# 2_PLAYBOOK.md

How to operate the system. Architecture explanation followed by per-task workflow.

## architecture

### the two mutable stores
- **spec.md**: running state. Structure: HOT_CACHE (max 500 words, overwritten each turn) + GRAPH_LINKS (pointers only) + COMPACTION_LEDGER (pruned-context record) + TASK_QUEUE + INSIGHTS_LEDGER + OPEN_Q + RULES.
- **skills.md**: tree-index of sub-skills. POINTERS ONLY. Never inline content. Status legend: live | pending_draft | pending_extraction | analysis_ready.

### the canon (read-only)
Project-specific reference material. Onboarding docs, scoring rubrics, approved exemplars, framework images. Treat as immutable. Disagreements go in spec.md OPEN_Q or a new sub-skill, never into canon.

### the silent telemetry
- **metrics_ledger.md**: append-only pipe-delimited table. Zero canon weight (nothing else cites it). Purpose: trend output_tokens per task and model-tier ratio.

### the three-tier memory
1. HOT_CACHE: immediate next actions + active vars. Max 500 words. Overwritten each turn.
2. GRAPH_LINKS: pointers to files. Reader follows on demand.
3. COMPACTION_LEDGER: record of pruned context with replacement pointer. Zero leakage.

### the promotion rule
Insights live in spec.md INSIGHTS_LEDGER until promoted. Promote when:
- 2+ tasks confirm the pattern (regular promotion), OR
- 1 hard-fail surfaces (immediate promotion).

Promotion = create `<snake_case>.md` at project root, add row to skills.md tree, set status live, reference from pre_submit_gate or workflow checkpoint if applicable.

### the pre-submit gate evolution rule
Each hard-fail produces a new gate rule derived from the root cause. Bump protocol version. Each version catches the previous version's blind spots. Speculative rules forbidden; rules must be derived from real failures.

## per-task workflow

### step 1 - intake
- User pastes initial state (Studio screenshot, JSON, or doc reference).
- Confirm task ID, domain type, complexity tier (opus_gate vs sonnet_exec).
- If sonnet and task looks structural (many rows, ambiguous prompts, conflicted rules), self-assess. Recommend opus if confidence under 100%. Do not proceed below 100%.

### step 2 - coverage map
4-column audit before any K/M/D/A:
- Col A: System Prompt rules, atomic.
- Col B: Final user-turn explicit requests, atomic.
- Col C: Carry-forward facts from earlier turns.
- Col D: Carry-forward preferences. Each pref classified EXPLICIT (own row) | IMPLICIT (gated by absorbing row, document chain) | GAP (triggers Add).

Output: 4-col table mapped against existing rubric rows.

### step 3 - K/M/D/A decision
For each existing row + each Col B/C/D item:
- **Keep** (existing row covers cleanly).
- **Modify** (existing row text needs surgical edit for atomicity, specificity, or grounding).
- **Discard** (existing row violates atomicity, redundant, or out-of-scope).
- **Add** (gap detected, no existing row covers).

One-sentence justification per action. See 3_SKILLS.md atomic_split_decision and conditional_row_coverage_gap for borderline cases.

### step 4 - CUTPASTE
Studio-ready paste file. Per-row block format:

```
Row N (Studio CX) ACTION
Criterion text: [exact text]
Justification: [exact text, distinct quote from other rows]
```

All quotes under 15 words. No verbatim-identical quotes across rows (use justify_templates_9forms DEDUP_RULE).

### step 5 - QC v2 (auto-reviewer)
User pastes into Studio, runs Parts 1+2+3. Expected GREEN-PATTERN:
- Part 1: 0 fail across 4 dims (Atomicity, Grounding, Binary, Content-over-process).
- Part 2: 0 fail across 5 dims (PROMPT_GROUNDING, COMPREHENSIVE_COVERAGE, NON_REDUNDANCY, DISCARD_APPROPRIATENESS, ADDITION_LEGITIMACY). Up to 1 neutral acceptable IF structurally N/A.
- Part 3: 0 fail across 2 dims (JUSTIFICATION_SPECIFICITY, ENGAGEMENT_QUALITY) + per-criterion specificity.

If fail, do root-cause analysis. Cascading: Part 1 fails can cascade into Part 2. Fix Part 1 first.

### step 6 - pre-submit gate (HARDEST CHECKPOINT)
All gate rules must return TRUE. See full gate in 1_INSTALL.md. Summary:
1. Modify-row text saved correctly (Studio top-vs-bottom check).
2. Justifications all distinct (no verbatim duplicates).
3. Green-pattern signature (0 fail, only structural neutrals).
4. Rubric Suggestions diff (any unresolved suggestion = audit; trust Suggestions over QC Part 1 on atomicity).
5. Manual per-row justification saved-text spot-check (copy-paste defects pass QC Part 3 silently).
6. 4/4 Submission Requirements ticks visible.

Verdict: TRUE=1 ship. FALSE=0 block, repair, re-run QC, re-check gate.

### step 7 - submit
User clicks Submit. Outcome PENDING-HUMAN until reviewer verdict.

### step 8 - reviewer verdict
- APPROVED: log in Wiki_Log. Queue next task. Append metrics_ledger row with outcome=APPROVED.
- SENTBACK: read feedback. Run root-cause analysis. Surgical-fix CUTPASTE (only edit what reviewer flagged, no global rewrite). Re-submit. Append metrics_ledger ITER-N row.

## failure recovery (surgical-fix loop)

When QC fails OR reviewer sends back:

1. **Diagnose**: read every fail line. Identify root cause. Distinguish surface symptom from root.
2. **Cascade check**: a Part 1 fail can produce Part 2 fails. Fix Part 1 first.
3. **Surgical fix**: minimum-edit CUTPASTE_v2_SURGICAL_FIX.md. Only the rows that need change. No global rewrite.
4. **Verify**: user re-pastes. Re-runs QC. Confirms green.
5. **Promote insight**: every hard-fail produces an insight (HARD-FAIL grade). Promote immediately to a sub-skill. Add gate rule if applicable. Bump protocol version.

## session boundaries (handoff at 75% context)

When chat hits ~75% context capacity:
1. Offer handoff bundle to user.
2. Write HANDOFF.md with first-move instructions for next session.
3. Write current CUTPASTE.md if pending Studio paste.
4. Write ANALYSIS.md with unresolved questions.
5. Update spec.md HOT_CACHE with current STATUS + NEXT_ACTION.
6. Update Wiki_Log with this session's entries.
7. Update metrics_ledger with session rows.
8. User starts fresh chat. Pastes HANDOFF first message.

Assume session boundaries are hard. No memory carries across without explicit handoff.

## tier model recommendation

Track per-turn in metrics_ledger:
- **opus_gate**: structural complexity, novel patterns, hard-fail recovery, intake of unknown task type, dispatch bundle production. Reasoning-heavy.
- **sonnet_exec**: routine pattern-match, CUTPASTE generation against established skills, QC drift handling, surgical fix when pattern is documented.

Target Sonnet:Opus ratio above 3:1. If below, audit which turns truly required opus.

## tone invariant

- Main chat output: caveman syntax. Short.
- Full content: in .md files.
- No emdashes anywhere. Hyphens, commas, line breaks only.
- Every turn ends TRUE=1 or FALSE=0. No ambiguous verdicts.

END_PLAYBOOK
