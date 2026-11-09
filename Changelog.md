# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [2.0.0] - 2026-11-09

### Added
- Footer bar with live clock, "showing X of Y" status, and a quick-switch dropdown to jump to any dashboard instantly
- Per-item display duration: each dashboard can set its own rotation seconds (admin panel inline field; optional on add) — header countdown and rotator honor per-item values
- Drag-to-reorder in the admin list (⋮⋮ handle), persisted via a new `order` field in Firestore
- "⟳ Reload" button to re-load the current iframe (recovers local sites when the server comes back)
- Friendly "Loading: …" placeholder page inside frames instead of a blank white box while/instead of the target site loading
- Toast notifications for add / delete / reorder / duration feedback
- Auto-derive a dashboard title from the URL when no title is given
- "Common local app paths" reference card in the admin panel (e.g. `/nodejsapps/`)
- Commit workflow reference (`commit.txt`) for changelog + commit/push steps

### Changed
- Admin URL input is now plain text with a local-site example placeholder (previously `type="url"`), so local URLs like `http://www.aqua-aerobic.net/nodejsapps/` paste cleanly
- Frame URLs are re-pointed automatically when edited in Firestore (no page reload needed)
- Admin actions (add / delete / reorder / duration) are guarded behind login with inline feedback instead of `alert()` dialogs
- Layout uses flex `min-height: 0` so the iframe area and footer scale correctly in all browsers

### Fixed
- Countdown timer can no longer display negative seconds
- Pausing now clears the rotator interval fully, so resume always starts a clean cycle
- Item titles/URLs in the admin list and iframe placeholders are inserted as text, preventing HTML injection from stored values

### Notes
- Backwards compatible: existing Firestore items without `order` or `duration` fall back to timestamp order and the 30-second default — no data migration required
