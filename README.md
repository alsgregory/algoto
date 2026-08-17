# algoto

## Creating a schema file

An algoto document is a small JSON or YAML file describing one tool. You can
write it by hand — start from the fields in `algoto.schema.json`, fill in the
ones that apply, and skip the rest (only `algoto` and `name` are required.)

Or point a coding agent at this repository and ask it to fill one in for you,
e.g. *"read the algoto schema and write an algoto document for my `forecast_demand`
tool"*. The `examples/` folder gives it a working template to follow.

## Validating a JSON or YAML file against the schema in Python

Install the dependencies (`pyyaml` is only needed for YAML):

```bash
pip install jsonschema pyyaml
```

Load the schema and your document, then validate. The same code handles both
JSON and YAML — YAML is a superset of JSON, so once parsed both are plain
Python dicts:

```python
import json
import yaml  # only needed for YAML documents
from jsonschema import validate, ValidationError

with open("algoto.schema.json") as f:
    schema = json.load(f)

# For a JSON document use json.load; for YAML use yaml.safe_load.
with open("my_tool.yaml") as f:
    document = yaml.safe_load(f)

try:
    validate(instance=document, schema=schema)
    print("Valid")
except ValidationError as e:
    print(f"Invalid: {e.message}")
```

## Examples

See [`examples/`](examples/) for complete algoto documents. `forecast_demand.algoto.json`
annotates a demand-forecasting tool.
