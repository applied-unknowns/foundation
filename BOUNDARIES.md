# Repository boundaries and promotion

**Status:** Proposed. Nothing here is in force until Justin approves it.
**Task:** [FND-03, issue #5](https://github.com/applied-unknowns/foundation/issues/5), part of [issue #2](https://github.com/applied-unknowns/foundation/issues/2).
**Drafter:** Claude (`jhilliardx-claude-ai`).
**Reach:** This file governs only the `applied-unknowns` organization. Justin's personal repositories follow their own rules; this file says only what must be true of work when it crosses into the organization.

Rule numbers below refer to the organization rules in [`.github/AGENTS.md`](https://github.com/applied-unknowns/.github/blob/main/AGENTS.md).

## 1. What goes where

| Place | What belongs there |
| --- | --- |
| `applied-unknowns` | Work for Applied Unknowns, and personal projects Justin chooses to bring in (rule 9 allows personal projects). Public by default (rule 8). |
| Justin's personal repositories (`jhilliardx`) | Everything rule 9 excludes from the organization: personal and family matters, anything tied to his employer, and anything against the organization's values. Also personal experiments and work not yet chosen for the organization. |

A piece of work belongs in the organization only if all three are true:

1. It is organization work, or a personal project Justin decides to bring in.
2. Rule 9 does not exclude it.
3. It can be public, or it has a stated reason to be private (rule 8).

Anything else stays personal. When it is unclear, it stays personal and the question goes to `OPEN.md`.

Justin's statement (Claude session, while setting up the organization): existing personal repositories stay personal for now, and work moves into the organization case by case as it touches company work. Nothing moves automatically.

## 2. Identities on each side

**In the organization:** each agent writes only as its own account (rule 3), and agents never use `jhilliardx` (Identities table).

**In personal repositories:** Justin's statement (Claude session, 2026-10-25): agents currently work there through connections signed in as `jhilliardx`, he accepts that risk, his personal repositories will be protected and require pull requests, and he will audit activity in them.

So in a personal repository, the commit author does not show who drafted the work. **Agent conclusion:** that is workable, because the promotion rules below never rely on personal-repository authorship. They require the promoting pull request to state who drafted the work. Whether to keep this practice is open in `OPEN.md`.

## 3. Promotion: bringing work into the organization

Promotion means any content that originated outside the organization entering an organization repository.

| # | Rule |
| --- | --- |
| P1 | Promotion happens only through a pull request in the receiving repository, reviewed under rule 5 and merged by Justin (rules 1 and 2). |
| P2 | The pull request names the source: repository, paths, and a link to the exact commit. It also names who drafted the content (Justin, which agent, or a third party), whatever the source repository's commit author says. |
| P3 | Promotion copies current files, never history. No branch or history from a personal repository is pushed or merged into an organization repository, including feature branches. History carries every earlier version of a file, including deleted credentials and personal information, and authorship that section 2 says may be misleading. |
| P4 | Before the pull request opens, the drafter screens the content for: credentials; private personal information and anything rule 9 excludes; and third-party material, listed with its license. |
| P5 | No `LICENSE` exists yet (`OPEN.md`), so promoted content is all rights reserved, like the rest of the organization, until that is decided. Third-party material is promoted only if its license allows publishing it in a public repository, with its notices kept. |
| P6 | AI involvement is credited: the drafter line in P2 names any agent that drafted the content (rule 4). |

Promotion into `.github` follows the same rules, but Justin carries the files, because neither agent can write there (`LESSONS.md` row 5).

Moving organization content into a personal repository is outside this file. Organization content is public.

## 4. How each rule is checked

| Rule | Check | Enforced by |
| --- | --- | --- |
| P1 | Read the default branch's rules: `gh api repos/applied-unknowns/<repository>/rules/branches/main` must show a `pull_request` rule with at least one required approval. Readback on `foundation`, 2026-10-27: present, one approval required. | GitHub |
| P2 | Reviewer confirms the source link points to a specific commit and the drafter line is present. | Reviewer |
| P3, on `main` | The same readback must show `allowed_merge_methods: ["squash"]` and `required_linear_history`, so a pull request lands as one new commit and no outside history reaches `main`. Readback on `foundation`, 2026-10-27: both present. | GitHub |
| P3, on branches | Reviewer confirms every commit in the pull request descends from the organization's `main`. GitHub does not prevent pushing outside history to a feature branch, where it is public even if never merged. | Reviewer |
| P4, credentials | Secret scanning and push protection were applied to the organization through GitHub's recommended security configuration (`LESSONS.md` row 22, Justin's statement). Agent accounts cannot read the repository's security settings (GitHub's application programming interface (API) returned no security fields to `jhilliardx-claude-ai` on 2026-10-27), so Justin confirms them on the settings page. | GitHub, confirmed by Justin |
| P4, personal information and rule 9 | No automated check exists. The drafter checks by hand and ticks the matching pull request template item. | Drafter and reviewer |
| P4, third party; P5; P6 | Reviewer confirms the license list and the credit line. | Reviewer |

### Known gaps

- Push protection blocks credentials in commits made on the command line, in the web interface, and through the API, but [GitHub's documentation](https://docs.github.com/en/code-security/concepts/secret-security/about-push-protection) does not claim it detects every secret, and by default anyone with write access can bypass it by giving a reason. Both agent accounts have write access. This belongs to FND-04 ([issue #6](https://github.com/applied-unknowns/foundation/issues/6)).
- Nothing automated catches private personal information. It depends on the drafter and the reviewer.
- Nothing prevents outside history being pushed to an organization feature branch. Only review catches it.

## 5. Open decision

Recorded in `OPEN.md`: whether agents keep working in personal repositories as `jhilliardx`, or get their own accounts added there. Own accounts would make personal-repository authorship trustworthy, at the cost of more setup. This file works either way.
