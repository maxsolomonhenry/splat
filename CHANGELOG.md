# Changelog

All notable changes to this project will be documented in this file.

## [Unreleased]

### Added
- **Workspace launcher**: Full workspace management layer above multi-board tabs. Launcher screen shows workspace cards with name, note count, and last-modified date. Create, rename, and delete workspaces. Each workspace contains up to 5 independent boards. "Back to Workspaces" toolbar button to return to launcher.
- **Legacy data migration**: On first launch, if old `splatAutosave` data exists but no workspaces are defined, auto-creates a "Migrated Board" workspace and migrates the data seamlessly.
- **Undo/Redo system**: Command-pattern undo/redo with comprehensive coverage of all state-changing operations. Stacks capped at 100 entries. Toolbar buttons (↩/↪) and keyboard shortcuts. Supported actions:
  - **Notes**: create, delete, edit text, move (single and multi-select), color change, pin/unpin, duplicate, bulk delete, bulk nudge
  - **Tags**: add to note, remove from note, rename globally, merge into another tag, delete from all notes, set parent category
  - **Codebook**: add code, import codebook CSV
  - **Groups**: create, delete, rename, collapse/expand, drag group zone (moves all member notes), auto-layout, organize all groups
  - **Connections**: create, delete, edit type/label
  - **Import**: file import (txt/csv), transcript quote import
  - **Board**: clear board
- **Tags/Codes system**: Notes support multiple textual tags — the core primitive for qualitative coding. Tags render as colored pills below note text, with colors auto-assigned by hashing the tag name. Inline tag input with autocomplete against all existing tags. Tags persist across save/load. Backward-compatible with older boards.
- **Codebook panel**: Resizable sidebar (drag handle, 200–600px) listing all tags with frequency counts, sortable by frequency, alphabetically, or by hierarchy. Per-tag actions: rename globally, merge into another tag, delete from all notes. Click any tag to filter the board. Export codebook as CSV.
- **Codebook hierarchy**: Tags can be assigned parent categories via a "Parent" button. Hierarchy sort mode groups codes under their parent category headers with "Uncategorized" as fallback. Persists in `tagParents` across save/load.
- **Codebook co-occurrence view**: Second codebook tab showing a tag co-occurrence matrix — which tags appear together on the same notes, sorted by frequency.
- **Codebook drag-to-tag**: Drag tags from the codebook panel onto notes to apply them. Pill-shaped drag image with drop-hover outline on target notes.
- **Tag definitions**: Each code/tag supports an inline editable definition in the codebook panel. Definitions persist in `tagDefinitions` and are included in codebook CSV export.
- **Tag history / audit trail**: All rename, merge, and delete operations on tags are recorded with timestamps. Codebook CSV export includes a history log section and per-tag "Merged From" column.
- **Add Code / Import CSV in codebook**: Pre-define codes in the codebook before tagging any notes. Bulk-import a codebook from CSV (columns: code name, definition, parent category).
- **Enhanced codebook CSV export**: Includes columns for Tag, Definition, Category (parent), Frequency, Merged From, and Examples (up to 3 note excerpts per tag), plus full history log.
- **Groups as drop zones**: Click Group (or press G) to create a named zone on the canvas. Drag notes into the zone to add them to the group. Drag notes out to remove. Zones auto-grow to fit contents. Drag the group header to reposition. Collapse/expand, rename (double-click label), delete (keeps notes). Groups persist across save/load.
- **Organize button**: Auto-layouts all group zones in a responsive grid across the viewport, positioning notes inside each group in a grid pattern.
- **Memos**: A distinct note type for researcher reflections. Click "+ Memo" or press M. Memos have dashed borders, a notebook icon, and display creation date. Filterable separately from data notes.
- **Connections/Links**: Click Connect (or press C) to enter connect mode. Click first note (blue ring appears), then second — connection created instantly. Click any connection line to edit type/label or delete via inline popover. Four types: related (gray), supports (green), contradicts (red dashed), leads-to (blue). Connections auto-update on drag. Persist across save/load.
- **AI agent chat panel**: Floating chat panel (bottom-right) with toggle, close, and reset buttons. Thinking animation with bouncing dots. Tool-use messages shown as pills. Markdown rendering (bold, italic, inline code) in assistant messages.
- **AI agent tool set (21 tools)**: `semantic_search`, `keyword_search`, `get_notes`, `get_selected`, `get_last_focused`, `get_all_notes`, `get_all_notes_of_color`, `add`, `edit`, `remove`, `set_color`, `highlight_notes`, `add_tags`, `remove_tags`, `get_codebook`, `add_memo`, `create_connection`, `remove_connection`, `get_connections`, `get_groups`, `create_group`, `add_to_group`, `remove_from_group`. Destructive tools require user confirmation. Agent loops up to 50 iterations for multi-step tasks.
- **AI context-aware system message**: System prompt dynamically indicates whether the user currently has notes selected, providing relevant context for agent responses.
- **Hybrid search (BM25 + semantic + keyword fallback)**: Search combines BM25 text scoring with cosine similarity on embeddings, with keyword fallback for notes missed by both methods. Results displayed in a ranked panel with color-coded relevance badges (high/medium/low/keyword). Tunable via advanced settings (BM25 weight, relevance threshold, minimum semantic relevance).
- **Search results panel**: Floating panel with ranked entries showing relevance score, note text preview, and source type. Click a result to focus/scroll to that note.
- **Transformers.js embedding provider**: Fully in-browser embedding computation using models like `Xenova/bge-small-en-v1.5`, `Xenova/all-MiniLM-L6-v2`, or `Xenova/all-mpnet-base-v2`. No data leaves the browser.
- **OpenAI embeddings provider**: `text-embedding-3-large` and other OpenAI embedding models as a provider option.
- **OpenRouter LLM support**: Third AI chat provider alongside Ollama and OpenAI. Configure via Settings with API key and model name (e.g. `anthropic/claude-sonnet-4`).
- **Transcript import**: Import interview transcripts via Settings. Opens a full-screen viewer with speaker-labeled paragraphs. Click paragraphs to select, or highlight specific text and click "Mark Quote". Speaker filter buttons to hide/show speakers. On import, assign participant IDs per speaker (or a single ID for untagged transcripts). Notes created with color-coded speaker assignment and participant tags.
- **CSV loading**: Import notes from CSV files.
- **Participant ID filtering**: Filter bar includes a "Participant" section. Any note ending with (P1), (P2), etc. is automatically detected. Participant IDs appear as filterable chips. Filter bar auto-refreshes when notes are edited.
- **Enhanced filter system**: Filter bar supports filtering by tag, note color (color dots), participant ID, and type (Notes/Memos). All filters combine with AND logic.
- **Export system** (via Settings): CSV (notes + tags + groups + participants), Markdown report (organized by groups with memos and connections), Codebook CSV.
- **Note timestamps**: Notes track `createdAt` and `updatedAt`. Shown on hover. Memos show creation date prominently.
- **Selection rectangle**: Click-and-drag on canvas background draws a rubber-band selection rectangle to select multiple notes at once.
- **Group drag**: When multiple notes are selected, dragging one drags them all together with undo support.
- **Note resize**: Notes support manual resizing via drag handle.
- **Zoom (in/out/reset)**: Toolbar buttons for zoom in, zoom out, and reset (click percentage label). Zoom level persists per board.
- **Pan**: Click-and-drag on canvas background to pan the view.
- **Minimap**: Overview panel (bottom-right) showing scaled-down board. Click to pan. Toggle with "map" button.
- **Snap-to-grid**: Toggle Snap button (⊞). Notes snap to 20px grid during drag.
- **Computing embeddings overlay**: Progress bar overlay shown while computing embeddings across providers.
- **Privacy notice in settings**: Dynamic notice warns when data leaves local machine (OpenAI/OpenRouter) vs. stays local (Ollama/Transformers.js).
- **Compressed auto-save**: Auto-save uses gzip compression via `CompressionStream`/`DecompressionStream` with base64 encoding for efficient localStorage usage.
- **Focused note animation**: Purple pulse animation highlights notes when AI adds or focuses on them.
- **Sample board**: Shown when no autosave data is detected, with notes explaining current features.
- **GitHub link on launcher**: Footer on workspace launcher includes a link to the GitHub repository for contributing or giving feedback.
- **Favicon**: Splatter logo as browser tab favicon.
- **Multi-board tabs**: Tab bar supports up to 5 separate boards with independent state per workspace. Add, switch, rename, delete boards.
- **Keyboard shortcuts**:
  - `Ctrl/Cmd+Z`: Undo
  - `Ctrl/Cmd+Shift+Z` / `Ctrl/Cmd+Y`: Redo
  - `Ctrl/Cmd+S`: Save board
  - `Ctrl/Cmd+F`: Focus search input
  - `Ctrl/Cmd+D`: Duplicate selected notes
  - `Ctrl/Cmd+A`: Select all notes (in select mode)
  - `Delete` / `Backspace`: Delete selected notes or selected connection
  - `Escape`: Close panels / exit modes / clear search
  - `N`: Add new note
  - `M`: Add new memo
  - `G`: Create group zone
  - `S`: Toggle select mode
  - `C`: Toggle connect mode
  - `T`: Add tag to last focused note
  - `Arrow keys`: Nudge selected notes by 10px (`Shift+Arrow`: 1px)

### Changed
- **UI/UX redesign**: Balanced visual overhaul — soft Post-it-style note colors (including tan and gray), slate blue accent, single-row toolbar, warm canvas background. File operations (Load, Save, Export, Clear Board) moved to Settings modal.
- **Workspace-scoped storage**: Board data stored per-workspace (`splatterWS_{id}_board_{index}`) rather than globally. Old `splatBoards`/`splatAutosave` keys are legacy.
- **Auto-save every 2 seconds**: Workspace auto-saves on a 2-second interval.
- **Board state includes pan/zoom**: Scroll position and zoom level are preserved and restored per board.
- **Board state includes codebook metadata**: `tagHistory`, `tagDefinitions`, and `tagParents` are saved/restored with each board.
- **Connection UX**: No `prompt()` dialogs. Connections create instantly as "related". Inline popover for editing type/label/delete. First note shows pulsing blue ring in connect mode.
- **Group UX**: Groups are now persistent drop zones — create empty, drag notes in/out. Dragging a group header moves all member notes. Auto-grows to fit. No more select-then-group workflow.
- Note data model extended with `type`, `groupId`, `createdAt`, `updatedAt`, group position/size fields. All backward-compatible.
- Save format includes `groups` and `connections` arrays.
- AI "edit" tool re-renders note menu, pin indicator, and tags after modifying text.
- AI "get_all_notes" tool includes tags in response.
- Embedding button shows "Recompute (N new)" when new notes lack embeddings; auto-embeds when model is loaded.
- Participant ID extraction is case-insensitive and matches `(P1)` anywhere in note text.
- Raw tool call detection: Chat handler detects when an LLM returns a tool call as raw JSON in content and converts it automatically.

### Fixed
- Dragging tags from codebook onto notes now works correctly. File drop handlers no longer intercept tag drag events.
- Note menu and pin indicator lost when AI edited a note (pre-existing bug).
- Pin icon not appearing after note edit.
- Early returns on `finishEditing` when double-clicking in a textarea or pressing Enter.
- Color picker swatches match the note color palette.
- Export dropdown renders above tab bar (z-index fix).
- Filter bar refreshes participant list after note edits.
