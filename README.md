# LN Roadmap

Static visual roadmap for Llama Naturals × Anatta. Single-file gantt with sprint banding, task-type pills (IMPL / TEST / BUG / SPIKE / CONV), today line, and day-of-N counter.

## Live

https://ln-roadmap-anatta.vercel.app/

## Deploy

Vercel auto-deploys `index.html` from `main` as a static site. No build step.

## Editing

`index.html` is the source. Update bars, milestones, and row meta directly. The today line and day counter recalculate on page load from `noticeStart` / `ganttStart` / `ganttEnd` in the inline script — bump those when the next 90-day window begins.

## Routine update flow

1. File the latest weekly sync transcript into `~/Documents/llamanaturals/project/transcripts/`.
2. Diff against the live `index.html` based on what shipped, slipped, was redirected, or got added.
3. Update `index.html`. Commit. Vercel redeploys.
