---
"mattpocock-skills": patch
---

Add `ado-board`, a standalone, model-invoked engineering skill for reading and updating the team's Azure DevOps work items. Resolve the board from the user's request or shared per-user board-scope cache, scope operations to that board, and preserve revision guards and human ownership of board columns. Board access does not select or start an implementation workflow and needs no repo tracker configuration. Remove `setup-matt-pocock-skills` from this fork and its plugin listings; references inside the other skills remain unchanged from upstream.
