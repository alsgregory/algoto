# Changelog

All notable changes to the algoto spec are recorded here. Versions follow
[Semantic Versioning](https://semver.org); the `major.minor` part is the value a
document declares in its `algoto` field.

## [1.1.1] - 2026-08-24

Documentation and clarifications only; no change to what validates.

### Added
- `conformance/` fixtures: valid/invalid documents (with `.expected.json`
  reasons) and cross-check cases pairing a document with the tool it describes,
  all as plain data so a validator in any language can prove itself without a
  package.

### Changed
- §4 now states which fields reach a model. `_meta` carries the document for
  client code, linters and validators, but current model tool APIs have no
  metadata field, so model-facing fields (`effect`, `interpretation`, error
  `hint`s) must also be surfaced through the tool description or input-schema
  property descriptions. §2 now marks which fields are consumed by client code
  and which by a model.
- Clarified that `requires` names prerequisite tools the agent should call
  first (a data-flow hint), not internal calls or a deployment constraint;
  schema descriptions updated to match.
- §6 now states that a cache over `deterministic` results must include the
  algorithm `version`, so a version bump does not serve stale outputs.
- §1 leads with the checkable-contract benefit (verifiable without an agent)
  and frames the agent-behaviour benefit as intent; a scope line says to
  document tools that run an algorithm, not plain data-access reads.
- §3 notes the token overhead of the structured form over equivalent prose.

## [1.1.0] - 2026-08-19

### Added
- `omission` field on input annotations: describes what the tool does when an
  input is absent — the behavioural consequence, not the raw default value
  (which stays in the tool's own schema). Complements the existing `effect`
  field, which covers what happens when the input *changes*.
- Versioned schema hosting: pinned schemas at `v1.0/algoto.schema.json` and
  `v1.1/algoto.schema.json` so consumers can pin to a specific spec version.
  The root `algoto.schema.json` always tracks the latest.

## [1.0.0] - 2026-08-18

### Added
- Initial algoto spec: the `algorithm`, `inputs`, `outputs`, `guardrails`,
  `execution` and `errors` annotation blocks, with `algoto` and `name` required.
- `uniqueItems` on `requires` and `exclusiveMinimum` on `poll_interval` as basic
  value checks.
- Field-level `examples` drawn from the forecast-demand scenario.
- Top-level `$schema` property so documents can link to the schema for live
  editor validation.
- Composite GitHub Action for package-free validation, plus documented
  `check-jsonschema` pre-commit and CI usage and the `$schema` convention.
- Worked examples under `examples/`: `forecast_demand`, `optimise_route` and
  `moving_average`.
