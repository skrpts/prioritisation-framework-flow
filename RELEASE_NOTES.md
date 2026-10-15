# Release Notes

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
