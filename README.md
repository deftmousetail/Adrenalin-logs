# AMD Adrenalin CSV Reader

A privacy-first, standalone browser tool for exploring performance telemetry exported from AMD Software: Adrenalin Edition.

**Current version: 1.1.1**

## Features

- Opens one Hardware CSV, one FPS / latency CSV, and one raw FrameTime file from the same session
- Processes every file locally in the browser
- Aligns the sources on their recorded timeline without shifting values to make them match
- Shows each CSV file's detected logging interval
- Provides CPU ↔ GPU, GPU limits, GPU HW, CPU HW, Frame pacing, and Frame time only views
- Draws AMD's sampled FPS as a solid line and, when FrameTime is loaded, a dashed trailing-one-second FPS calculated from raw frames
- Calculates 1% Low FPS from P99 raw frame time and 0.1% Low FPS from P99.9 raw frame time
- Requires at least 100 visible frames for 1% Low and 1,000 for 0.1% Low
- Keeps sampled FPS statistics to minimum, average, and maximum so they are not confused with per-frame lows
- Supports synchronized zooming, panning, hover values, row reordering, search, and keyboard controls
- Uses an expanded FrameTime overflow scale for large hitches in the Frame time only view
- Includes a quick-start Guide, metric glossary, and compact loaded-file information panel
- Runs as one portable HTML file with no dependencies or build step

## Use it

Use the hosted reader at [deftmousetail.github.io/Adrenalin-logs](https://deftmousetail.github.io/Adrenalin-logs/), or download `index.html` and open it in a modern browser.

1. Add up to three files from the same recording: Hardware CSV, FPS / latency CSV, and FrameTime.
2. Choose a diagnostic view or select individual metrics.
3. Drag across the plot to zoom into a period and hover rows for exact values.
4. Compare trends and timing. Similar changes are useful clues, but they do not prove cause.

AMD logs are normally found in:

```text
C:\Users\YOUR-WINDOWS-USERNAME\AppData\Local\AMD\CN
```

`AppData` is hidden by default. Example names are:

- `Hardware.20260822-223204.CSV`
- `FPS.Latency.20260822-223204.CSV`
- `20260822-223204.FrameTime`

## FPS and FrameTime

The FPS / latency CSV is periodic telemetry. Its rows follow the logging interval selected in AMD Adrenalin, usually 250 ms to 5 seconds, but FPS and Average Frame Time may still refresh only about once per second. Repeated values are therefore normal.

The FrameTime file contains individual frame durations. Version 1.1.1 uses those raw frames for:

- **1% Low FPS:** `1000 / P99 frame time`
- **0.1% Low FPS:** `1000 / P99.9 frame time`
- **Raw-derived FPS comparison:** average frame delivery during the preceding one-second window

The comparison line is not time-shifted. A FrameTime spike may appear before AMD's next sampled FPS update, which helps make the different recording cadences visible.

## Controls

| Action | Control |
|---|---|
| Scroll metric rows | Mouse wheel |
| Zoom around the pointer | Ctrl + mouse wheel |
| Select a time range | Drag across the plot |
| Pan a zoomed range | Shift + drag |
| Reset the timeline | Double-click, `Home`, or `0` |
| Keyboard zoom and pan | `+` / `-`, Left / Right arrow |
| Choose a row | Up / Down arrow |
| Move a row | Drag its handle or Ctrl/Command + Up/Down |
| Hide a row | Its `×`, Delete, or Backspace |

## Test data

The `test` folder contains a synthetic five-minute session with a CPU-limited period in the middle. It can be used for demonstrations and regression checks without publishing a real user's recording.

## Privacy

CSV parsing, statistics, and chart rendering happen entirely in the browser. The source files are not uploaded by the application.

## Contributing

Bug reports, focused feature ideas, documentation improvements, and code contributions are welcome. Read [CONTRIBUTING.md](CONTRIBUTING.md) before opening a pull request.

## License

Licensed under the [MIT License](LICENSE).
