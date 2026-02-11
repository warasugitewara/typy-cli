# Changelog

## [Unreleased] - Fork with Windows Fix

### Fixed
- **Windows double input issue**: Fixed a critical bug where key inputs were being registered twice on Windows environments (Windows Terminal, PowerShell, nushell)
  - Root cause: `KeyEvent` was processing all event kinds (Press, Release, Repeat), not just Press events
  - Solution: Added `KeyEventKind::Press` filter to only process actual key presses
  - Affected files: `src/terminal/game.rs`

### Changed
- Added explicit `stdout.flush()` calls in keyboard input handlers to ensure proper output buffering
  - Modified functions: `handle_correct_char()`, `handle_incorrect_char()`, `add_incorrect_char()`
  - Affected files: `src/terminal/keyboard.rs`

### Added
- Import of `KeyEventKind` from crossterm for event filtering
- Added `ABOUT.ja.md` with Japanese documentation about this fork

## Base Version
Based on [Pazl27/typy-cli](https://github.com/Pazl27/typy-cli) - All original features and functionality remain intact.
