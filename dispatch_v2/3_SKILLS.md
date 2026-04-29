# 3_SKILLS.md

9 sub-skills, consolidated. Each section is self-contained. Load on-demand by relevance, not all-at-once.

---

## skill 1: coverage_map_method

**purpose**: Audit task inputs systematically before any K/M/D/A action.

**when to load**: every task intake, before deciding actions.

**method**: 4-column table.
- **Col A**: System Prompt rules, atomic. One row per rule.
- **Col B**: Final user-turn explicit requests, atomic. One row per request.
- **Col C**: Carry-forward facts from earlier user turns. One row per fact.
- **Col D**: Carry-forward preferences (taste, comfort, cost-tolerance, style). Each pref classified:
  - **EXPLICIT**: own row covers it.
  - **IMPLICIT**: gated by an absorbing row whose pass logic forces compliance with the pref. Document the chain.
  - **GAP**: no coverage. Triggers an Add row.

**output**: 4-col table mapped against existing rubric rows. Each existing row tagged "covers Col B-3 + Col C-1" or similar. Each unmapped Col B/C/D item flagged for Add or implicit-chain.

**rule**: implicit chain valid only when violation of pref necessarily fails the absorbing row.

---

## skill 2: atomic_split_decision

**purpose**: Decide whether a multi-clause criterion stays bundled or splits into independent rows.

**when to load**: any row with AND, OR, commas joining verbs, or parenthetical expansions. Any row Rubric Suggestions panel flags.

**decision tree**:
- **Q1 - single goal?**
  - YES: bundle ok (anchor: glucose-readings = morning + evening as one reporting goal).
  - NO: split.
- **Q2 - independently failable? (can A pass while B fails?)**
  - YES: split (anchor: deadline + location = 2 independent prohibitions).
  - NO: bundle ok.
- **Q3 - AND vs OR semantics**
  - "A and/or B" alternative methods to one goal: bundle ok.
  - "A and B" both required: split.

**hard rule from task 883**: When Rubric Suggestions panel disagrees with QC v2 Part 1 on atomicity, Suggestions is authoritative. See skill 8.

**precedent splits**: task 443 split shellfish + budget + Ayutthaya + Siem Reap + luxury-avoid + street-food into 6 Adds. Task 883 split 35% + four-integrations + six-PMs into 3 Adds.

---

## skill 3: conditional_row_coverage_gap

**purpose**: Detect "When X, does..." rows that pass vacuously when X never occurs.

**when to load**: any row beginning with "When", "If", "Where", or any conditional clause.

**check**: Does the final user turn explicitly demand X?
- YES: add an explicit inclusion partner row that tests X is present.
- NO: conditional row stands alone.

**example**: Row "When the response includes restaurant suggestions, does it mention shellfish-free options?" passes vacuously if the response omits restaurant suggestions. If final UT demands restaurant suggestions, add inclusion partner row "Does the response include restaurant suggestions?"

---

## skill 4: cutpaste_row_format

**purpose**: Studio-ready paste file. One row block per rubric row.

**format per row**:
```
Row N (Studio CX) ACTION
Criterion text: [exact text to paste into Criterion field]
Justification: [exact text to paste into Justification field]
```

Where:
- N = row number in the writer's plan (1, 2, 3, ...).
- CX = corresponding row in the original Studio rubric (C1, C2, ... or "new").
- ACTION = Keep | Modify | Discard | Add.

**footer**: Studio entry order checklist (which rows to enter first, which to verify post-save).

**rules**:
- All criterion text and justification text quoted exactly. No paraphrasing in CUTPASTE.
- All quotes inside justifications under 15 words.
- All justifications use distinct quote anchors (no verbatim duplicates across rows).

---

## skill 5: justify_templates_9forms

**purpose**: 9 canonical one-sentence justification templates. DEDUP_RULE prevents Part 3 ENGAGEMENT_QUALITY false-positives.

**forms**:
1. **Add, UT-grounded**: 'This criterion is included as a fulfillment of a key prompt request: "[exact UT quote under 15 words]."'
2. **Add, SP-grounded**: 'This criterion enforces a system-prompt rule: "[exact SP quote under 15 words]."'
3. **Modify, atomicity-fix**: 'This criterion is modified to test only [single check] because the original bundled [list], violating atomicity.'
4. **Keep, UT-grounded**: 'This criterion is included as a fulfillment of a key prompt request: "[exact UT quote under 15 words]."'
5. **Keep, SP-grounded**: 'This criterion enforces a system-prompt rule: "[exact SP quote under 15 words]."'
6. **Discard, atomicity**: 'This criterion is discarded because it bundles [N] independently-failable items, violating the atomicity rule; it is replaced by [N] atomic criteria.'
7. **Discard, redundancy**: 'This criterion is discarded because it duplicates Row [X] without adding distinct test coverage.'
8. **Discard, out-of-scope**: 'This criterion is discarded because it tests a behavior the user did not request.'
9. **Modify, specificity-fix**: 'This criterion is modified to match the prompt's exact specificity: "[user quote]" rather than the original generalized phrasing.'

**DEDUP_RULE**: No two justifications in the same task may share verbatim quote text. If two rows would naturally cite the same source quote, pick one for that quote and force the other to a different anchor.

---

## skill 6: studio_edit_verification

**purpose**: Catch the single most common Modify-row defect.

**the trap**: Studio Modify rows display two stacked text lines:
- **Top line**: ORIGINAL criterion text. Display only. Immutable.
- **Bottom line**: CURRENT SAVED text. Editable.

Clicking "Modify" alone does NOT overwrite the bottom line. Writer must explicitly edit the bottom field. If they skip the edit, the row ships with original text. QC v2 Part 1 reads bottom line, flags as un-modified.

**procedure**:
1. After every Modify edit, re-open the row.
2. Confirm bottom line matches the CUTPASTE REPLACE target verbatim.
3. If bottom == top, the edit was missed. Re-edit. Re-save. Re-verify.

**hard-fail origin**: task 720 Row 1 shipped without text replace, cascaded into Part 1 atomicity fail + Part 2 NON_REDUNDANCY fail.

---

## skill 7: qc_v2_reverse_graph

**purpose**: Decoded structure of the Studio QC v2 auto-reviewer. Use to predict pass/fail.

**Part 1 - Criteria** (4 dimensions):
- ATOMICITY: each row asks one binary question. Bundled exception applies for single-goal bundles.
- SELF_CONTAINMENT (GROUNDING): every value in criterion appears in user turns or system prompt. No model-generated content hard-coded.
- OBJECTIVE_EVALUABILITY (BINARY): exact counts, exact strings, name-presence checks, "at least one of" topic checks. No subjective language.
- CONTENT_OVER_PROCESS: criterion checks what response contains, not how model produced it.

**Part 2 - Prompt-Rubric** (5 dimensions):
- PROMPT_GROUNDING: criteria match prompt specificity.
- COMPREHENSIVE_COVERAGE: all explicit final-turn requirements covered.
- NON_REDUNDANCY: no two criteria mechanically overlap.
- DISCARD_APPROPRIATENESS: every Discard either replaced by atomic split or genuinely out-of-scope. N/A if no Discards.
- ADDITION_LEGITIMACY: every Add traces to a final-turn directive. N/A if no Adds.

**Part 3 - Justifications** (2 dimensions):
- JUSTIFICATION_SPECIFICITY: each row's justification cites a specific user phrase or SP rule.
- ENGAGEMENT_QUALITY: justifications differentiated. Verbatim duplicates across rows = fail.

**GREEN-PATTERN signature**:
- 0 fail across all 3 parts.
- Up to 1 neutral on Part 2 acceptable IFF DISCARD_APPROPRIATENESS or ADDITION_LEGITIMACY = N/A from no-discard/no-add plan.
- 0-Discards AND 0-Adds plans return 2 N/A neutrals - structural, acceptable.
- 1 neutral on Part 3 acceptable when discarded-row rationale generation surfaces the discard reason.

**format drift caveat**: Part 2 output format can shift between prose-per-requirement and dimension-header-per-verdict between runs without state change. Conclusions are stable; counts can shift. Track format mode alongside counts.

---

## skill 8: qc_rubric_suggestions_priority

**purpose**: Resolve conflicts between Studio's Rubric Suggestions panel and QC v2 Part 1 on atomicity.

**the priority rule**: When Rubric Suggestions panel and QC v2 Part 1 disagree on atomicity, Rubric Suggestions is AUTHORITATIVE. Submit plan must match Rubric Suggestions, regardless of QC green.

**root cause of QC false-positive**: QC v2 Part 1's "bundled-instruction exception" was designed for single-goal bundles (glucose-readings pattern: morning and evening are facets of one reporting goal). Auto-reviewer applies this exception too liberally whenever N items trace to a single user-turn quote, even when items are independently failable. Rubric Suggestions operates from strict atomicity, no exception.

**case study (task 883)**: Row 7 "Does the response include all three requested achievements: 35% + four integrations + six PMs?" - QC Part 1 PASS via bundled-exception, Suggestions DISCARD + 3 atomic Adds. Suggestions correct. Atomic_split_decision Q2 confirms (response could mention 2 of 3 and fail only the third).

**pre-submit checklist**:
1. Open Rubric Suggestions panel in Studio.
2. Diff every suggestion against current plan.
3. If suggestion is DISCARD + split and current plan keeps the bundled row: audit via atomic_split_decision.
4. If items independently failable: match the Suggestion. Discard. Add atomic splits.
5. Submit only after all suggestions resolved OR explicitly dismissed with documented Writer Comment.

**meta-pattern for other domains**: Any workstream with both an auto-reviewer AND a separate suggestions panel evaluating the same artifact must establish a priority rule. Default: more conservative panel is authoritative when they disagree. Auto-reviewers that reason about exceptions are prone to over-application.

---

## skill 9: rubric_correction_simulated_diagnostic

**purpose**: Offline mental-run QC checklist. Use when no Studio access or pre-CUTPASTE sanity check.

**6 Critical Scorecard characteristics** (each row tested):
1. Grounded in prompt (SP or UT, exact quote available).
2. Atomic (single binary question).
3. Objective (binary-gradable from response text alone).
4. Content-focused (tests output, not process).
5. Specific (matches prompt's exact specificity, not generalized).
6. Non-redundant (does not duplicate another row's test).

**3 Non-critical Scorecard characteristics**:
7. Justification cites distinct quote.
8. Action (K/M/D/A) matches the underlying logic.
9. Coverage gaps from earlier turns audited.

**Trinity Dialectic mapping**: each row defended on Logos (logical structure), Pathos (user need served), Ethos (alignment with rubric correction discipline).

**output**: green/yellow/red verdict per row + per characteristic. Fix yellows + reds before CUTPASTE.

END_SKILLS
