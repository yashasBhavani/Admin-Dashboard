# AGENTS.md

## What this is

A single-page static admin dashboard mockup. No framework, no build system, no
package.json, no JavaScript, no tests. `index.html` is the only page and the
entrypoint; all styling lives in one CSS file. The working tree matches the
last commit (`71aaffc`).

## Working here

- **Verify in the browser**: open `index.html` directly (no dev server or build
  step exists). Re-check the page visually after CSS or layout changes — there
  is no other way to validate.
- **CSS path gotcha**: the stylesheet link is `Main-Files/styles.css`
  (capitalized directory). Keep the `Main-Files/` path exactly as-is; it is
  case-sensitive and referenced verbatim from `index.html:7`.
- **Single Grid on `body`**: grid-template-areas `"sidebar header"` /
  `"sidebar main"` at `Main-Files/styles.css:53`. `.sidebar` is the left column
  spanning both rows; `.header` and `.content` (grid-areas `header`/`main`) sit
  inside an unstyled `.right` wrapper div (`index.html:29`). Grid placement
  depends on class names, not DOM nesting — the HTML nesting is loose in places
  but works. Don't "clean up" the HTML structure.
- **Classes are the layout contract**: renaming/removing a class in HTML must
  also update selectors like `.header.top`, `.username.logo`, `.div` (matches
  `class="right div"`), `.box.project`, `.trending`, `.secondList` in CSS or
  styles silently drop.
- **Design tokens live in `:root`** at the top of `Main-Files/styles.css:1`.
  `--body-color` / `--dashboard-color` are the page/sidebar backgrounds and
  `--border-color` is the accent. Spacing uses `--gap-size`, not a shared gap
  variable. Prefer the `:root` variables over hardcoded values.
- **Responsive fallback**: the `@media (max-width: 768px)` block at
  `Main-Files/styles.css:368` re-stacks the grid; keep it in sync when editing
  the desktop layout.
