# Contributing

Thanks for helping improve AMD Adrenalin CSV Reader.

## Ways to contribute

- Report a reproducible bug
- Suggest a focused feature
- Improve browser, keyboard, mobile, or accessibility behavior
- Improve compatibility with AMD log formats
- Improve user-facing documentation

## Development workflow

1. Fork the repository.
2. Create a short, descriptive branch.
3. Edit `index.html`.
4. Open it locally in a modern browser and test the complete reader.
5. Open a pull request explaining the change and how it was tested.

The app intentionally remains one portable HTML file. There is no dependency installation, build step, or server requirement.

## Test with supported sources

The reader accepts at most one file of each type from a session:

- Hardware CSV
- FPS / latency CSV
- FrameTime

The synthetic files in `test` are safe to use for routine checks. Do not commit real recordings unless they have been deliberately anonymized and are necessary to reproduce a parser problem.

## Testing checklist

Check the behavior relevant to your change, including:

- File selection and drag-and-drop accept one, two, or three matching sources.
- Unsupported files, duplicate source types in one batch, and more than three files produce a clear error.
- Loading another file of an occupied type asks before replacing it.
- The three source types align on one timeline while retaining their recorded timestamps.
- The Loaded files section stays compact; filenames have an accessible `×`, and the `i` panel contains source details and first-sample restoration.
- Session-name, time-overlap, and duration checks warn about likely mismatches without discarding already loaded files.
- When the conservative detector flags a possible first-sample outlier, it can be excluded and restored without changing the source file or FrameTime anchor.
- Diagnostic views select their documented metrics. GPU HW and CPU HW remain independently toggleable and can be combined.
- Metric selection, search, row hiding, row dragging, and keyboard reordering work.
- Horizontal zoom and pan update both the graph and visible-range statistics.
- Tight zooms with one CSV sample show a dashed held value and a marker instead of an empty row.
- The top statistics strip follows the rows visible in the scrolling chart viewport.
- Sampled FPS shows only minimum, average, and maximum.
- Raw FrameTime shows average, P99, P99.9, worst, average FPS, 1% Low, and 0.1% Low.
- 1% Low equals `1000 / P99 frame time` only when at least 100 frames are visible.
- 0.1% Low equals `1000 / P99.9 frame time` only when at least 1,000 frames are visible.
- With matching FPS and FrameTime sources loaded, the FPS row shows a solid logged line and a dashed trailing-one-second raw-derived line on the same scale.
- FPS hover shows logged FPS, raw-derived FPS, and their difference without shifting timestamps.
- The FrameTime overview emphasizes min–max variation, and the isolated split scale keeps large spikes readable.
- The Guide's quick start is visible immediately and its detailed topics expand and collapse correctly.
- Mouse, touch/pointer, and keyboard controls remain limited to the chart when appropriate.
- The app remains usable at narrow viewport widths.

## Data and privacy

Keep real or sensitive performance logs out of the repository. If a sample is essential for a parser bug, remove identifying information and explain the anonymization in the pull request.

## Scope

Keep pull requests focused. Discuss a large visual redesign, new dependency, or architectural change in an issue before implementation.
