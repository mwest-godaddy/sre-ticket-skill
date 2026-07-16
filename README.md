# sre-ticket-skill

A [Claude Code](https://claude.com/claude-code) / Claude **skill** for writing, validating,
classifying, and improving SRE Jira tickets.

It encodes Google SRE principles adapted for **Kanban** (not Scrum) teams: a mandatory
five-type work taxonomy (Incident / Toil / Interrupt / Engineering / Overhead), the 50% ops
rule, SLO- and error-budget-driven prioritisation, a four-column board, a triage-readiness
checklist, per-type ticket templates, and a validation rubric.

> This repository is the **source** for the skill. It is intentionally *not* checked in under
> `.claude/skills/`, so cloning this repo doesn't auto-activate the skill in this project.
> Install it where you actually want to use it (see below).

## Layout

```
sre-ticket-skill/
└── skills/
    └── sre-ticket/
        └── SKILL.md      # the skill (frontmatter + instructions)
```

This mirrors the recommended skill anatomy — one directory per skill, containing a `SKILL.md`
with YAML frontmatter (`name`, `description`) and Markdown instructions. Bundled resources
(`scripts/`, `references/`, `assets/`) can be added alongside `SKILL.md` later if needed.

## Installing

Copy the `sre-ticket` directory into a skills location Claude Code discovers:

**Per-project** (available in one repo):

```bash
mkdir -p /path/to/your-repo/.claude/skills
cp -R skills/sre-ticket /path/to/your-repo/.claude/skills/
```

**Personal** (available everywhere for your user):

```bash
mkdir -p ~/.claude/skills
cp -R skills/sre-ticket ~/.claude/skills/
```

Once installed, the skill activates when you ask Claude to write, review, or classify an SRE
ticket, or explicitly via `/sre-ticket`, `/sre-validate`, or `/sre-classify`.

## Modes

The skill detects which mode you need:

- **WRITE** — draft a new ticket from a rough idea or Slack thread, via one round of questions at a time
- **VALIDATE** — audit an existing ticket against the SRE quality rubric (scored PASS / WEAK / FAIL)
- **CLASSIFY** — walk a decision tree to determine the correct work type
- **IMPROVE** — validate, then rewrite a ticket with a changelog

## Team customisation

Two things are team-specific and should be maintained outside the skill (e.g. a Confluence page
linked from the Jira project description), then reflected here as your team evolves:

- The **Service / Product** field list and its **scope classification** (In Scope – Operated /
  Advisory / Provisional / Out of Scope). The skill currently ships with `cPanel`, `AAB`, and
  `MWP` as *In Scope — Operated*; adjust these in `SKILL.md`.
- Keep the VALIDATE rubric in sync with your team's Triage Readiness Checklist.
