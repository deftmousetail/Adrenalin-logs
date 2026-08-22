# AMD Adrenalin CSV Reader

A privacy-first, standalone browser tool for exploring performance telemetry exported from AMD Software: Adrenalin Edition.

## Features

- Opens CSV files locally in the browser; performance logs are not uploaded
- Automatically detects numeric telemetry columns
- Add, remove, search, and reorder graph rows
- Min, average, and max statistics for the visible range
- 1% Low and 0.1% Low statistics for FPS columns
- Mouse-wheel vertical row scrolling
- Ctrl + mouse wheel horizontal zoom
- Drag-to-zoom, Shift + drag panning, previous view, and reset zoom
- One-row or all-row hover tooltips
- Auto-collapsing or pinned-open control sidebar
- No dependencies, installation, server, or build step

## Use it

1. Download `index.html`.
2. Open it in a modern browser.
3. Drop an AMD Adrenalin CSV onto the page or select **Open CSV**.
4. Choose the numeric columns you want to compare.

The application is a single HTML file, so it can also be published directly with GitHub Pages.

## Privacy

CSV parsing and chart rendering happen entirely in the browser. The repository intentionally ignores `*.csv` files to reduce the risk of committing personal performance recordings.

## Contributing

Bug reports, feature ideas, documentation improvements, and code contributions are welcome. Read [CONTRIBUTING.md](CONTRIBUTING.md) before opening a pull request.

## License

Licensed under the [MIT License](LICENSE).
