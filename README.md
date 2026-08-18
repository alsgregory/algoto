# algoto — An Algorithmic Agentic Tool Specification

**[Documentation](https://alsgregory.github.io/algoto/)** · **[Schema](docs/algoto.schema.json)**

## Creating a schema file

An algoto document is a small JSON or YAML file describing one tool. You can
write it by hand — start from the fields in `docs/algoto.schema.json`, fill in the
ones that apply, and skip the rest (only `algoto` and `name` are required.)

Or point a coding agent at this repository and ask it to fill one in for you,
e.g. *"read the algoto schema and write an algoto document for my `forecast_demand`
tool"*. The `examples/` folder gives it a working template to follow.

## Validating documents

An algoto document is plain JSON or YAML with a published schema, so you can
validate it without installing algoto.

### In your editor

Link the schema at the top of the document. VS Code and most editors then
validate and autocomplete as you type:

```json
{
  "$schema": "https://alsgregory.github.io/algoto/algoto.schema.json",
  "algoto": "1.0",
  "name": "forecast_demand"
}
```

### On every commit

Add the `check-jsonschema` pre-commit hook:

```yaml
# .pre-commit-config.yaml
repos:
  - repo: https://github.com/python-jsonschema/check-jsonschema
    rev: 0.29.4
    hooks:
      - id: check-jsonschema
        name: Validate algoto documents
        files: '\.algoto\.(json|ya?ml)$'
        args:
          - --schemafile
          - https://alsgregory.github.io/algoto/algoto.schema.json
```

### In CI

Add the bundled action to your workflow:

```yaml
      - uses: alsgregory/algoto/.github/actions/validate@v1.0.0
```

### With pipx

Run the check straight from the command line, nothing to install first:

```bash
pipx run check-jsonschema \
  --schemafile https://alsgregory.github.io/algoto/algoto.schema.json \
  **/*.algoto.json
```

## Examples

See [`examples/`](examples/) for complete algoto documents:

- `forecast_demand.algoto.json` — demand forecasting (prediction)
- `optimise_route.algoto.json` — travelling salesman route optimisation
- `moving_average.algoto.json` — exponential moving average (financial indicator)

## Contributing

Changes to the spec follow [Semantic Versioning](https://semver.org), where the
`major.minor` part is the value a document declares in its `algoto` field:

- **major** — a breaking change: removing or renaming a field, or tightening
  validation so an existing document no longer passes.
- **minor** — a backward-compatible addition: a new optional field or enum value.
- **patch** — wording only (descriptions, examples); nothing that changes what validates.

Bump the `algoto` value and the schema's `$id` on a major or minor change, and
treat a published schema URL as immutable — new versions land as a new file under
`docs/` rather than editing the old one. Record every change in
[CHANGELOG.md](CHANGELOG.md) and tag releases (`vX.Y.Z`).
