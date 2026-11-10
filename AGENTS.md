# AGENTS.md

## Fulservice project tracking (GitHub Project "Fulservice")

Board: https://github.com/orgs/GenAI-Labs-Inc/projects/1. This section overrides other merge/QA rules in this repo for Fulservice work.

- **Issues live in `GenAI-Labs-Inc/eme-server`**, for every EME repo. Set the project field *Component* to the repo you touch.
- **Flow**: Backlog -> In progress -> In review -> Testing local -> Testing EME server -> Deployed to PROD.
- **Only own issues**: work only on issues assigned to the person who launched the session (`gh issue list -R GenAI-Labs-Inc/eme-server --assignee @me`). Someone else's issue: comment, don't implement.
- **Create**: `gh issue create -R GenAI-Labs-Inc/eme-server --assignee @me --label fulservice --project "Fulservice"`. Fill Priority, Size, Owner type (AI/Human/Pair), Agent, Component.
- **Start**: Status -> In progress. Branch from `fulservice`.
- **PR**: target `fulservice`, body has `Closes GenAI-Labs-Inc/eme-server#<n>`. The project moves it to In review on link and Testing local on merge.
- **Testing EME server / Deployed to PROD**: only a human sets these (and the *Deployed to test on* / *Deployed to PROD on* dates).
- **Blocked**: comment, label `blocked`, Status -> Backlog, Owner type -> Human. Never change Priority or Milestone without a human.
- **CI cost**: run CI once, not on every push. Light checks (build + affected tests) on PRs to `fulservice`; full suite only once on the `fulservice` -> `tested` promotion PR. Any workflow added must use `concurrency` with `cancel-in-progress`, `paths` filters, and no scheduled runs. Don't push repeatedly to a PR just to re-trigger CI.
- Each machine once: `gh auth refresh -s project`.
