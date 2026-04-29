# 4_EXEMPLARS.md

3 compressed task examples and the 14 insights mined to date. The examples show pattern-in-action; the insights show what compounded.

## task 614 - Northbridge Memo (Type B: revision/memo)

**outcome**: APPROVED first-try. No surgical fix needed.

**intake**: SP = communications coach. UT-final = revise memo for clarity. 10 pre-populated rubric rows.

**plan**: 4 Modify (atomicity tightening) + 4 Keep + 2 Add (gap fill).

**key pattern**: Type B tasks have most rows already drafted. The work is surgical tightening, not greenfield. K/M/D/A typically heavy on Modify, light on Add.

**lesson**: When intake quality is high, justifications dominate the work. Fewer atomic-split decisions; more justification dedup discipline.

---

## task 720 - Wrestling Event (Type C: hard-fail then surgical recovery)

**outcome**: SUBMITTED v2 SURGICAL FIX after v1 hard-fail. The hard-fail produced 4 insights and bumped protocol v2.0 -> v2.1.

**intake**: SP = event-planning assistant, 5 rules. 5 user turns. 3 event options with conflicting constraints.

**plan v1**: 8 rows. 3 Modify (R1 atomicity split, R3 + R5 specificity), 2 Keep, 3 Add (R6 AEW impractical, R7 departure time, R8 food inclusion).

**failure mode**: Submitted. Auto-QC returned:
- Part 1: 1 fail (R1 still flagged stacked).
- Part 2: 1 fail (NON_REDUNDANCY R1 + R6 overlap).
- Part 3: 3 fails (R3 + R6 justifications verbatim-identical).

**root causes**:
1. R1 criterion text was NOT actually edited in Studio. Writer clicked "Modify" but did not edit the bottom field. Studio shipped row with original (un-modified) text.
2. R3 and R6 justifications shared verbatim quote ("If there is a schedule or budget conflict, point it out clearly"). Part 3 ENGAGEMENT_QUALITY flagged.

**recovery (v2 SURGICAL FIX)**: 3 edits, no row adds/removes:
- R1: criterion text replace.
- R3: justification swap to UT1 budget quote.
- R6: justification swap to UT1 coaching quote.

Re-paste, re-run QC, all-green. Submit.

**insights promoted from this hard-fail**:
- insight 4: studio_modify_text_must_verify -> sub-skill `studio_edit_verification.md`.
- insight 5: justification_dedup_mandatory -> updated `justify_templates_9forms.md` v2 with DEDUP_RULE.
- insight 6: cascading_part1_to_part2_failures -> spec.md rule.
- insight 7: qc_v2_dimension_counts_decoded -> sub-skill `qc_v2_reverse_graph.md`.
- PROTOCOL BUMP: pre_submit_gate v2.1 with rules 1-3 derived from this cycle.

**lesson**: Type C tasks are the ones that grow the system. Each hard-fail is a paid-for insight. The pre-submit gate would have caught all 3 fails if it had existed before this task; v2.1 makes them impossible going forward.

---

## task 883 - LinkedIn Coach (Type D: pre-submit audit catches QC blind spot)

**outcome**: SUBMITTED v2 SURGICAL FIX. Pre-submit audit caught 2 defects that QC v2 missed. Saved 1 iteration cycle.

**intake**: SP = career coach, 3 rules. 5 user turns. UT-final = LinkedIn copy (headline + 3-sentence About + connection note).

**plan v1**: 9 rows. 8 Keep with Form-4 UT-grounded justification-fill + 1 Add (R9 "exactly one headline" singularity check). User pasted, ran QC, ALL-GREEN.

**audit block**: pre-submit checklist halted the Submit click. Two defects surfaced:
1. **R7 atomicity violation**: "Does the response include all three requested achievements: 35% + four integrations + six PMs?" Rubric Suggestions panel: DISCARD + 3 atomic Adds. QC v2 Part 1: PASS via "bundled-instruction exception" (FALSE POSITIVE). Domain rule (atomic_split_decision Q2): items independently failable, must split. Suggestions correct.
2. **R8 justification copy-paste defect**: criterion was about headline tailoring to Nimbus AI role. Saved justification quoted R7's grounding text instead. QC Part 3 PASS because Part 3 regenerates its own rationales per row, does NOT grade saved-text fidelity.

**recovery (v2 SURGICAL FIX)**: 5 edits:
- R7: action Keep -> Discard with reason.
- R8: justification text replace with UT2 platform-launches quote.
- R10/R11/R12: three new Adds for atomic 35% / four integrations / six PMs split.

Re-paste, re-run QC, GREEN: Part 1 15/0/0, Part 2 5/0/0 (all 5 dims ACTIVE PASS), Part 3 11/0/1 (1 structural neutral on discarded R7 rationale). Submit.

**insights promoted from this hard-fail**:
- insight 13: qc_v2_atomicity_blind_spot -> NEW sub-skill `qc_rubric_suggestions_priority.md`.
- insight 14: justification_copy_paste_defect -> rolled into pre_submit_gate manual spot-check rule.
- PROTOCOL BUMP: pre_submit_gate v2.2 with rule 4 (Rubric Suggestions diff).

**lesson**: Type D shows the pre-submit gate is now strong enough to catch failures BEFORE submit. v2.2 catches v2.1 blind spots. Each version is the immune response to the prior version's near-miss.

---

## the 14 insights mined to date

Each insight: short label, one-line summary, promotion status.

| # | label | summary | promotion |
|---|---|---|---|
| 1 | column_d_preferences_scan | Coverage map needs Col D for earlier-turn preferences (taste, comfort, cost). Each EXPLICIT/IMPLICIT/GAP. | folded into coverage_map_method.md step 1 |
| 2 | implicit_chain_coverage_doctrine | A pref is acceptably IMPLICIT only when violation necessarily fails an absorbing row. | folded into coverage_map_method.md |
| 3 | upstream_question_doctrine | UT questions answered upstream do NOT need final-response rationale rows; persistence in final response is the test. | spec.md rule |
| 4 | studio_modify_text_must_verify | Studio Modify shows top=ORIGINAL bottom=SAVED. Click-Modify alone does NOT overwrite. Re-open and verify bottom matches CUTPASTE. | promoted to studio_edit_verification.md (HARD-FAIL grade from 720) |
| 5 | justification_dedup_mandatory | QC Part 3 ENGAGEMENT_QUALITY flags verbatim-identical justifications. | promoted to justify_templates_9forms.md v2 DEDUP_RULE (HARD-FAIL grade from 720) |
| 6 | cascading_part1_to_part2_failures | One Part 1 atomicity fail can cascade into Part 2 NON_REDUNDANCY fail. Fix Part 1 first. | spec.md rule |
| 7 | qc_v2_dimension_counts_decoded | Part 1 = 4 dims, Part 2 = 5 dims, Part 3 = 2 dims + per-criterion. | promoted to qc_v2_reverse_graph.md |
| 8 | bundled_instruction_exception | Single-goal bundles ok in one row; independently-failable items must split. | promoted to atomic_split_decision.md |
| 9 | conditional_row_coverage_gap | "When X, does..." rows pass vacuously if X never occurs. Add inclusion partner row. | promoted to conditional_row_coverage_gap.md |
| 10 | qc_part2_format_drift | Auto-reviewer Part 2 output format non-deterministic between runs. Conclusions stable. Track format mode. | spec.md rule + qc_v2_reverse_graph.md note |
| 11 | two_neutrals_no-d-no-a_acceptable | Plan with 0-Discards AND 0-Adds returns 2 N/A neutrals; structural, not concerning. Refines GREEN-PATTERN. | qc_v2_reverse_graph.md update |
| 12 | keep_justification_fill_default_pattern | When all rows are Keep with placeholder justifications, Form 4 (UT-grounded) is default. Pick distinct UT clause per row. | justify_templates_9forms.md note |
| 13 | qc_v2_atomicity_blind_spot | QC Part 1 false-positive bundled-exception when items independently failable. Rubric Suggestions panel authoritative. | promoted to qc_rubric_suggestions_priority.md (HARD-FAIL grade from 883) |
| 14 | justification_copy_paste_defect | Studio copy-paste of justifications across rows produces wrong-quote defects QC Part 3 misses (regenerates own rationales). | rolled into pre_submit_gate spot-check (HARD-FAIL grade from 883) |

## meta-observation

- Insights 4-7 came from one task (720) hard-fail. Single failure, 4 paid-for lessons.
- Insights 13-14 came from one task (883) pre-submit audit catch. Pre-submit gate caught what QC missed.
- Pattern: each task either confirms existing patterns (regular promotion on 2+ confirms) or surfaces a hard-fail (immediate promotion). System compounds either way.
- The pre_submit_gate is now the highest-leverage artifact. v2.0 had 0 rules. v2.2 has 4 rules + 2 manual checks. Each version catches the previous version's blind spots.

END_EXEMPLARS
