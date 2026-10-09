# Weekly Research Scheduled Task

Suggested schedule:

```text
Every Friday at 9:00 AM America/Detroit
```

Manual fallback:

```text
Run the weekly thunder research workflow now.
```

Use the manual fallback when the scheduled Friday run was missed because the
laptop was closed, offline, or the ChatGPT desktop app was not running.

Suggested task prompt:

```text
Every Friday morning, or whenever I manually ask you to run the weekly thunder research workflow, run my weekly research workflow.

Work in /Users/abieber/Repositories/thunder-stone00.

Read AGENTS.md, README.md, and inbox/weekly-prompts.md.

For each TODO item in the current weekly inbox:
- Check results/ and prior DONE items in inbox/weekly-prompts.md for related prior research.
- If the topic was already researched, either add a short follow-up note to the prior result or create a new dated result folder only if the new question materially changes the research.
- Research the topic using current web sources.
- Create outputs under results/YYYY-MM-DD/topic-slug/.
- Include summary.md, sources.md, notes.md, and open-questions.md.
- Put source links inline in summary.md and preserve all source links in sources.md.
- Mark the inbox item DONE.
- Add the Output path and all related paths beneath the completed inbox item.

After all current TODO items are handled:
- Archive this week's researched prompt batch to prompts/YYYY-MM-DD.md.
- Add a new dated section at the top of inbox/weekly-prompts.md for the next week.
- Leave that section ready for lightweight dictated capture with an example TODO item shape.
- Report what was researched, what was skipped, and where the outputs live.
```
