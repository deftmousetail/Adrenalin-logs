# Contributing

Thanks for helping improve AMD Adrenalin CSV Reader.

## Ways to contribute

- Report a reproducible bug
- Suggest a focused feature
- Improve browser, keyboard, or mobile behavior
- Improve CSV compatibility
- Improve documentation or accessibility

## Development workflow

1. Fork this repository.
2. Create a branch with a short descriptive name.
3. Edit `index.html`.
4. Test the complete reader locally in a modern browser.
5. Open a pull request explaining the change and how you tested it.

There is no build step or dependency installation. The application is intentionally kept as a single portable HTML file.

## Testing checklist

Before submitting a pull request, verify the relevant behaviors:

- A CSV opens through both file selection and drag-and-drop.
- Numeric columns can be added, removed, and searched.
- Timestamped samples use their real elapsed positions, including irregular gaps.
- CSVs without usable timestamps fall back to row-number spacing.
- Non-timestamp AMD summary rows are not plotted as samples.
- Min, average, and max follow the visible horizontal range.
- FPS columns show correct 1% Low and 0.1% Low values.
- Mouse wheel scrolls graph rows vertically.
- Ctrl + mouse wheel zooms horizontally.
- Plot dragging selects a zoom range.
- Shift + drag pans the current range.
- Row labels can be dragged to reorder graph rows.
- Main-keyboard and numpad `+`/`-` zoom whenever data is loaded; Left/Right arrows pan with the chart focused.
- Up/Down arrows choose a row and Ctrl/Command + Up/Down reorders it.
- `Home` and `0` reset the complete timeline.
- Keyboard row changes are announced by a screen reader.
- The sidebar auto-collapses and can be pinned open.
- Hover: one and Hover: all both display the intended values.

## Data and privacy

Do not commit real or sensitive CSV performance recordings. If a sample is necessary to reproduce a parser bug, remove identifying information and explain the anonymization in the pull request.

## Scope

Keep pull requests focused. Large visual redesigns, new dependencies, or architectural changes should start as an issue so the approach can be discussed first.
