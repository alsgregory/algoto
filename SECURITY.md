# Security Policy

## Reporting a Vulnerability

If you discover a security issue in the algoto schema or documentation, please report it privately by emailing **alastair@twentyfirstgroup.com**.

Do not open a public issue for security vulnerabilities.

## Scope

This repository contains a JSON Schema specification and static documentation. There is no server-side code, no dependencies, and no user input handling. Security concerns are most likely to involve:

- Malicious content injected via pull requests
- Issues in the JSON Schema that could cause validation bypass
