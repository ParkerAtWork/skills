# Issue tracker: Azure DevOps

Issues and specs for this repo live as work items on an Azure DevOps (ADO) board. For every tracker operation, call the Skill tool with `ado-board`: it resolves the board below from the shared per-user board-scope cache and maps each operation to ADO.

## Board

- **Board:** `<board alias or team name, as it appears in the board-scope cache>`
- **Area Path:** `<only needed when the board has more than one Area Path>`
- **Ticket type:** `User Story`
- **Bug type:** `Bug`
- **Map type:** `User Story`
- **Resolved state:** `<state a resolved wayfinder ticket moves to; leave blank to keep the state and tag it instead>`

## When a skill says "publish to the issue tracker"

Create a work item on the board above through `ado-board`.

## When a skill says "fetch the relevant ticket"

Read the work item by ID through `ado-board`. The user will normally pass the ID directly.

## Closing work

Agent-finished work is not closed here: comment and link the branch or PR, and leave column moves to the team's board process. See `ado-board` for wontfix and wayfinder resolution.
