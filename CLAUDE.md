# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

Mason registry for Java development tools. Provides packages for nvim-java that aren't in the official mason-registry. Packages include JDTLS, Spring Boot Tools, Java Test, Lombok, and OpenJDK.

## Development Workflow

No local build/test/lint commands. All validation via GitHub Actions:
- **Registry Lint**: Validates package schemas on PR
- **Package Tests**: Cross-platform CI validation
- **Release**: Auto-triggers on push to `main`

Open PRs early to leverage CI for cross-platform testing. Local testing is complex.

## Package Structure

Each package lives at `packages/<name>/package.yaml`. Required fields:
- `name`: Unique identifier
- `description`: From upstream source
- `homepage`: HTTPS URL
- `licenses`: SPDX identifiers (MIT, Apache-2.0, EPL-2.0, etc.)
- `languages`: Target languages (usually `Java`)
- `categories`: One of LSP, DAP, Formatter, Linter, Runtime, Compiler
- `source`: purl identifier with version (`pkg:<type>/<path>@<version>`)

Optional: `bin` (executables), `share` (arch-independent files), `opt` (add-on content)

## Common Source Types

- `pkg:generic/...` - Direct downloads (jdtls, openjdk)
- `pkg:openvsx/...` - VS Code extensions from OpenVSX
- `pkg:github/...` - GitHub releases
- `pkg:npm/...`, `pkg:pypi/...`, etc.

## Expression Syntax

Dynamic values: `{{variable | filter}}`
Example: `{{ version | strip_prefix "v" }}` transforms `v1.0.0` to `1.0.0`

## Key Files

- `CONTRIBUTING.md` - Complete package specification with examples
- `renovate.json5` - Automatic version updates config
- `.github/workflows/` - CI/CD pipelines

## Schema Validation

Use YAML language server with schemastore: https://json.schemastore.org/mason-registry.json

Integrates with b0o/SchemaStore.nvim for in-editor diagnostics.

## Git Guidelines

Conventional commit messages. Renovate auto-updates package versions.
