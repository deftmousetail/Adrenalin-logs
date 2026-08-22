# AMD Adrenalin CSV Reader

A privacy-first, standalone browser tool for exploring performance telemetry exported from AMD Software: Adrenalin Edition.

**Current version: 2.0.1**

## Features

- Opens one or more CSV files locally in the browser; performance logs are not uploaded
- Combines hardware and FPS / latency logs on one synchronized timestamp axis
- Preserves each file's native sampling rate without interpolating values
- FPS vs GPU, FPS vs CPU, and frame-pacing comparison presets
- Loaded-file list with sample counts and individual remove controls
- Session-mismatch warning based on filename identifiers and timestamp overlap
- Automatically detects numeric telemetry columns
- Add, remove, search, and reorder graph rows
- Timestamp-aware horizontal spacing that shows irregular sampling and recording gaps accurately
- Min, average, and max statistics for the visible range
- Sampled 1% Low and 0.1% Low statistics for FPS columns, with an in-app measurement caveat
- Mouse-wheel vertical row scrolling
- Ctrl + mouse wheel horizontal zoom
- Drag-to-zoom, Shift + drag panning, previous view, and reset zoom
- Keyboard zoom, panning, row selection, and row reordering
- Compact hoverable and clickable chart-navigation help
- One-row or all-row hover tooltips
- Auto-collapsing or pinned-open control sidebar
- No dependencies, installation, server, or build step

## Use it

1. Download `index.html`.
2. Open it in a modern browser.
3. Drop one or both matching AMD Adrenalin CSVs onto the page, or select **Add CSV files**.
4. Use a comparison preset or choose the metrics you want to compare.

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

When CSVs contain usable timestamp columns, every source retains its own timestamps and sampling rate. The graphs share a horizontal time axis, but values are not merged or interpolated. Hover values marked `≈` are the closest real reading from that source. The initial `N/A` period in an FPS / latency log remains on the timeline as an empty graph interval until the game begins reporting values.

Before combining files, the reader compares the session identifier at the end of each standard AMD filename and checks their common timestamp range. Different identifiers, no overlap, or less than 50% overlap with the shorter recording produce a confirmation warning. The user can cancel or deliberately load the files together; an overridden mismatch remains visible in the sidebar status.

Large gaps in a recording are left visually open, and rows without a usable timestamp—such as AMD's aggregate `N/A` hardware-summary row—are excluded from the timeline. CSVs without usable timestamps still fall back to row-number spacing, but timestamped and row-based files cannot be combined in one view.

Min, average, max, Sampled 1% Low, and Sampled 0.1% Low values follow the visible horizontal range. FPS lows are the averages of the lowest 1% and 0.1% of valid logged FPS samples in that range. They are sample-based summaries—not per-frame benchmark percentiles—and brief hitches may be missed or averaged out by the logging interval. The same caveat is available from the chart's top-right help button.

## Privacy

CSV parsing and chart rendering happen entirely in the browser. The repository intentionally ignores `*.csv` files to reduce the risk of committing personal performance recordings.

## Contributing

Bug reports, feature ideas, documentation improvements, and code contributions are welcome. Read [CONTRIBUTING.md](CONTRIBUTING.md) before opening a pull request.

## License

Licensed under the [MIT License](LICENSE).
