# Open items

Items waiting on Justin's decision or attention for this organization. Agents add; Justin closes by deleting the line in a pull request, with the outcome noted in the commit. Founding-brief decisions stay in the founding brief's open items list until Justin decides whether the briefs feed the charter (below). The agent instructions for the whole organization are in [`.github/AGENTS.md`](https://github.com/applied-unknowns/.github/blob/main/AGENTS.md).

## Settings to change

- [ ] Ruleset `default-branch-pr-required`: turn on "Dismiss stale pull request approvals when new commits are pushed." The readback on 2026-10-25 showed it off.
- [ ] Same ruleset: turn on "Require review from Code Owners." `CODEOWNERS` merged in pull request #1, so rule 13 can now be enforced by the platform.
- [ ] Organization roles: assign the `agents` team the All-repository write role, or keep granting Write repository by repository. Today each new repository needs a manual grant.

## Decisions from issue #2

Justin approved the ten invariants, tasks FND-01 to FND-04, and Claude Opus 5.5 with ChatGPT 6 as the first cross-model test pair on [#2](https://github.com/applied-unknowns/foundation/issues/2), 2026-10-27. These are still open:

- [ ] Ratify or revise the end-to-end acceptance scenario in #2. FND-01 writes its pass criteria either way.
- [ ] Whether the three founding briefs become source material for the charter (FND-01). Both agents recommend yes.
- [ ] A research effort and spending ceiling, needed before M1's research packets are dispatched.
- [ ] Whether the foundation must be complete before the first product work starts, or both may run in parallel. Raised in Claude's review on #2 (point 7); the proposed charter in #11 also lists it.
- [ ] Final wording of the organization's purpose, and how the foundation relates to broader product work. Listed as open in the proposed charter in #11.
- [ ] Whether agents keep working in personal repositories as `jhilliardx`, or get their own accounts added there so personal-repository authorship can be trusted. `BOUNDARIES.md` (FND-03) works either way.
- [ ] The collaborative proposal resolution rule from #2: ChatGPT drafts it for `.github/AGENTS.md`, Claude reviews, Justin carries it; or Justin declines it.

## Decisions

- [ ] Contributor terms and a license. `CONTRIBUTING.md` holds outside pull requests until these are decided; no `LICENSE` exists yet, so all rights are reserved by default.
- [ ] Rules 14, 15, and 16 in `AGENTS.md` are Proposed. Set, change, or reject each.
- [ ] A confidential route for conduct reports (for example, an organization email address). `CODE_OF_CONDUCT.md` says none exists yet.
- [ ] Whether to commit to an acknowledgment time for security reports. Removed from `SECURITY.md` in review because Justin had not stated it.
- [ ] Two-factor authentication on both agent accounts, then require it for the organization.

## Later

- [ ] When a repository has continuous integration: add required status checks and code scanning results to the ruleset, and pin actions to commit hashes.
- [ ] When agents run on application programming interface (API) access: one GitHub App per vendor replaces each interim user account.
- [ ] A push ruleset restricting changes to `.github/workflows/` to code owners.
- [ ] Before the first private repository: Advanced Security bills per active committer to private repositories, and both agent accounts count as committers. Decide whether the security configuration covers private repositories.
