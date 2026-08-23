# AMD Adrenalin CSV Reader

A privacy-first, standalone browser tool for exploring performance telemetry exported by AMD Software: Adrenalin Edition.

**Current version: 1.0**

Created by [deftmousetail](https://github.com/deftmousetail).

## Features

- Loads one Hardware CSV, one FPS / Latency CSV, and one matching FrameTime file
- Processes every file locally in the browser; logs are never uploaded
- Aligns raw frame durations to the first valid FPS timestamp
- Checks filename session identifiers, timestamp overlap, and recording duration
- Detects the known 9999 FPS startup artifact and lets the user retain or exclude it without changing the original file
- Plots sampled Hardware and FPS / Latency metrics on one synchronized timeline
- Adds adaptive raw FrameTime rendering with visible-range statistics
- Uses an expanded split scale for large FrameTime spikes in the isolated Frame time view
- Provides CPU ↔ GPU, GPU limits, GPU HW, CPU HW, Frame pacing, and Frame time diagnostic views
- Allows GPU HW and CPU HW to be active together; CPU HW includes system memory utilization
- Supports metric searching, row reordering, row hiding, drag zoom, panning, and timeline-width condensation
- Offers current-row or all-visible-row tooltip modes
- Includes practical Guide and Glossary panels
- Has no dependencies, installation, server, or build step

## Use it

1. Download `index.html`.
2. Open it in a modern browser.
3. Add up to one file of each supported type from the same recording session:
   - `Hardware.YYYYMMDD-HHMMSS.CSV`
   - `FPS.Latency.YYYYMMDD-HHMMSS.CSV`
   - `YYYYMMDD-HHMMSS.FrameTime`
4. Choose a diagnostic view or select individual metrics.

AMD logs are normally found at:

```text
C:\Users\YOUR-WINDOWS-USERNAME\AppData\Local\AMD\CN
```

`AppData` is hidden by default. Replace the placeholder with the Windows account folder name and paste the path into File Explorer's address bar.

## Chart controls

| Action | Result |
|---|---|
| Mouse wheel | Scroll through metric rows |
| Ctrl + mouse wheel | Zoom around the pointer |
| Drag the plot | Zoom into the selected time period |
| Shift + drag | Move through a zoomed timeline |
| Double-click | Return to the complete session |
| Drag a row handle | Rearrange rows |
| × on a row handle | Hide that row |
| Condense | Cycle through Full, 72%, 50%, and 33% timeline width |

Keyboard alternatives:

- `+` / `-`: zoom
- `←` / `→`: move through time
- `↑` / `↓`: choose a row
- `Ctrl` or `Command` + `↑` / `↓`: move the chosen row
- `Delete` / `Backspace`: hide the chosen row
- `Home` or `0`: return to the complete session

## Diagnostic views

- **CPU ↔ GPU** compares FPS with total CPU and GPU utilization.
- **GPU limits** compares FPS with GPU utilization, clock speed, board power, and hotspot temperature.
- **GPU HW** shows numeric GPU metrics from the Hardware CSV.
- **CPU HW** shows numeric CPU metrics and system memory utilization from the Hardware CSV.
- **Frame pacing** combines raw FrameTime with sampled FPS and stutter indicators.
- **Frame time only** isolates individual frame durations and expands the upper scale when spikes exceed 50 ms.

Diagnostic views reveal relationships worth investigating; they do not prove that one metric caused a performance problem.

## Understanding the data

Hardware and FPS / Latency CSV values are periodic measurements. Use them for sustained load, broad trends, and major changes.

A FrameTime file contains individual frame durations and is better suited to frame-pacing distributions and short hitches. Raw frames are aligned to the first valid FPS timestamp. Nearby Hardware samples can suggest a relationship, but their slower sampling cannot prove the exact cause of one frame-time spike.

FrameTime statistics are calculated from frames in the visible timeline. **Worst** is the single longest visible frame duration. FPS 1% Low and 0.1% Low are calculated from visible logged FPS samples and are not equivalent to benchmark-grade lows calculated from every individual frame.

## GitHub Pages

This repository can be published directly because the application is a single `index.html` file.

In the repository, open **Settings → Pages**, choose **Deploy from a branch**, select the publishing branch and `/(root)`, then save.

## Privacy

Parsing and chart rendering happen entirely in the browser. Do not commit personal performance recordings to the repository.

## Contributing

Bug reports, feature ideas, documentation improvements, and focused code contributions are welcome. Read [CONTRIBUTING.md](CONTRIBUTING.md) before opening a pull request.

## License

Licensed under the [MIT License](LICENSE).
