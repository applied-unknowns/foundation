# Lessons

Dated lessons from operating this organization. Each lesson says what happened, what we do now, and where the procedure lives if it became one. Lessons are added, never rewritten; a lesson that turns out wrong gets a new entry that supersedes it.

Lines marked **Agent conclusion** are Claude's or ChatGPT's reading of what happened, not Justin's statement.

## 2026-10-25: First repository and first pull request

### Setup

| # | What happened | What we do now |
| --- | --- | --- |
| 1 | The `.github` repository needs a default branch before anyone can branch from it or attach rules to it. | Create new repositories with "Add a README file" checked, so `main` exists. The placeholder is replaced by the first pull request. |
| 2 | One organization-level branch ruleset protects every repository's default branch, including repositories created later. Status-check and code-scanning rules were left off because they block every merge until checks exist. | Add those rules when a repository has continuous integration. Enable "Require review from Code Owners" now that `CODEOWNERS` exists (see `OPEN.md`). |
| 3 | The ruleset bypass is set to organization admin, pull requests only. That lets Justin merge any pull request without its required approvals. It does not allow direct pushes to `main`. | Documented in `AGENTS.md`. **Agent conclusion:** a first draft described it as "for pull requests he authors," which was wrong; a ruleset's effect is checked against GitHub's description of the setting, not inferred. |
| 4 | A ruleset's effective rules on a public repository can be read from outside without credentials. The readback showed "dismiss stale approvals" off, against the plan. | After any ruleset change, read the effective rules back and compare to the plan. |

### Identities and tools

| # | What happened | What we do now |
| --- | --- | --- |
| 5 | Neither agent can write to `.github`, even though both agent accounts have Write. Claude's cloud sessions cannot attach any repository whose name begins with a dot; ChatGPT also cannot write there (Justin's report, cause not yet known). | For dot-named repositories, Justin carries the work using the procedure in `.github/AGENTS.md`, "Carrying an agent's work." Working records live in `foundation` so they are not affected. |
| 6 | The connector that reaches Justin's own account can read this organization's public repositories but cannot write to it, because its GitHub app is not installed on the organization. | Keep it that way. An agent connection with owner rights standing on the organization is what the Identities table rules out. |
| 7 | The plan Claude first recommended for landing `.github` pull request #1 had ChatGPT open the pull request with Claude's draft, and Claude review it. That plan would have shown ChatGPT as the submitter of work Claude drafted, and had the drafter review its own draft. Carrying alone causes neither problem when the drafter is stated and the reviewer is someone else. | Keep three roles distinct and record each: submitter (who opens the pull request or pushes), drafter (who wrote it), and reviewer (never the drafter). **Agent conclusion:** check every option against all the rules before recommending one. |
| 8 | The co-author line `Claude <noreply@anthropic.com>` credited Anthropic's own "Claude" GitHub account, not `jhilliardx-claude-ai`. GitHub links co-authors by email. | Use each account's commit email from the Identities table (rule 15, proposed). The merged commit for pull request #1 was left as is: rewriting `main` is blocked, and the commit's prose names the correct account. |
| 9 | The first branch was named `agents/readme-set` though Justin pushed it. | Branch prefix names the account that pushes (rule 14, proposed). Authorship is stated in the commit and pull request, not the branch. |

### The GitHub web interface

| # | What happened | What we do now |
| --- | --- | --- |
| 10 | Dragging a folder into Upload files flattened it: `profile/README.md` arrived as `README (1).md` at the root. | Upload root files only; add nested files with Create new file and the full path. |
| 11 | Propose changes created a branch and a commit but no pull request. The pull request exists only after Create pull request, and has a number. | Confirm the pull request number before asking for review. |
| 12 | The default squash message stacks every branch commit message, including any pasted pull request body. | Replace it at merge with a clean title and description. Messy branch commits do not matter under squash merging. |
| 13 | Co-author trailers pasted into a web form lost their angle brackets and merged onto one line, so GitHub ignored them. | Each trailer on its own line, angle brackets intact, at the very end of the message. Check the commit page after merging. |

### Review

| # | What happened | What we do now |
| --- | --- | --- |
| 14 | ChatGPT edited the pull request #1 files before upload, so it could not be the independent reviewer under rule 5. | When a reviewer has edited the work, either name that in the review as a confirmation rather than an independent review, or use a reviewer that has not touched it. |
| 15 | Pull request #1 merged with no review on record, using the admin bypass. | Logged here as the first exception (rule 16, proposed). Pull request #2 goes through the full loop. |
| 16 | Step-by-step instructions given across several messages, with changes between them, were hard to follow. | Justin's statement: for pull requests an agent prepares, tell him only the action he needs to take (for example "approve pull request #2" or "have ChatGPT review this pull request"), not a walkthrough. When a walkthrough is needed, give one ordered list and restate the whole list if anything changes. |
| 17 | ChatGPT's review of pull request #2 found five blocking problems Claude missed, including that `GOVERNANCE.md` is not one of GitHub's default community health files, and a permission table that read as letting agents merge. | **Agent conclusion:** independent review works and is worth the wait. A claim about how GitHub behaves is checked against GitHub's documentation before it ships. Default issue templates must live in `.github/ISSUE_TEMPLATE/` in the `.github` repository. |
| 18 | Pull request #2 merged through the admin bypass. Neither agent can post reviews in `.github`, so both of ChatGPT's review rounds (request changes, then approve) and Claude's reply were run outside GitHub and posted verbatim by Justin as comments, with the bypass explained on the pull request. | An independent review did happen, so this was not an exception under rule 16. The bypass was of GitHub's approval gate only, which cannot count a review posted by Justin. This is the working pattern for `.github` until an agent can review there. |
| 19 | The co-author line in pull request #2's merge commit lost its angle brackets again, so GitHub did not credit `jhilliardx-claude-ai`. The prose line still names the author. | Before clicking Confirm squash and merge, check that the trailer still reads `Name <email>` with brackets. The web merge box can drop them on paste. |

## 2026-10-25: The second repository

| # | What happened | What we do now |
| --- | --- | --- |
| 20 | The repository was created as `foundations`, while `.github` already linked to `foundation`. Renaming fixed it; GitHub redirects the old name. | Settle a repository name in writing before creating it, and check links that already point to it. |
| 21 | Claude could not push to the new repository until the `agents` team was granted Write on it. Organization settings give the team nothing per repository on their own, and the Add teams dialog can default to Read. | Every new repository needs the `agents` team granted Write, unless the team holds the All-repository write role (see `OPEN.md`). Check the role on the team's row. |
| 22 | Secret scanning, push protection, and private vulnerability reporting were turned on by applying the GitHub recommended security configuration. Sources, all Justin's statements in the Claude session of 2026-10-25: at 16:45 he quoted the setup screen, "These settings will apply to 1 existing repository and all new repositories going forward"; at 16:47, after checking the `.github` security settings page for all three settings, he said "it looks good to me." | Resolves the claim in `.github/SECURITY.md`. New repositories inherit the configuration. |

## 2026-10-27: Issue #2 replaces the founding-brief steps

| # | What happened | What we do now |
| --- | --- | --- |
| 23 | ChatGPT's foundation plan (#2) came from a conversation Justin had with ChatGPT outside the repository. Claude's first review read it as competing with the founding-brief steps in `BACKLOG.md`, because nothing in the repository said the direction had changed. Justin's statement on #2: he had asked for a clean-slate plan, and the existing files were found only when the issue was opened. | A change of direction decided in a conversation is written into the repository (an issue comment or `OPEN.md`) before agents act on it. The founding-brief steps were removed from `BACKLOG.md` in favor of #2; whether the briefs feed the charter is open in `OPEN.md`. |
| 24 | Reconciling #2 took several exchanges on the issue: Claude's review and correction, Justin's direction, ChatGPT's addendum, Claude's reconciliation, ChatGPT's response, and Claude's endorsement. The addendum itself settled in one assessment round by each agent. Each agent stated its own endorsement rather than claiming the other's. | Keep endorsements explicit and per agent. The one-round default in the proposed collaborative resolution rule is not yet in force; this was one observation of it, not proof that one round is enough. |
| 25 | Both agents started M0 within two minutes of each other. By GitHub's timestamps: ChatGPT posted a task claim on #2 at 01:20 UTC; Claude created issues #3 to #6 at 01:21; ChatGPT created duplicates #7 to #9 at 01:21 with the opposite author split; ChatGPT retracted its split on #2 at 01:23 and named #3 to #6 canonical. By each agent's own report: Claude last read #2 at 01:17 and did not re-check before creating issues, and ChatGPT's issue search did not yet show #3 to #6. | Before creating issues or pull requests: post the claim, then re-read the issue's comments and the issue list (not search, which lags) right before writing. If a collision still happens, the earliest existing issue wins and the other agent retracts on the record. **Agent conclusion:** both agents skipped a re-check; neither caused it alone. |
