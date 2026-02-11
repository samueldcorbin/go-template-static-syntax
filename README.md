# Go Template Static Syntax

VS Code extension that adds syntax highlighting for `.gohtml` files, with full language support inside `{{define "static-*"}}` blocks.

## Features

- Go template syntax highlighting in `.gohtml` files
- Embedded **CSS** highlighting in `{{define "static-css-*"}}` blocks
- Embedded **JavaScript** highlighting in `{{define "static-js-*"}}` blocks
- Embedded **TypeScript** highlighting in `{{define "static-ts-*"}}` blocks

## Usage

Name your template definitions with the `static-css-`, `static-js-`, or `static-ts-` prefix to get full language support inside the block:

```gohtml
{{define "static-css-main"}}
<style>
  .container {
    display: flex;
    align-items: center;
  }
</style>
{{end}}

{{define "static-js-main"}}
<script>
  document.addEventListener("DOMContentLoaded", () => {
    console.log("loaded");
  });
</script>
{{end}}
```

Blocks without a `static-*` prefix are treated as standard Go template / HTML.

## License

MIT
