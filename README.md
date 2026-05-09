# Splatter: Qualitative Coding & Affinity Diagramming

**One HTML file. Zero installation. Built for qualitative researchers.**


## [TRY OUT SPLATTER](https://hasiburrahman.net/splatter/)

Splatter is a single-file qualitative coding and affinity diagramming tool that runs entirely in your browser. Import interview transcripts, tag quotes, group themes, draw connections, and export your analysis — all without leaving the page.

> **Based on [Splat](https://github.com/ianarawjo/splat) by Ian Arawjo and the Montréal HCI group.** Modified by [Hasibur Rahman](https://hasiburrahman.net/) at [CHAI Lab](https://chainortheastern.net/). Licensed under GPL v3.0.

## How to Use

Open `splatter.html` in your browser. That's it.

## Features

### Qualitative Coding
- **Tags/Codes**: Add multiple tags to any note. Tags render as colored pills with autocomplete from your emerging codebook. Press `T` to tag the last focused note.
- **Codebook panel**: See all tags with frequency counts. Rename, merge, or delete tags globally. Export codebook as CSV.
- **Participant tracking**: End any note with `(P1)`, `(P2)`, etc. Participant IDs appear in the filter bar automatically.

### Transcript Import
- **Import interview transcripts** via Settings → Import Transcript.
- Auto-detects `[Speaker 1]` / `Speaker 1:` patterns. Falls back to paragraph splitting for untagged transcripts.
- **Transcript viewer**: Browse paragraphs, filter by speaker, click to select whole blocks or highlight specific quotes.
- **Participant ID assignment**: Map speakers to participant IDs before import (e.g., Speaker 2 → P5).

### Board Interaction
- **Notes & Memos**: Press `N` for a data note, `M` for a researcher memo. Double-click to edit.
- **8 colors**: Yellow, pink, blue, green, orange, purple, tan, gray.
- **Groups (drop zones)**: Press `G` to create a named zone. Drag notes in to group, drag out to remove. Drag the group header to move everything together.
- **Connections**: Press `C` to enter connect mode. Click two notes to link them. Click any connection line to edit type (related/supports/contradicts/leads-to), add a label, or delete.
- **Undo/Redo**: `Ctrl+Z` / `Ctrl+Shift+Z`. Tracks all operations.
- **Auto-save**: Every 60 seconds to localStorage.
- **Multi-board tabs**: Up to 5 independent boards with their own notes, groups, and connections.
- **Snap-to-grid**: Toggle with the ⊞ button.
- **Minimap**: Overview panel in the bottom-right. Click to pan.

### Filtering & Search
- **Filter bar**: Filter by tag, color, participant ID, or type (notes/memos). Filters combine with AND logic.
- **Semantic search**: Hybrid BM25 + embedding search. Supports HF Transformers.js (in-browser), Ollama (local), or OpenAI (cloud).
- **Search results panel**: Ranked matches with click-to-focus navigation.

### AI Assistant (optional)
- **Tool-calling agent**: AI can search, create, edit, and remove notes.
- **Three providers**: Ollama (local/private), OpenAI, or OpenRouter (access to Claude, Gemini, etc.).
- Configure via the Settings gear icon.

### Export
- **Save/Load Board**: JSON format for easy sharing.
- **Export CSV**: Notes with tags, groups, participant IDs, timestamps.
- **Export Markdown**: Structured report organized by groups, with memos and connections.
- **Export Codebook**: Tag frequencies with example quotes.

All file operations are in Settings (gear icon).

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| `N` | New note |
| `M` | New memo |
| `G` | Create group zone |
| `C` | Toggle connect mode |
| `T` | Add tag to last focused note |
| `S` | Toggle select mode |
| `Ctrl+Z` | Undo |
| `Ctrl+Shift+Z` | Redo |
| `Ctrl+S` | Save board |
| `Ctrl+F` | Focus search |
| `Delete` | Delete selected notes/connection |
| `Escape` | Close panels / exit modes |
| `Arrow keys` | Nudge selected notes (Shift: 1px) |

## Using Ollama (Local AI)

To use [Ollama](https://ollama.com) for embeddings or the AI chat, you must enable CORS:

```bash
launchctl setenv OLLAMA_ORIGINS "*"
```

Then restart Ollama and serve with `ollama serve`. The Ollama model you choose must support tools for the AI assistant to work.

## Using OpenRouter

[OpenRouter](https://openrouter.ai) gives access to models like Claude, Gemini, and others. Add your API key and model name (e.g., `anthropic/claude-sonnet-4`) in Settings.

## Credits

- **Original tool**: [Splat](https://github.com/ianarawjo/splat) by [Ian Arawjo](https://ianarawjo.com) and the [Montréal HCI](https://hci.iro.umontreal.ca/) group. AI assistance and search features by Jingyue Zhang, Ling Xin He, and Yunfan Shang.
- **Splatter modifications**: [Hasibur Rahman](https://hasiburrahman.net/) at [CHAI Lab](https://chainortheastern.net/) — undo/redo, tags/codebook, groups, memos, connections, transcript import, participant filtering, multi-board tabs, minimap, OpenRouter support, UI/UX redesign.

## License

Licensed under the [GNU General Public License v3.0](https://github.com/ianarawjo/splat/blob/main/LICENSE).
