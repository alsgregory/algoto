# Changelog

All notable changes to the algoto spec are recorded here. Versions follow
[Semantic Versioning](https://semver.org); the `major.minor` part is the value a
document declares in its `algoto` field.

## [1.0.0] - 2026-08-17

### Added
- Initial algoto spec: the `algorithm`, `inputs`, `outputs`, `guardrails`,
  `execution` and `errors` annotation blocks, with `algoto` and `name` required.
- `uniqueItems` on `requires` and `exclusiveMinimum` on `poll_interval` as basic
  value checks.
- Field-level `examples` drawn from the forecast-demand scenario.
- `examples/forecast_demand.algoto.json` as a worked example.
