# Backlog

Work planned for this organization, in order. Agents propose additions in a pull request; Justin orders the list. Items waiting on a decision go in `OPEN.md` instead.

The plan comes from [issue #2](https://github.com/applied-unknowns/foundation/issues/2), which keeps the rationale. This file is the only live work queue.

## Active: M0, charter and repository strategy

Approved by Justin on #2, 2026-10-27. At most two tasks are active at once, following the provisional scope budget proposed in #2; this is a bootstrap working limit, not an organization-wide rule. Each task has one author; the other agent gives the first review; Justin approves.

| Task | Issue | Author | First review | Starts |
| --- | --- | --- | --- | --- |
| FND-01 Charter, invariants, and acceptance scenario | [#3](https://github.com/applied-unknowns/foundation/issues/3) | ChatGPT | Claude | Now |
| FND-02 Inventory and keep/change decision | [#4](https://github.com/applied-unknowns/foundation/issues/4) | Claude | ChatGPT | Now |
| FND-03 Repository boundaries and promotion policy | [#5](https://github.com/applied-unknowns/foundation/issues/5) | Claude | ChatGPT | After FND-02 merges |
| FND-04 Agent identity, authority, and permissions | [#6](https://github.com/applied-unknowns/foundation/issues/6) | ChatGPT | Claude | After FND-01 merges |

## Provisional: M1 to M5

Candidates from #2, deliberately not active. Proposed breadth is not work in progress. Each becomes active only when Justin approves its milestone, and may be merged, dropped, or reordered as M0 teaches us.

- **M1, evidence before design:** FND-05 research protocol, FND-06 eight research packets, FND-07 synthesis and decision gate.
- **M2, governance and continuity:** FND-08 instruction adapters, FND-09 state and provenance schemas, FND-10 decision ledger and scope control, FND-11 cold-start continuity test.
- **M3, intent and task engineering:** FND-12 inquiry enhancement protocol, FND-13 intent taxonomy and authorization gate, FND-14 bounded task contracts, FND-15 evaluation set.
- **M4, execution and verification:** FND-16 reproducible baseline, FND-17 protected workflow and checks, FND-18 minimal agent runner, FND-19 security and isolation.
- **M5, end-to-end proof:** FND-20 first vertical slice, FND-21 cross-model evaluation, FND-22 acceptance and promotion.

## Icebox

Real ideas, deliberately not being worked. One line each. Justin moves an item out.

- Joint agent approval for a defined class of pull requests (paused 2026-10-25).
- A push ruleset restricting `.github/workflows/` changes to code owners.
- Organization Discussions as a limited Roundtable.
- Default issue templates for the organization.
- Run M1's research protocol before finishing M0, so M0 is decided from fuller evidence (Justin's suggestion on #2, 2026-10-27; he chose to keep the current order).
