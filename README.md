# AI Automation Agency — Agent Team

Three Claude Code agents that run the front of your agency pipeline, built on the
playbook in [`knowledge/playbook.md`](knowledge/playbook.md). They implement the
playbook's **Step 7 ("Agent Team")** under its hard rule:

> **Agents draft, humans send.** Nothing reaches a client without human review.

## The three agents

| Agent | What it does | Playbook step |
|-------|--------------|---------------|
| **Lead Generation Agent** | Finds & enriches real companies + buyers in your niche from public web sources; writes them to `output/leads.csv` | 1 (Market), 3 (source) |
| **Outreach Agent** | Writes personalized cold email + LinkedIn copy and creates **Gmail drafts** (never sends) | 3 (send), 4 (Message) |
| **Sales Agent** | Handles replies, drafts audit proposals, prices builds/retainers, tracks the pipeline | 2, 4, 5→6 |

Agent definitions live in [`.claude/agents/`](.claude/agents). Claude Code loads
them automatically — invoke with e.g. *"Use the lead-generation-agent to build a
list for my niche."*

## Setup (do this first)

1. **Fill in [`knowledge/icp-config.md`](knowledge/icp-config.md).** Nothing works
   until your niche, buyer, painful process, offer, signature, and booking link
   are defined. This is the playbook's "market first" rule.
2. Confirm the **Gmail** connector is connected (it is used for drafts).
3. Add a **booking link** (Calendly/Cal.com) to the config so the Sales Agent can book.

## Typical weekly flow

1. `lead-generation-agent` → adds verified leads to `output/leads.csv`.
2. You review the leads.
3. `outreach-agent` → creates Gmail drafts + a LinkedIn queue. **You review and send.**
4. Replies come in → `sales-agent` → drafts responses, books calls, writes proposals.
5. You review, send, and run the calls.

## What this system genuinely does — and does NOT do

**Does (works in this environment):**
- Finds *real* companies/buyers via public web search.
- Writes personalized, playbook-structured copy.
- Creates *real* Gmail drafts for your review.
- Generates audit proposals and tracks the pipeline as files.

**Does NOT (be clear-eyed about this):**
- ❌ No LinkedIn Sales Navigator / paid enrichment — lead volume & email coverage
  are limited to public data. Hitting the playbook's 400 contacts/month needs a
  paid enrichment tool.
- ❌ No auto-send — drafts only, by design.
- ❌ No LinkedIn automation — LinkedIn copy is queued for you to send manually.
- ❌ No calendar booking — the Sales Agent inserts your booking link + proposed times.
- ❌ No fabricated results — agents never invent clients, stats, or ROI. Where you
  have no proof yet, copy uses honest, non-claiming framing.

## Files

```
.claude/agents/     the three agent definitions
knowledge/          playbook.md · icp-config.md · message-frameworks.md
templates/          lead-tracker.csv · audit-proposal.md
output/             runtime: leads.csv, pipeline.md, proposals/ (generated)
```
