# AMD Adrenalin CSV Reader

A privacy-first, standalone browser tool for exploring performance telemetry exported from AMD Software: Adrenalin Edition.

**Current version: 1.0.0**

## Features

- Opens CSV files locally in the browser; performance logs are not uploaded
- Automatically detects numeric telemetry columns
- Add, remove, search, and reorder graph rows
- Timestamp-aware horizontal spacing that shows irregular sampling and recording gaps accurately
- Min, average, and max statistics for the visible range
- 1% Low and 0.1% Low statistics for FPS columns
- Mouse-wheel vertical row scrolling
- Ctrl + mouse wheel horizontal zoom
- Drag-to-zoom, Shift + drag panning, previous view, and reset zoom
- Keyboard zoom, panning, row selection, and row reordering
- One-row or all-row hover tooltips
- Auto-collapsing or pinned-open control sidebar
- No dependencies, installation, server, or build step

## Use it

1. Download `index.html`.
2. Open it in a modern browser.
3. Drop an AMD Adrenalin CSV onto the page or select **Open CSV**.
4. Choose the numeric columns you want to compare.

The application is a single HTML file, so it can also be published directly with GitHub Pages.

## Controls

| Action | Mouse | Keyboard while chart is focused |
|---|---|---|
| Zoom in or out | Ctrl + mouse wheel | `+` / `-` on the main keyboard or numeric keypad; chart focus is not required |
| Select a zoom range | Drag across the plot | — |
| Pan | Shift + drag | Left / Right arrow |
| Reset zoom | Double-click or **Reset zoom** | `Home` or `0` |
| Choose a graph row | Point at its row | Up / Down arrow |
| Move a graph row | Drag its label | Ctrl/Command + Up/Down arrow |

## Time axis and statistics

When the CSV contains a usable timestamp column, samples are positioned according to their actual timestamps rather than their row numbers. Large gaps in a recording are left visually open, and rows without a usable timestamp—such as AMD's aggregate `N/A` summary row—are excluded from the timeline. CSVs without usable timestamps fall back to row-number spacing.

Min, average, max, 1% Low, and 0.1% Low values follow the visible horizontal range. FPS lows are the averages of the lowest 1% and 0.1% of valid FPS samples in that range.

## Privacy

CSV parsing and chart rendering happen entirely in the browser. The repository intentionally ignores `*.csv` files to reduce the risk of committing personal performance recordings.

## Contributing

Bug reports, feature ideas, documentation improvements, and code contributions are welcome. Read [CONTRIBUTING.md](CONTRIBUTING.md) before opening a pull request.

## License

Licensed under the [MIT License](LICENSE).
