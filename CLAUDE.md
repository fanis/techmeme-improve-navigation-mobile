# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Greasemonkey/Tampermonkey/Violentmonkey userscript that fixes browser Back/Forward navigation on Techmeme's mobile site. When users tap the "more" link on a story, Techmeme opens an in-page overlay without updating the URL - this script pushes a history entry so Back closes the overlay and Forward reopens it.

## Architecture

Single-file userscript at `src/techmeme-improve-navigation.js`. No build step, no dependencies, no tests.

Key mechanisms:
- Capture-phase click listener on `td.nav_to_more` extracts the item ID from `openItemPage('...')` onclick attribute
- `history.pushState()` with `#tm_more=<itemId>` hash before Techmeme's own onclick fires
- `popstate` listener: no hash = close overlay (clicks `#back_selector`), hash present = reopen via `window.openItemPage()`
- IIFE with strict mode, `@run-at document-start`, `@grant none`

## Development

No build or lint commands. Edit the JS file directly and reload in browser with userscript manager.

The script depends on Techmeme's DOM structure (`td.nav_to_more`, `#back_selector`) and global `openItemPage` function - if Techmeme changes these, the script breaks.

## Licence

PolyForm Internal Use License 1.0.0 - free for personal/internal use, no redistribution.
