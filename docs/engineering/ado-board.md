## What it does

`ado-board` reads and updates work items on your team's Azure DevOps (ADO) board: User Stories, Bugs, parent and dependency links, tags, assignments, and Discussion comments.

It provides **board access**, not an implementation workflow. Asking about a card does not start coding, select a delivery process, or move the card to another column. It needs no repo tracker configuration or setup skill.

## When to reach for it

Type `/ado-board`, or the [agent](https://www.aihero.dev/ai-coding-dictionary/agent) reaches for it automatically when you ask to find, create, link, tag, comment on, or assign ADO work items.

## Prerequisites

The team's ADO plugin must provide `ado-access` for approved, authenticated ADO operations and `query-ado-work-items` for the shared board-scope cache.

## Board scope

Name your board or its saved alias. The skill matches that name against the shared per-user cache of projects, teams, and Area Paths. Without a name, it uses the cache only if there is exactly one board. Ambiguous choices are questions, not guesses.

The skill reads the cache but never edits it. If the cache is missing or invalid, `query-ado-work-items` owns building or refreshing it. Reads and writes stay within the resolved board, including membership checks for work items supplied by ID.

## Common questions

**Will this start an implementation workflow?**

No. It performs the requested board operations and stops. Reading a User Story does not authorize code changes or a delivery workflow.

**Do I need the setup skill or an issue-tracker config file?**

No. Provide a board name or alias, or use the only board in the cache.

**Will it move my cards or close finished work?**

No column moves or Ready changes are performed. State changes require an explicit request and cannot move the card to another column. Reporting completed work does not close it. The skill never deletes work items, links, comments, or attachments.

## It's working if

- The agent names the expected project, team, and Area Path before its first write.
- Requested work items appear under the right Area Path, with the links, tags, or comments you asked for.
- A board lookup ends with the requested results, without starting code work or moving a card.

## Where it fits

`ado-board` is a reach-for-it-anytime standalone skill. It uses the team's `ado-access` integration and shares the board cache owned by `query-ado-work-items`, rather than choosing an engineering flow. [ask-matt](https://aihero.dev/skills-ask-matt) remains the upstream router for the other skills.
