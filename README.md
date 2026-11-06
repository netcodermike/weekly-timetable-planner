# Weekly Timetable Planner

Plan a weekly timetable with time parsing, overlap rejection, and portable saved schedules.

[![Build and verify](https://github.com/netcodermike/weekly-timetable-planner/actions/workflows/verify.yml/badge.svg)](https://github.com/netcodermike/weekly-timetable-planner/actions/workflows/verify.yml)

**Language:** Kotlin · **Platform:** Windows, macOS, Linux desktop · **App type:** Desktop timetable editor with conflict checks

First-release learning implementation, with explicit scope below. This is one independently runnable app, not a placeholder in a combined repository.

## Features

- Seven weekday groups
- Start/end intervals
- Boundary-aware conflict checks
- Save/open Properties schedules

## Requirements

JDK 17 and Gradle 8.9; first build downloads Kotlin 2.0.21 from Gradle/Maven. No binary wrapper is included.

## Quick start

```sh
git clone https://github.com/netcodermike/weekly-timetable-planner.git
cd weekly-timetable-planner
gradle run
```

Commands run from the repository root. Lines marked for a particular operating system apply only there. Language tools are prerequisites, not installed by the app. Close desktop windows normally; terminal/server apps stop with Ctrl+C unless their usage notes say otherwise.

## Example workflow

Add Monday 09:00–10:00 Study, then 10:00–11:00 Work. Try a conflicting 09:30 event and verify rejection. Save/open the schedule.

## Architecture, configuration, and data

Main.kt represents each event as day/start-minute/end-minute/title. Same-day intervals overlap only if each starts before the other ends; touching boundaries are valid. Up to 500 events are validated before insertion/import. Swing displays a sorted schedule with removal and explicit save/open. Tests check HH:mm parsing, conflict boundaries, and persistence encoding.

## Verification

Build with the quick-start command where needed, then run:

```sh
gradle run --args="--self-test" --no-daemon
```

Manual acceptance: Add Monday 09:00–10:00 Study, then 10:00–11:00 Work. Try a conflicting 09:30 event and verify rejection. Save/open the schedule. Also test malformed inputs and an unwritable output destination.

See [validation record](docs/VALIDATION.md) for observed checks and their limits. CI results verify only what the workflow runs; they do not establish native GUI correctness or production readiness.

## Limitations and next steps

Weekly repeating plan only: no dates, recurrence exceptions, notifications, calendar sync, exports, drag layout, or autosave. UI inputs accept 00:00–23:59, so midnight-ending events are not directly enterable. Unsaved edits are lost on close. Save can replace the chosen file.

## Troubleshooting

Use the exact platform/toolchain above. Preserve originals and use synthetic fixtures first. Errors are displayed in the UI or stderr. A headless machine can run the model tests but cannot verify native GUI/audio behavior. Output paths are chosen explicitly; keep backups of important data.

## Source map

- `build.gradle.kts`
- `settings.gradle.kts`
- `src/main/kotlin/Main.kt`

## Development and license

Read [contributing](CONTRIBUTING.md) before changing the app, and [security/privacy](SECURITY.md) before supplying private data. Use synthetic fixtures for tests. No telemetry, paid API key, or account is required by the app itself. Dependencies, when present, are stated in Requirements.

[MIT license](LICENSE), copyright 2026 netcodermike.
