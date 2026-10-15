# Copilot instructions

## Project shape

The application is a standalone static page in `index.html`. Its semantic HTML, responsive CSS, question data, and browser-side JavaScript all live in that file; it has no package manifest, build pipeline, or configured test/lint runner. Open `index.html` directly in a browser to run it.

The quiz flow is data-driven: `questions` stores each prompt, four answer strings, a zero-based `correct` answer index, and an explanation. `renderQuestion()` builds the answer buttons, `selectAnswer()` locks the current question and updates score and feedback, and the Continue handler advances or calls `showResults()`. The results panel replaces the quiz panel; Play again resets the state.

## Commands and verification

There are no configured build, lint, or automated test commands. For a manual browser smoke test, open `index.html` and check that:

- a correct answer increments the score and displays the explanation;
- an incorrect answer leaves the score unchanged and shows the correct answer and explanation;
- progress reaches 10/10 and the results screen reflects the earned score;
- Play again returns to question 1 with a score of zero.

For a single behavior check, exercise that specific answer path in the browser; there is no test runner or per-test command.

## Implementation conventions

- Keep the page self-contained: styles and script are inline, with no external assets or runtime dependencies.
- Keep question content in the `questions` array. `correct` is a zero-based index corresponding to the answer’s position in `answers`.
- Preserve native button controls, semantic headings, live feedback, and the progress bar’s `aria-valuenow`; generated answer text is assigned with `textContent`.
- Use the existing CSS custom properties for both `prefers-color-scheme` themes. Keep motion effects compatible with the `prefers-reduced-motion` override.
- Keep the quiz centered in its narrow responsive layout and use the existing design tokens and feedback states when extending the interface.
