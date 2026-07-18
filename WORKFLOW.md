# Workflow Comparison: Core Features Section

## Round 1 (vague prompt)
Prompt: "Add a flexbox section with three items to my landing page."

## Round 2 (precise prompt)
Prompt:  "Add a 'Core Features' section to index.html, styled in css/styles.css, matching the existing color palette and font defined there. Three cards in a flexbox row: Cattle Farming, Vaccination Schedules, Sheep and Goat Farming — each a full <a href> linking to its section anchor, wrapped in a semantic list (<ul>/<li>), not <div onclick>. Requirements: color scheme should be dark green, medium green, walnut brown, sand and light gray. The cards must be equal height regardless of text length (use align-items: stretch); below 600px viewport width, switch to flex-direction: column full-width stacking; icons are decorative and need aria-hidden="true"; links need a visible :focus outline; text/background contrast must meet WCAG AA (4.5:1). Example: at 375px width, cards should stack vertically at 100% width with 16px gap. Plan your approach first, then implement, then write Playwright tests that check (1) three cards render as real anchor tags with hrefs, (2) at a 375px viewport the layout stacks vertically, (3) an axe-core scan reports no accessibility violations. Run the tests and show me the output before I review."

## Core Features Section — Round 1 vs Round 2

### Correctness
Round 1 (one-line prompt) produced three flex items with no breakpoint and no real link behavior — the cards were bare <div>s, so clicking did nothing. Round 2  produced real <a href> cards linking to the correct page anchors, confirmed by a Playwright test asserting three anchor elements with valid href values.

### Accessibility
Round 1's divs had no keyboard focus path, and the decorative icons had no aria-hidden, both accessibility failures. Round 2 initially failed its own axe-core test for that same missing aria-hidden attribute — caught from the test output, not by eyeballing the page — then passed after the fix. Round 2 also added visible :focus outlines that round 1 lacked entirely.

### Edge cases
Testing a card with a much longer description exposed the gap: round 1's flexbox let that card grow taller than its neighbors, breaking row alignment. Round 2 used align-items: stretch, kept equal card heights regardless of content length, and included a 375px-viewport stacking test from the start.

### Review effort
Round 1 took about 5 minutes total but shipped broken — no keyboard access, uneven card heights, dead links. Round 2 took about 14 minutes, including one failing test and a fix, but needed no further debugging afterward. The extra upfront time bought a feature that was actually verified working, not just visually plausible.

## Takeaway
Round 2 took longer up front but produced a feature I didn't have to
personally debug — round 1's output looked done but wasn't.