# Contributing

Thanks for helping improve AMD Adrenalin CSV Reader.

## Ways to contribute

- Report a reproducible bug
- Suggest a focused feature
- Improve AMD log compatibility
- Improve browser, keyboard, mobile, or accessibility behavior
- Improve documentation

## Before you start

For a small, focused fix, open a pull request directly. For a large visual redesign, new dependency, file-format change, or architectural change, open an issue first so the approach can be discussed.

Do not commit real or sensitive performance recordings. If a sample is necessary to reproduce a parser problem, remove identifying information and explain the anonymization in the pull request.

## Development workflow

1. Fork the repository.
2. Create a branch with a short, descriptive name.
3. Edit `index.html` or the relevant documentation file.
4. Open `index.html` locally in a modern browser and test the affected behavior.
5. Open a pull request that explains what changed and how it was tested.

There is no build step or dependency installation. The application is intentionally kept as one portable HTML file, and all log processing must remain local to the browser.

## Supported session files

The reader accepts at most one file of each type:

- `Hardware.YYYYMMDD-HHMMSS.CSV`
- `FPS.Latency.YYYYMMDD-HHMMSS.CSV`
- `YYYYMMDD-HHMMSS.FrameTime`

Files may be inspected individually or combined when they belong to the same recording session. Loading another file of an occupied type should request confirmation before replacing it.

## Testing checklist

Test the parts affected by your change. A pull request does not need to exercise every item when the change is narrowly scoped.

### Loading, parsing, and session matching

- Each supported file type opens through both file selection and drag-and-drop.
- A matching Hardware, FPS / Latency, and FrameTime set can be loaded together.
- More than three files, duplicate types in one batch, unsupported layouts, malformed CSV quoting, and unusable files produce a clear error.
- Adding a second file of an already loaded type requests confirmation and replaces only that source.
- Individual sources can be removed, and **Remove all** returns to the home screen.
- Filename session identifiers, timestamp overlap, and recording duration produce a warning when files may not belong to the same session.
- Hardware and FPS / Latency values retain their recorded timestamps on the shared timeline.
- Raw FrameTime data aligns to the first valid FPS timestamp without shifting the capture start.
- Leading timestamped FPS `N/A` rows remain an empty interval; the plot begins when numeric reporting starts.
- Timestamped samples preserve irregular gaps. Files without usable timestamps fall back to row-number spacing.
- Non-timestamp AMD summary rows are not plotted.
- The known first-sample `9999 FPS / 0.1 ms` pattern offers **Exclude artifact** and **Keep all data**.
- Excluding that artifact affects plots and statistics only, can be reversed from **Loaded files**, and does not alter the original file or FrameTime alignment.
- Ordinary high FPS values and later `9999` values do not trigger the startup-artifact dialog.

### Metrics, presets, and statistics

- Numeric metrics can be searched, selected, cleared, hidden, and reordered.
- Metric choices remain in source-column order; graph-row order remains independently draggable.
- **CPU ↔ GPU**, **GPU limits**, **Frame pacing**, and **Frame time only** select their documented metrics.
- **GPU HW** selects numeric GPU Hardware metrics.
- **CPU HW** selects numeric CPU Hardware metrics plus `SYSTEM MEM UTIL`.
- GPU HW and CPU HW can be active together, and removing one group leaves the other intact.
- Statistics use only samples in the visible time range.
- The statistics strip contains only graph rows that are fully or partly visible and updates while scrolling.
- FPS statistics show the expected 1% Low and 0.1% Low values.
- FrameTime statistics and thresholds update with the visible range; **Worst** is the longest visible frame.
- Dense FrameTime rendering emphasizes the min–max variation strokes, while sufficiently zoomed views show individual frames.
- The isolated Frame time view retains detail below 50 ms and uses its expanded upper scale for larger spikes.

### Chart interaction and tooltips

- Mouse wheel scrolls graph rows; Ctrl + mouse wheel zooms around the pointer.
- Dragging the plot selects a time range; Shift + drag pans it.
- Double-click, `Home`, and `0` restore the complete timeline.
- `+` and `-` zoom; Left and Right pan when the chart is focused.
- Up and Down select a row; Ctrl/Command + Up/Down reorder it.
- Delete and Backspace hide the selected row.
- Row handles can be dragged, and their × controls hide the intended rows.
- **Condense** cycles through Full, 72%, 50%, and 33% without changing the selected time range or statistics, and becomes unavailable below the supported viewport width.
- **Current row** snaps CSV hover values to recorded samples.
- **All displayed rows** includes only fully or partly visible graph rows and refreshes while the chart scrolls.
- Sample times appear once per CSV source rather than beside every metric.
- Raw FrameTime hover values remain exact.

### Interface, guidance, and accessibility

- The sidebar can be opened, collapsed, and pinned.
- The `?` panel contains chart-navigation controls only.
- **Guide** and **Glossary** open and close correctly by button, outside click, and Escape.
- Dialogs do not allow chart keyboard shortcuts to fire while they are open.
- The home screen shows the Windows log location, supported filename examples, local-processing notice, and repository credit.
- The layout remains usable on narrow screens; unsupported condensed states fall back to full width without showing a stale active state.
- Keyboard row changes and status notifications are announced to screen readers.
- Interactive controls retain visible focus states and meaningful accessible labels.

## Pull request notes

Keep pull requests focused and avoid unrelated formatting changes. In the description, include:

- The problem being addressed
- The behavior before and after the change
- The browsers and file combinations tested
- Screenshots for visible interface changes
- Any remaining limitations or follow-up work

If a release changes the public version, keep the version shown in `index.html`, the document title, and the README release information consistent.
