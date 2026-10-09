# thunder-stone00

This repo is the home for recurring research capture, notes, sources, and
weekly research results.

## Workflow

1. Capture rough research tasks in `inbox/weekly-prompts.md` throughout the
   week.
2. When the weekly research run starts, copy or move the active inbox items into
   `prompts/YYYY-MM-DD.md`.
3. Before researching, check existing inbox history and `results/` for related
   topics.
4. Write completed research to `results/YYYY-MM-DD/topic-slug/`.
5. Mark the original inbox item as `DONE` and add the result path plus any
   related paths.

## Definitions

- `Inbox`: The active capture file at `inbox/weekly-prompts.md`. This is where
  rough research tasks go before a research run.
- `TODO`: A research item that has been captured but not yet researched.
- `IN_PROGRESS`: A research item currently being worked.
- `DONE`: A research item that has completed outputs and an `Output:` path.
- `SKIPPED`: A research item intentionally not researched during a run.
- `Related paths`: Local files, prior research folders, Jira issues, Confluence
  pages, source docs, or external links that may help interpret the task.
- `Output`: The primary completed research summary path, usually
  `results/YYYY-MM-DD/topic-slug/summary.md`.
- `Prompts`: Weekly archived copies of researched inbox items, stored under
  `prompts/YYYY-MM-DD.md`.
- `Results`: Completed research output folders, stored under
  `results/YYYY-MM-DD/topic-slug/`.
- `Topic slug`: A short lowercase folder name for a research topic, using
  hyphens instead of spaces.
- `Open questions`: Questions that remain unresolved or should be revisited
  later.

## Inbox Convention

The inbox should stay easy to dictate into. Use simple bullets, not briefs.

```markdown
- TODO Research whether paid search incrementality testing has changed in 2026.
  Related paths:
  Output:
```

When research is complete:

```markdown
- DONE Research whether paid search incrementality testing has changed in 2026.
  Related paths:
  - research/results/2026-10-16/paid-search-incrementality/
  - work/projects/example-context.md
  Output: research/results/2026-10-16/paid-search-incrementality/summary.md
```

Use `TODO`, `IN_PROGRESS`, `DONE`, or `SKIPPED` as the status. If an item has
already been researched, prefer adding the new question as a related follow-up
instead of creating a duplicate result.

## Result Folder Convention

Each researched topic should get its own folder under the weekly result date:

```text
results/
└── YYYY-MM-DD/
    └── topic-slug/
        ├── summary.md
        ├── sources.md
        ├── notes.md
        └── open-questions.md
```

- `summary.md`: concise synthesis with inline links to supporting sources.
- `sources.md`: all sources used, grouped by topic or claim.
- `notes.md`: working notes, quotes within copyright limits, and observations.
- `open-questions.md`: unresolved questions and useful future follow-ups.

## Research Template

Use `templates/research-result.md` as the starting shape for `summary.md`.
Keep the summary readable first, with citations close to the claims they
support.

## Scheduling

Use `automation/scheduled-task.md` as the source-of-truth prompt when creating
or updating the weekly scheduled research task. If the Friday run is missed
because the laptop was closed, offline, or the ChatGPT desktop app was not
running, use the manual fallback:

```text
Run the weekly thunder research workflow now.
```
