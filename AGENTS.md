# thunder-stone00

This repo stores recurring research prompts, notes, sources, results, and durable
workflow-audit history.

## Research Capture

When Andy dictates or requests a research task to be done later:

- Add it to `inbox/weekly-prompts.md`.
- Keep capture lightweight as a `TODO` bullet.
- Include `Related paths:` and `Output:` fields.
- Add local files, notes, projects, Jira issues, Confluence pages, prior result
  folders, or external links that seem related.
- Do not require a research brief unless explicitly requested.

## Research Runs

When performing a research run:

- Read `README.md` first.
- Use the definitions in `README.md#definitions` as the source of truth for
  statuses, paths, and result terms.
- Treat "run the weekly thunder research workflow now" as the manual fallback
  for a missed scheduled run.
- Check `inbox/weekly-prompts.md` and `results/` for prior related research.
- Write outputs under `results/YYYY-MM-DD/topic-slug/`.
- Include `summary.md`, `sources.md`, `notes.md`, and `open-questions.md`.
- Cite sources inline in summaries and preserve links in `sources.md`.
- Mark completed inbox items `DONE`.
- Add the output path and related paths beneath the completed inbox item.
- Add a new dated inbox section for the next capture period after the run.

Keep this system useful and low-friction. The inbox is for rough capture; the
result folders are where polish belongs.

## Codex Workflow Audits

- Use the `codex-workflow-audit` skill from `moon-stone00` as the source of truth
  for audit method, report shape, and scheduled-task instructions.
- Save reports under `audits/codex-workflow/YYYY-MM-DD/scope-slug/report.md`.
- Update `audits/codex-workflow/index.md` after each run.
- Do not apply the research inbox or four-file result contract to workflow audits.
- Preserve prior reports and recorded decisions; never overwrite a distinct run.
