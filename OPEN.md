# Open items

Items waiting on Justin's decision or attention for this organization. Agents add; Justin closes by deleting the line in a pull request, with the outcome noted in the commit. Founding-brief decisions stay in the founding brief's open items list until the charter exists. The agent instructions for the whole organization are in [`.github/AGENTS.md`](https://github.com/applied-unknowns/.github/blob/main/AGENTS.md).

## Settings to change

- [ ] Ruleset `default-branch-pr-required`: turn on "Dismiss stale pull request approvals when new commits are pushed." The readback on 2026-10-25 showed it off.
- [ ] Same ruleset: turn on "Require review from Code Owners." `CODEOWNERS` merged in pull request #1, so rule 13 can now be enforced by the platform.
- [ ] Organization roles: assign the `agents` team the All-repository write role, or keep granting Write repository by repository. Today each new repository needs a manual grant.

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
