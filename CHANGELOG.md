# Changelog

All notable changes to the algoto spec are recorded here. Versions follow
[Semantic Versioning](https://semver.org); the `major.minor` part is the value a
document declares in its `algoto` field.

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
