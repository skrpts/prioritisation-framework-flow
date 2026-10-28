# Release Notes

## v1.1.28
GH#1045 — run the two scoring frameworks this pipeline is named for. `ice-evaluator` and `moscow-classifier` shipped declared and uninvoked, so a package whose description promises "RICE, ICE and MoSCoW scoring" applied only RICE, and the trade-off analysis that is documented to "compare rankings across all three frameworks" compared one.

Stage 2's prose specifies all three sub-stages on the `scoring-model-application` skill, which RICE already occupies; two entries on one skill slug share its title, so each got its own backing skill (`ice-scoring`, `moscow-classification`) and Stage 2 is now the `parallel:` block the documentation describes. Each member binds `backlog` ← Backlog Normalisation — the entry preceding the block, never a sibling, since parallel members run concurrently.

THREE silently-wrong values fixed along the way, none of which any rule flags, because a reference that resolves is not an error even when it resolves to the wrong artefact. `ice-evaluator` read `{{steps.previous.output}}` under BOTH "Normalised backlog" and "RICE scores (if already calculated)", so it received the backlog where RICE scores belonged; its own framework does not depend on RICE, so that reference is removed rather than bound to something it does not mean. `moscow-classifier` did the same across three labels. Worst was `prioritisation-report-generator`, the step that exists to "combine all framework results": it read `{{steps.Scoring Model Application.output}}` THREE times, under "RICE scoring results", "ICE scoring results" and "MoSCoW classification results" — so the report compared RICE against itself twice and never saw the other two frameworks at all. Each is now a declared slot bound to the stage that produces it. Its fourth input asked for "Trade-off analysis (if available)" via `{{steps.previous.output}}` while running AS the trade-off-analysis step, and `previous` is undefined after a parallel block in any case; removed.

MoSCoW is sequenced AFTER the RICE/ICE block rather than inside it. Stage 2's prose asks for all three in parallel while Stage 2c's own bullets require cross-referencing the RICE and ICE rankings, and those cannot both hold: a parallel member cannot consume a sibling's output, and the engine refuses a referenced slot that nothing binds (`execution_context_missing_binding`). MoSCoW genuinely depends on the other two, so it is not a true sibling — the cross-check is kept and the parallelism narrowed to the two framework scorers that are actually independent. `ice-evaluator` read `{{steps.previous.output}}` under BOTH "Normalised backlog" and "RICE scores (if already calculated)", so it received the backlog where RICE scores were expected; `moscow-classifier` did the same across three labels. Both prompts mark the cross-framework scores OPTIONAL in their own text ("if available"), which resolves the apparent contradiction between running the sub-stages in parallel and cross-referencing each other's output: the slots are declared `required: false` and left unbound, so they are correctly absent rather than silently holding the wrong artefact. Stage 3 now binds all three framework outputs explicitly. Skills 3→5, total 12→14.

## v1.1.27
GH#1100 consumer wave (batch 2) — declare the data flow this workflow was resolving positionally.

Each stage below now receives its input through a declared `bindings:` entry instead of `default_from_previous`, which K-073 revoked. **The value is unchanged**: every binding names the step that immediately precedes it, which is exactly what the positional default resolved to. What changes is that the dependency is stated rather than inferred from position, so a reorder can no longer silently feed a stage the wrong artefact.

Bindings added:
  `risk-assessment-prompt` ← `from_step: "Trade-off Analysis"` (step 4)
  `polish-language` ← `from_step: "Risk Assessment"` (step 5)

Dependency pins moved to the published versions that declare these slots:
  `company-okrs` 1.0.1 → 1.0.3
  `language-polish` 1.0.1 → 1.0.3
  `llm-service` 1.0.1 → 1.0.3
  `polish-language` 1.0.1 → 1.0.7
  `risk-assessment` 1.0.1 → 1.0.3
  `risk-assessment-prompt` 1.0.1 → 1.0.3

## v1.1.26
GH#1045 — Stage 1 now runs. The backlog intake and normalisation stage was documented but nothing invoked it, so the pipeline began at RICE scoring on whatever raw backlog you pasted in.

The stage's prompt shipped with the package from the start and is unchanged; what was missing was anything to run it. It now normalises each backlog item into a consistent structure, carries your existing priority labels through verbatim, and flags items that lack enough detail to score rather than scoring them on guesswork.

**Still incomplete, and this is the honest part.** The description promises RICE, ICE and MoSCoW. Only RICE runs. The ICE and MoSCoW prompts ship, and their stages are documented as running in parallel with RICE — but all three are documented against a single skill, and a skill runs one prompt, so two of the three cannot be reached. That needs an engine change (GH#1092), not a content fix. Until then this skrpt applies one framework of the three it names.

## v1.1.25
GH#745 — declare per-step `output: {name, type}` on every execution step (scores/text, prioritisation_report/text, risk_assessment/text, polished_report/text). Lights up the #744 rich flow-map. Content-only; no bindings or logic changes.

## v1.1.24
GH#645 Row 3b — migrate to K-037 dep-referenced schema. Strip 6 inline shared-content files and declare 6 hub-shared deps (UUID id + slug name + version + checksum from `gen-dep-checksums.mjs`). Closes pre-Step-3 inline-vendoring for this bundle.

## v1.1.23
Wave 2: re-signed with canonical engine signing pipeline.

## v1.1.22
Tags migrated inline into manifest (GH#586). tags.yaml retired.

## v1.1.21
Bundle re-signed with canonical engine signing pipeline (Wave 2 migration).

## v1.1.20
Signature fix — RELEASE_NOTES.md now included in integrity checksum.

## v1.1.19
Initial catalog release with full structural and content-quality validation. All scanner checks pass.
