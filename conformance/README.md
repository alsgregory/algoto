# algoto conformance fixtures

A language-agnostic test set for an algoto validator. Everything here is plain
data — no package, no code, no dependency to install — so an implementation in
any language proves itself by walking this directory and comparing outcomes.

There are two levels, because there are two kinds of check.

## Schema conformance — `valid/` and `invalid/`

These check whether a document is **well-formed** against
[`algoto.schema.json`](../docs/algoto.schema.json). Any JSON Schema 2020-12
validator can run them.

- `valid/*.json` — documents that MUST pass.
- `invalid/*.json` — documents that MUST fail, each with a sibling
  `*.expected.json` describing the failure:

  ```json
  { "reason": "human-readable explanation", "field": "path.to.offending.field" }
  ```

  `reason` is guidance for a human; do not string-match on it. `field` is the
  location a validator should flag — the stable thing to assert on.

Run the schema level with any validator, e.g.:

```bash
# every valid/ document must pass
check-jsonschema --schemafile ../docs/algoto.schema.json valid/*.json

# every invalid/ document must fail
for f in invalid/*.json; do
  case "$f" in *.expected.json) continue;; esac
  check-jsonschema --schemafile ../docs/algoto.schema.json "$f" \
    && echo "SHOULD HAVE FAILED: $f"
done
```

## Cross-checks — `cross-check/`

Schema validation cannot tell whether a document matches the **tool it
describes**. That drift is where real documents go wrong, and catching it needs
the tool's definition alongside the document. Each case is a directory:

```
cross-check/<case>/
  document.json   the algoto document
  tool.json       the tool it annotates
  expected.json   { "passes": false, "reason": "..." }
```

`tool.json` is a minimal, protocol-agnostic description of the tool and its
neighbours:

| Field | Meaning |
|---|---|
| `name` | the tool's real name |
| `parameters` | the parameter names the tool actually accepts |
| `error_codes` | the error codes/conditions the tool can actually emit |
| `server_tools` | the names of the tools present on the same server |

A cross-check validator loads both files and asserts the outcome in
`expected.json`. The cases here cover the two most common joins:

- `phantom-parameter` — an `inputs` key that is not a real parameter.
- `requires-missing-tool` — a `requires` entry naming a tool not on the server.

These are seeds, not the whole space. The same shape extends to the rest of the
document-vs-tool checks — every documented parameter is real *and* every real
parameter is documented, every documented error is one the tool can emit and
vice versa, `name` matches the tool it annotates. Add a directory per case.
