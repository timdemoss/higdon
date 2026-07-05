# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

A data-only repository containing a Claude Code plugin marketplace definition. There is no application code, build system, test suite, or linter — every file is a JSON manifest.

## Structure

- `plugins/marketplaces/claude-plugins-official/marketplace.json` — the marketplace index. Its `plugins` array lists plugin IDs and is the source of truth for which plugins the marketplace includes.
- `plugins/marketplaces/claude-plugins-official/plugins/<id>.json` — one manifest per plugin. The filename (minus `.json`) must match both the manifest's `id` field and the entry in `marketplace.json`.

## Plugin manifest conventions

Each plugin manifest wraps an MCP server from https://github.com/modelcontextprotocol/servers and follows a consistent schema:

- Required fields: `id`, `name`, `description`, `version`, `author` ("Anthropic"), `license` ("MIT"), `categories`, `repository`, `mcpConfig`, `requiredEnv`, `tools`.
- Optional fields seen in existing manifests: `icon`, `optionalEnv`, `resources`.
- `mcpConfig` is an `npx -y @modelcontextprotocol/server-<id>` invocation. Secrets are never real values — use placeholders like `<your-github-token>`; path arguments use placeholders like `/path/to/database.db`.
- `requiredEnv` is always present, even when empty (`[]`). Each entry has `name` and `description` (including where to obtain the credential).
- `tools` lists every tool the MCP server exposes, each with `name` and `description`.

## Workflow skills

`.claude/skills/` defines six project skills implementing an "uncover your unknowns" workflow (documented in `docs/unknowns-playbook.md`): `/blindspot`, `/interview`, and `/brainstorm` before building; `/impl-notes` during implementation; `/quiz` and `/explainer` after. Prefer starting nontrivial or unfamiliar work with one of the before-building skills.

## Making changes

- When adding a plugin: create `plugins/<id>.json` following the schema above and add the `id` to the `plugins` array in `marketplace.json`. Both edits are required — a manifest not listed in the index is orphaned.
- Validate JSON after editing: `python3 -m json.tool <file>` (there is no other CI or tooling).
