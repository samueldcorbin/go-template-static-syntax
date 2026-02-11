# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a VS Code extension that provides syntax highlighting for `.gohtml` files (Go HTML templates). Its key feature is embedded language support for CSS, JavaScript, and TypeScript inside specially-named `{{define}}` blocks.

## Architecture

The extension consists of three files:

- **`package.json`** — Extension manifest. Registers the `gohtml` language, associates it with `.gohtml` files, and declares the TextMate grammar with embedded language mappings (`meta.embedded.block.css`, `meta.embedded.block.javascript`, `meta.embedded.block.typescript`).
- **`language-configuration.json`** — Bracket matching and auto-closing pairs for Go template delimiters (`{{`/`}}`), HTML tags, and standard brackets/quotes.
- **`syntaxes/gohtml.tmLanguage.json`** — TextMate grammar definition. This is the core file.

## Grammar Design

The TextMate grammar (`text.html.gohtml`) layers on top of `text.html.basic` and defines these repository patterns:

- **`comment-block`** — Matches `{{/* ... */}}` Go template comments
- **`css-block`** — Matches `{{define "static-css..."}}...{{end}}`, embeds `source.css`
- **`js-block`** — Matches `{{define "static-js..."}}...{{end}}`, embeds `source.js`
- **`ts-block`** — Matches `{{define "static-ts..."}}...{{end}}`, embeds `source.ts`
- **`go-template-tag`** — Matches generic `{{ ... }}` template expressions

The naming convention for embedded blocks is `static-css`, `static-js`, or `static-ts`, optionally followed by a suffix (e.g., `static-css-reset`). The regex pattern is `static-css(?:-[^"]*)?`. Go template tags are also recognized inside embedded blocks, so `{{ .Variable }}` inside a CSS block won't break highlighting.

## Development

No build step is required. To test, open this folder in VS Code and press F5 to launch the Extension Development Host. There are no tests, linting, or CI configured.
