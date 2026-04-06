# Contributing to AI Pulse

Thanks for wanting to add something. This doc tells you exactly what belongs here and how to do it right.

---

## What Belongs Here

**Models** — New releases that represent a genuine capability jump or license change worth knowing about. Not every checkpoint drop.

**Tools** — Things that work in production or have meaningfully changed how people build. Not demos, not early-access only, not "coming soon."

**Research** — Papers with findings that changed how the field thinks or builds. Not incremental results, not workshop papers without follow-up.

**AI Security** — Attack techniques, defense tools, standards. This section has a higher bar than most — links to papers or working code, not blog posts about blog posts.

**Fracture Lines** — Open problems with honest status. If you're adding a new problem category, it needs sources and a "status" assessment. If you're updating an existing one because something changed, note what changed and link the evidence.

---

## What Doesn't Belong Here

- Paywalled content without a freely accessible preprint or summary
- Duplicate entries (search before you add)
- Tools you haven't personally used or verified work
- Anything you'd describe as "promising" or "upcoming" — add it when it ships
- Marketing copy — descriptions should be accurate, not promotional

---

## How to Submit

1. Fork the repo
2. Add your entry in the right section — keep the existing table format
3. Include a working source link
4. If you have personal experience with the tool, add a short note in your PR description — it helps with the curator's take notes
5. Open a PR with the title: `[Category] Add <name of what you're adding>`

**One entry per PR** unless you're proposing a new section — open an issue for that first.

---

## Updating Fracture Lines

[FRACTURE-LINES.md](FRACTURE-LINES.md) has a higher bar than the main README.

To add or update a Fracture Lines entry:
- Claims need citations — link papers, not blog posts where avoidable
- "The problem" section must be concrete
- Status must be honest — active research ≠ solved

Open an issue first if you're proposing an entirely new problem category.

---

## Updating the Changelog

If your PR adds something meaningful, add a line to [CHANGELOG.md](CHANGELOG.md) under the current month.

Format:
```
**[Date] Category — Short description**
- What was added and why it matters
```

---

<sub>Part of <a href="README.md">AI Pulse</a></sub>
