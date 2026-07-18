# CLAUDE.md

   ## Project
   Capstone front-end site(Lwazi AgriCare) built during my internship.

   ## Stack
   - HTML, CSS, vanilla JavaScript
   - Live Server for local development
   - Prettier for formatting, ESLint for linting

   ## Conventions
   - Commit messages follow Conventional Commits (feat, fix, docs, chore, refactor)
   - 2-space indentation
   - Class names use BEM-style naming (block__element--modifier)
   - Source files live under /src

# Project rules

- Clickable card/feature components use real <a href> or <button> elements
  inside semantic lists — never <div onclick>. Keyboard and screen-reader
  access is not optional.
- Any flex/grid row of cards needs a defined mobile breakpoint (this
  project: 600px) that switches to column stacking — verified with a
  Playwright viewport test, not just "looks fine at my window size."
- Decorative icons get aria-hidden="true"; icons that convey information
  need real alt text — checked automatically via axe-core in the test
  suite, not by eyeballing it.