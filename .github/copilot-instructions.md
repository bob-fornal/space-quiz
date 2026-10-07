# Repository guidance

## Architecture

- The project is a standalone browser app in `index.html`; markup, styles, quiz data, and behavior are kept in that file. There is no framework, package manifest, or build step.
- `quizData` is the source for each question, its ordered answer options, and the zero-based correct-option index. `loadQuestion()` renders the current item and refreshes progress, score, feedback, and navigation.
- Quiz state is held in `currentQuestion`, `score`, `wrongCount`, `answered`, and `answers`. Answer selection, previous/next navigation, completion, and restart are handled by the top-level functions in the inline script.

## Codebase conventions

- Keep changes self-contained in `index.html` unless the project grows a separate concern that warrants its own file. CSS is in the document's `<style>` block; quiz behavior and data are in its `<script>` block.
- Preserve the `prefers-color-scheme` light and dark theme rules. When adding or changing visual styles, check both schemes and keep text readable against its background.
- The UI uses native buttons for answers and navigation. Preserve keyboard operation and disabled states; answer feedback and score changes are rendered into the existing DOM elements.
- The quiz length is currently ten and is referenced in several places, including `answers`, progress calculation, final scoring, and navigation boundaries. If changing the number of questions, update these related values together.
- Responsive adjustments use a `max-width: 480px` media query near the end of the style block.

## Build and validation

- There are no configured build, lint, or automated test commands. Open `index.html` directly in a browser to run the app.
- Playwright MCP is configured in `.vscode/mcp.json` for browser-level smoke tests.
- For a focused manual check, use Tab and Enter to select and navigate; verify one correct and one incorrect answer update the appropriate score and feedback; then finish the quiz and use “Try Again” to confirm results and reset behavior.
