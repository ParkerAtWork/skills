## What it does

`ado-board` lets the engineering skills use an Azure DevOps (ADO) board as their issue tracker. When `to-spec` publishes a spec, `to-tickets` links tickets with blocking edges, `triage` applies a label, or `wayfinder` claims a ticket, this skill turns that step into the matching work-item operation on the right board: a User Story or Bug, a Parent link, a Predecessor link, a tag, a Discussion comment.

It never guesses which board. It reads the per-user **board-scope cache** that the team's ADO skills already share, matches the board named in the repo's tracker config, and scopes every read and write to that board's Area Paths. It also never treats "close" the way GitHub does: on a board where column placement, Ready, and Blocker carry meaning, finished work is commented on and linked, and column moves stay with the people who own the board.

## When to reach for it

Type `/ado-board`, or the [agent](https://www.aihero.dev/ai-coding-dictionary/agent) reaches for it automatically whenever a skill needs the issue tracker and the repo's tracker is Azure DevOps.

| Your situation | Reach for |
| --- | --- |
| Your repo's work lives on an ADO board and you want the spec and ticket flows to land there | `ado-board`, after setup |
| The repo isn't configured for any tracker yet | [setup-matt-pocock-skills](https://aihero.dev/skills-setup-matt-pocock-skills) first, and pick Azure DevOps |
| You only want to look something up on the board, not run a flow | The team's read-only `query-ado-work-items` skill |

## Prerequisites

- The team's ADO plugin, which provides `ado-access` (the approved way to call ADO) and `query-ado-work-items` (which builds the board-scope cache).
- [setup-matt-pocock-skills](https://aihero.dev/skills-setup-matt-pocock-skills) run in the repo with Azure DevOps chosen, so `docs/agents/issue-tracker.md` names the board.

## The board-scope cache

The cache is a per-user file that maps each board (project, team, Area Paths) to its IDs. It is built once by `query-ado-work-items` and refreshed only with your permission when a mapping looks wrong. `ado-board` reads it and never writes it, so every ADO skill agrees on what "the board" means. If the cache is missing or suspect, the agent asks `query-ado-work-items` to build or refresh it before going on.

## Common questions

**Will it move my cards across the board?**

No. Column moves, the Ready flag, and the Blocker field belong to the board's owners. `ado-board` comments, links, tags, and assigns; it asks before changing a state, and only removes an item with your go-ahead. It never deletes anything.

**Where do triage labels go?**

Into work-item tags, using the strings in `docs/agents/triage-labels.md`. An external blocker is the Blocker field, not a tag.

## It's working if

- Tickets from `to-tickets` appear on your board under the right Area Path, with Parent and Predecessor links you can see in ADO.
- The agent names the project, team, and Area Path before its first write, and they're the board you expected.
- Finished work shows a comment and a linked branch or PR, and the card is still in the column a human put it in.

## Where it fits

`ado-board` is a **vocabulary layer** under the main flow, the same way [domain-modeling](https://aihero.dev/skills-domain-modeling) sits under grilling: it doesn't add a step, it changes where the tracker steps land.

- [setup-matt-pocock-skills](https://aihero.dev/skills-setup-matt-pocock-skills) points the repo at it, because the other skills only reach it through the tracker config.
- [to-tickets](https://aihero.dev/skills-to-tickets) is its heaviest user, because blocking edges become native Predecessor links.

[ask-matt](https://aihero.dev/skills-ask-matt) routes across the whole set when you are unsure which skill the situation wants.
