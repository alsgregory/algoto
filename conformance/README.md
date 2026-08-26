# Conformance fixtures

A test set for an algoto validator, as plain data — no package to install. An
implementation in any language walks this directory and checks each document
passes or fails as expected.

- `valid/*.json` — documents that must pass the schema.
- `invalid/*.json` — documents that must fail. Each has a sibling
  `*.expected.json` naming the reason and the offending `field`. Assert on
  `field`; treat `reason` as a note for developers.

Schema validation only tells you a document is well-formed. Whether it matches
the tool it describes — its inputs are real parameters, its errors real error
codes — is a check for the tool author's own test suite, against the tool.
