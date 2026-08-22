# AMD Adrenalin CSV Reader

A privacy-first, standalone browser tool for exploring performance telemetry exported from AMD Software: Adrenalin Edition.

**Current version: 2.1.1**

## Features

- Opens one Hardware log, one FPS / latency log, or one matching pair locally in the browser; performance logs are not uploaded
- Combines hardware and FPS / latency logs on one synchronized timestamp axis
- Limits a session view to two files: one file per supported log type
- Replaces the occupied slot—with confirmation—when another file of the same type is added
- Preserves each file's native sampling rate without interpolating values
- CPU ↔ GPU, GPU limits, and frame-pacing diagnostic views
- Loaded-file list with explicit **Remove** and **Remove all** controls
- Session-mismatch warning based on filename identifiers and timestamp overlap
- Automatically detects numeric telemetry columns
- Add, remove, search, and reorder graph rows
- Stable metric-list ordering regardless of checkbox state
- Guided empty state explaining the workflow and sampling limitations
- Timestamp-aware horizontal spacing that shows irregular sampling and recording gaps accurately
- Min, average, and max statistics for the visible range
- Top statistics strip automatically follows the graph rows in the vertical viewport
- Sampled 1% Low and 0.1% Low statistics for FPS columns, with an in-app measurement caveat
- Mouse-wheel vertical row scrolling
- Ctrl + mouse wheel horizontal zoom
- Drag-to-zoom, Shift + drag panning, and reset through **Fit all**, double-click, or the keyboard
- Keyboard zoom, panning, row selection, and row reordering
- Compact hoverable and clickable chart-navigation help
- One-row or all-row hover tooltips
- Auto-collapsing or pinned-open control sidebar
- No dependencies, installation, server, or build step

## Use it

1. Download `index.html`.
2. Open it in a modern browser.
3. Drop one or both matching AMD Adrenalin CSVs onto the page, or select **Add CSV files**. The reader accepts at most one Hardware file and one FPS / latency file.
4. Use a diagnostic view or choose the metrics you want to compare.

The application is a single HTML file, so it can also be published directly with GitHub Pages.

## Controls

| Action | Mouse | Keyboard while chart is focused |
|---|---|---|
| Zoom in or out | Ctrl + mouse wheel | `+` / `-` on the main keyboard or numeric keypad; chart focus is not required |
| Select a zoom range | Drag across the plot | — |
| Pan | Shift + drag | Left / Right arrow |
| Reset zoom | Double-click the plot or choose **Fit all** in the sidebar | `Home` or `0` |
| Choose a graph row | Point at its row | Up / Down arrow |
| Move a graph row | Drag its label | Ctrl/Command + Up/Down arrow |

## Time axis and statistics

When CSVs contain usable timestamp columns, every source retains its own timestamps and sampling rate. The graphs share a horizontal time axis, but values are not merged or interpolated. Hover uses the nearest real logged reading from each source without adding an approximation symbol. The initial `N/A` period in an FPS / latency log remains on the timeline as an empty graph interval until the game begins reporting values.

## Diagnostic views

- **CPU ↔ GPU:** FPS, GPU utilization, and total CPU utilization for an initial bottleneck triage.
- **GPU limits:** FPS, GPU utilization, GPU clock, total board power, and GPU hotspot temperature for spotting load, power, clock, or thermal relationships.
- **Frame pacing:** FPS, average frame time, 99th% FPS, micro-stutter, and heavy-stutter rate for investigating inconsistent delivery.

These views show sampled relationships; they do not establish causation or definitively identify the limiting processor. AMD's Radeon GPU Profiler uses CPU submission and GPU execution/idle timing for processor-level bottleneck classification, which is more detailed than Adrenalin's periodic CSV telemetry. See [AMD's Adrenalin metric definitions](https://www.amd.com/en/resources/support-articles/faqs/DH3-038.html) and [Radeon GPU Profiler's queue-timing methodology](https://gpuopen.com/manuals/rgp_manual/overview_windows/).

Before combining files, the reader compares the session identifier at the end of each standard AMD filename and checks their common timestamp range. Different identifiers, no overlap, or less than 50% overlap with the shorter recording produce a confirmation warning. The user can cancel or deliberately load the files together; an overridden mismatch remains visible in the sidebar status. Other CSV layouts and attempts to select more than one file of either supported type are rejected.

The loaded-file list has a visible **Remove** button for each slot and a **Remove all** action. Adding a different file of an already-loaded type prompts before replacing that slot, so files cannot accumulate across game sessions.

When no files are loaded—or after **Remove all**—the main panel explains the two-file workflow and the limits of periodic logging. AMD allows a sampling interval from 0.25 to 5 seconds. At the fastest 250 ms setting, roughly 15 frames occur at 60 FPS between samples. The reader is therefore intended for sustained trends, major changes, and broad relationships rather than definitive per-frame pacing or bottleneck analysis.

Large gaps in a recording are left visually open, and rows without a usable timestamp—such as AMD's aggregate `N/A` hardware-summary row—are excluded from the timeline. CSVs without usable timestamps still fall back to row-number spacing, but timestamped and row-based files cannot be combined in one view.

The statistics strip stays accessible above the chart but includes only graph rows currently visible in the vertical viewport. Min, average, max, Sampled 1% Low, and Sampled 0.1% Low values also follow the visible horizontal time range. FPS lows are the averages of the lowest 1% and 0.1% of valid logged FPS samples in that range. They are sample-based summaries—not per-frame benchmark percentiles—and brief hitches may be missed or averaged out by the logging interval. The same caveat is available from the chart's top-right help button.

## Privacy

CSV parsing and chart rendering happen entirely in the browser. The repository intentionally ignores `*.csv` files to reduce the risk of committing personal performance recordings.

## Contributing

Bug reports, feature ideas, documentation improvements, and code contributions are welcome. Read [CONTRIBUTING.md](CONTRIBUTING.md) before opening a pull request.

## License

Licensed under the [MIT License](LICENSE).
