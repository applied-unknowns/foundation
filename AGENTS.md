# Rules for this repository

Read the organization rules first: [`.github/AGENTS.md`](https://github.com/applied-unknowns/.github/blob/main/AGENTS.md). This file adds rules for this repository and never loosens those.

This repository is the working record of Applied Unknowns. It holds what the organization knows about itself: what is waiting on a decision, what is planned, what has been learned, and which repositories exist. Later it will hold the founding brief, the architecture decision records (ADRs), and the charter.

## Layout

| Path | Holds | Who writes |
| --- | --- | --- |
| `OPEN.md` | Items waiting on Justin's decision or attention | Agents add; Justin closes |
| `BACKLOG.md` | Planned work in order, and the icebox | Agents propose; Justin orders |
| `LESSONS.md` | Dated lessons and logged exceptions to the rules | Agents and Justin add; nobody rewrites |
| `INDEX.md` | One line per repository in the organization | Updated with every change that adds, renames, or retires a repository |

## Rules

| # | Rule | Status |
| --- | --- | --- |
| 1 | `LESSONS.md` is append-only. A lesson that turns out wrong gets a new entry that supersedes it; the old entry stays. | Proposed |
| 2 | An item leaves `OPEN.md` only in a pull request that says how it was resolved. Agents may propose closing an item; Justin merges the closure. | Proposed |
| 3 | A pull request that adds, renames, or retires a repository updates `INDEX.md` in the same pull request. | Proposed |
| 4 | Lines marked as Justin's statement are things he said. Agent readings are marked **Agent conclusion**. | Proposed |
