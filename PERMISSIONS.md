# Agent identity, authority, and GitHub enforcement

**Version:** 0.1 (Proposed)  
**Task:** [FND-04, Issue #6](https://github.com/applied-unknowns/foundation/issues/6)  
**Source:** [Foundation proposal #2](https://github.com/applied-unknowns/foundation/issues/2); [charter](CHARTER.md)  
**Drafter:** ChatGPT (`jhilliardx-chatgpt-ai`)  
**Status:** Proposed analysis and verification plan. This document does not confer permissions, change existing Set rules, or attest that untested controls work.

## 1. Purpose, scope, and evidence vocabulary

The objective is to make authority **inspectable and testable**, especially the difference between a policy that people agree to honor and a technical control that GitHub actually enforces. Owner approval is required for any live permission or settings change; none is performed here.

Use three distinct evidence types:

- **Set policy:** Owner-established instruction in [organization `AGENTS.md`](https://github.com/applied-unknowns/.github/blob/main/AGENTS.md) or [`GOVERNANCE.md`](https://github.com/applied-unknowns/.github/blob/main/GOVERNANCE.md). This is binding on agents, but a sentence alone is not a platform restriction.
- **Configured control:** A reported or observed GitHub setting, tied to a repository, effective ruleset and readback date. Do not infer it from a feature's availability.
- **Verified behavior:** A readback or controlled test that actually demonstrates a property in the specified configuration. A read-only permission response does not establish what every write would do.

**Evidence tags used below:** **[S]** Set repository or organization rule; **[O]** direct read-only observation by ChatGPT on 2026-10-27; **[L]** report preserved in [`LESSONS.md`](LESSONS.md) or [`OPEN.md`](OPEN.md), not independently tested here; **[D]** published GitHub documentation; **[P]** proposed control or test.

The scope is the public `applied-unknowns/foundation` repository and the organization-wide rules it inherits by instruction. Other repositories may have different settings. Differences in application programming interface (API) access between a model's hosted environments are runtime-specific facts, not properties of the underlying model.

## 2. Identified principals

| Principal | Foundation permission as observed [O] | Set duties and limits [S] | Evidence and qualification |
| --- | --- | --- | --- |
| `jhilliardx` | `admin` | Human founder, final approver, only permitted merger and ruleset approver; agent work must not use this identity. | GitHub collaborator-permission readback [O]. Organization rules 1–3. |
| `jhilliardx-chatgpt-ai` | `write` | Agent author and independent reviewer of Claude work, using own account and `chatgpt/` branches. Must not merge or exercise bypass, even where technically possible. | GitHub collaborator-permission readback [O]. [Issue #2 owner decision](https://github.com/applied-unknowns/foundation/issues/2). |
| `jhilliardx-claude-ai` | `write` | Agent author and independent reviewer of ChatGPT work, using own account and `claude/` branches. Must not merge or exercise bypass. | GitHub collaborator-permission readback [O]. Issue #2. |
| Outside human contributor | Not established; varies by repository role and organization settings | May propose; has no implied right to alter approved requirements or merge. | No per-person permission readback. Public visibility is not the same as write authority. [GitHub roles documentation](https://docs.github.com/en/organizations/managing-user-access-to-your-organizations-repositories/managing-repository-roles/repository-roles-for-an-organization) [D]. |
| Future API-operated agent | No current identity/installation assumed | Requires a separate narrowly scoped GitHub App or equivalent and independent owner approval before operation. | `OPEN.md` defers per-vendor apps. No technical enforcement claim. |

**Important separation:** Distinct GitHub account names show who submitted a review. They do **not** by themselves prove which model actually generated the analysis or that separate humans controlled the accounts. Independence is established by identity **and** review-process evidence, not user names alone.

## 3. Action and authority matrix

The table states **permitted policy**, **technical reality**, and **verification** separately.

| Action | Owner `jhilliardx` | Agents (each own identity) | Outside contributor | Actual GitHub boundary / gap |
| --- | --- | --- | --- | --- |
| Read the public repository and governed instructions | Permitted | Permitted, required before work | Public read, where available | Public read is not authority to change anything [D]. |
| Open an issue or propose an architectural change | Permitted | Permitted in own identity | Subject to repository access/settings | An issue or comment is not an approved change [S]. |
| Push an authorized feature branch | Permitted | Permitted for bounded, claimed work | Only with Write or permitted fork workflow | Agents have Write [O]; feature-branch permission does not authorize `main`. |
| Open a pull request (PR) | Permitted | Permitted; one purpose, target and assumptions, template | Depending on repository permissions | GitHub can host PR records; authored proposals are not accepted results [S]. |
| Independently review another author's PR | Permitted | Required as first cross-model review in Issue #2 | May comment; whether a review can satisfy required approval depends on Write or higher [D] | Review attribution must show a distinct reviewer; author never self-certifies [S]. |
| Approve work conceptually / ratify governing scope | Sole final decision | Recommend and challenge only | Recommend only | A GitHub approval event by an agent is **technical review**, not owner authorization [S]. |
| Merge a PR into the protected default branch | **Sole permitted merger** | **Prohibited by Set policy** | No authorization given | **GAP-01:** GitHub's standard Write role generally permits merge when repository protection requirements are met [D]. A one-review ruleset does not, by itself, restrict successful merges to Justin. No owner-only merge technical enforcement has been verified. |
| Bypass required reviews or branch rules | Owner only where explicitly configured and authorized | Prohibited | No bypass authority | Existing admin PR-only bypass is reported in `LESSONS.md` row 3 [L]. Agent exclusion from bypass has not been independently re-read here. |
| Modify organization instructions, `CODEOWNERS`, or workflow | Owner's explicit review required | Can propose through permitted PR only | No implicit right | Organization rule 13 [S]. Effective code-owner approvals remain an open settings item [L]. |
| Change org membership, roles, rulesets, security settings, or credentials | Owner authorization and proper platform privilege | Not authorized | Not authorized | GitHub Admin differs from Write [D]. Accessible connector features must not be mistaken for delegated authority. |
| Deploy or use privileged automation | Explicit owner approval for each operation | No standing authorization | None | Organization `GOVERNANCE.md` permission ladder [S]. No trusted automated production execution is established. |
| Promote research content from personal repositories | Accept through governed PR only | May propose and screen within approved scope | No implied authority | Deferred to FND-03; provenance links themselves may be sensitive. Do not infer that a private repository makes excluded content acceptable. |

### GAP-01: Human-only merging is a policy, not a proven platform invariant

[GitHub repository roles](https://docs.github.com/en/organizations/managing-user-access-to-your-organizations-repositories/managing-repository-roles/repository-roles-for-an-organization) say Write can ordinarily merge a pull request. Both agents have Write [O]. Their Set prohibition on merging is therefore **currently a behavioral boundary**, not shown to be a technical restriction on those accounts.

A branch rule requiring an independent approval blocks some unsafe paths, but could still allow agent B's approval followed by agent A's merge. Requiring an approval from `jhilliardx` as code owner may enforce human *approval* if configured correctly; it must not be claimed to enforce human-only *execution of merge* without a separate verified restriction. GitHub's [ruleset documentation](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/available-rules-for-rulesets) distinguishes these protections.

**Proposed owner decision [P]:** Before unattended agent execution, define and verify a restriction that prevents agent credentials from performing a merge, not merely a written instruction. One **unverified candidate** for isolated test V-04 is a GitHub ruleset **Restrict updates** rule scoped to Justin as the only bypass actor. GitHub documents the rule's push restriction but does not establish here whether it also prevents a Write user from merging a pull request. It is not an accepted fix. Candidate controls must be tested with the actual roles, effective rulesets, and current account/plan capability. Do not remove agent Write access, change a ruleset, or grant an App without the owner's explicit approval.

## 4. Recorded controls and verification gaps

| ID | Control / observation | State and confidence | Verification still required |
| --- | --- | --- | --- |
| C-01 | `foundation` role readback: owner Admin; each named agent Write. | **Observed** with connected GitHub permission read action on 2026-10-27 [O]. | Repeat after membership change; record timestamp and role per account. |
| C-02 | Organization-wide default-branch PR ruleset: one required approval, squash-only merges, linear history, and a requirement for approval from someone other than the last pusher. The reported admin PR-only bypass is **not included** in the effective-rules endpoint. | **Claude-observed** on 2026-10-27 in FND-03 [PR #13](https://github.com/applied-unknowns/foundation/pull/13), `BOUNDARIES.md` readback [L]. The reported settings include `require_last_push_approval: true`, `dismiss_stale_reviews_on_push: false`, and `require_code_owner_review: false`; independently unverified in this runtime. | Re-read applicable rules and separately verify bypass actors and actual enforcement. Save a source-linked, sanitized JavaScript Object Notation (JSON) readback. The current connector did not provide the effective-rules endpoint. |
| C-03 | `main` protected against direct agent pushes and unapproved merges. | **Reported** by existing merged PR workflow and governance ledger [L]; not proven for every actor. | Verify in an owner-authorized disposable test repository with equivalent rules, without unsafe direct writes to canonical `main`. |
| C-04 | Stale-review dismissal is off, last-pusher approval is required, and code-owner review is off in Claude's effective readback. | **Claude-observed** in PR #13 [L]; independent behavior not established. `OPEN.md` still requests changes. | Determine whether the last-pusher requirement already guards against an older approval remaining effective after a new push, using V-06, before selecting another setting. |
| C-05 | No `CODEOWNERS` file was found at `.github/CODEOWNERS`, root `CODEOWNERS`, or `docs/CODEOWNERS` **within the foundation repository**. The file merged in the distinct `.github` repository's PR #1 governs **that repository only**; it does not protect `foundation/AGENTS.md`. | **Observed** file lookups on 2026-10-27 [O]; per-repository placement confirmed by [GitHub code-owner documentation](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners) [D]. | Verify after settings changes. `OPEN.md` saying code-owner enforcement "can now" be enabled applies to the separate `.github` repository, **not foundation**; coordinate a later correction to `OPEN.md` after Claude's PR #13 (which edits that file) merges. |
| C-06 | Secret scanning, push protection, and private vulnerability reporting enabled via an organization configuration. | **Justin-reported** in `LESSONS.md` row 22 [L]; cannot be independently certified by this GitHub connection. | Owner-side settings readback for each repository; compare security configuration applicability and bypass authority. |
| C-07 | Default push protection may allow a writer to bypass a block by giving a reason. | **Documented GitHub behavior**, not verified in this organization [D]. | Owner checks delegated bypass / exemptions, especially for both agent accounts. Never test with live credentials or real sensitive material. |
| C-08 | Agents are different accounts and gave one another first review of FND-01 and FND-02. | **Observed** in PRs [#10](https://github.com/applied-unknowns/foundation/pull/10) and [#11](https://github.com/applied-unknowns/foundation/pull/11) [O]. | Independently check each accepted review applies to the final changed commit; investigate stale approvals if new changes were pushed. |
| C-09 | Authored Git commit attribution can accidentally use a personal email even under an agent account. | **Observed** during [PR #11](https://github.com/applied-unknowns/foundation/pull/11) and corrected in its current history [O]. | Check author and committer identity against the approved `users.noreply.github.com` identity before requesting review; do not assume the runtime keeps that setting. |
| C-10 | Some hosted runtimes have tool limitations, including inaccessible dot-named repositories, REST-only access, or per-repository connector attachment. | **Claude-reported** runtime observations and `LESSONS.md` rows 5–6 [L], **not universal model limits**. | Probe every actual provider/runtime capability read-only before delegating tasks; record failure modes. |
| C-11 | A reviewer can request changes and independently approve once the corrected version passes. | **Observed** in PRs #10 and #11 [O]. | Check that reviewer independence and latest-commit coverage survive history rewrites or follow-up changes. |

**Code ownership reference:** [GitHub: About code owners](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners). A `CODEOWNERS` file must exist in the **same repository** in an accepted location and on the base branch; enabling required code-owner reviews is a separate protection setting.

**Secret protection reference:** [GitHub: Push protection](https://docs.github.com/en/code-security/concepts/secret-security/push-protection), [Delegated bypass](https://docs.github.com/en/code-security/how-tos/secure-your-secrets/manage-bypass-requests/enable-delegated-bypass). Detection is not exhaustive and bypass may be possible. Neither secret scanning nor an agent's checkbox substitutes for source review.

## 5. Safe validation program: proposed, not executed

Each test has a reproducible input, expected result and required evidence. Tests that could change actual permissions or canonical state are **blocked pending owner authorization and an isolated test repository**.

| Test | Method | Expected evidence / pass | Stop condition |
| --- | --- | --- | --- |
| V-01: Role inventory | Read collaborator permissions for the three declared accounts through approved read-only API. | Timestamped readback; roles mapped to current `AGENTS.md` Identities. | Missing permission to read is **unknown**, not presumed No. |
| V-02: Effective branch controls | Read rulesets applicable to the exact default branch for the repository. | Sanitized effective JavaScript Object Notation (JSON) with required PR/reviews, bypass actors, push/force/delete limits and merge types, tied to repository/ref/time. | Inaccessible settings stop enforcement claims. |
| V-03: No unauthorized direct push | **Only with owner approval**, configure a disposable repository with equivalent rules; attempt harmless direct update using each agent's limited test identity. | Denial plus audit/Hypertext Transfer Protocol (HTTP) outcome under defined permissions. | Never probe `main` or alter real rules as part of this proposal. |
| V-04: Owner-only merge enforcement | In disposable repo, give two test accounts equivalent Write and approvals, then test whether one account can technically merge after the other approves. | Definitive allow/deny result, documented effective ruleset. A positive result means policy-only boundary persists. | Do not perform unauthorized merges on `foundation`. |
| V-05: Independent review | On a test PR, verify same author cannot satisfy its own review and that another model/account's review is separately recorded. | Review identifier, account identifiers, final commit Secure Hash Algorithm (SHA) value, timing. | Do not conflate identity distinctness with model provenance proof. |
| V-06: Stale review and code ownership | In an owner-approved disposable test repository, compare approval behavior after a new push under `require_last_push_approval: true` with `dismiss_stale_reviews_on_push: false`; separately verify local `CODEOWNERS` and code-owner requirements. | Document whether a review granted **before** the latest push can satisfy the gate, along with explicit blocked/unblocked results and effective settings. | No premature `foundation` changes, no live settings modification, and no reviewer bypass. |
| V-07: Secret/provenance containment | Offline tests using benign synthetic strings and mock paths; inspect outputs for copying confidential source identifiers or treating instructions as commands. | No genuine secrets, no sensitive public provenance or unreviewed policy changes. | Never introduce real credentials, personal records, or employer data as fixtures. |
| V-08: Runtime/identity continuity | Start a clean authorized agent session; load Git state; compare account, permitted actions, model provider, and approval record with expected. | Versioned report including disagreements and unknowns; do not infer unseen settings. | Any identity mismatch or missing authorization stops writes. |

Record **PASS / FAIL / UNVERIFIED / NOT APPLICABLE** per test; include date, repository, revision, ruleset snapshot reference, account, tool/runtime, reviewer, and possible impact. A paper plan is not a passed test.

## 6. Risk and escalation register

| Risk | Severity (agent assessment) | Why material | Owner decision or later implementation |
| --- | --- | --- | --- |
| R-01 Agent has technical merge capability despite owner-only Set rule | **High, unverified exploitability in current configuration** | Write role can ordinarily merge once branch protections are satisfied; two agents could satisfy one another's required reviews. | Validate controls and select human-only merge enforcement before unattended runs (GAP-01). |
| R-02 Required code-owner approval not operational in `foundation` | High for future autonomous changes | No repository-local `CODEOWNERS` found; owner review requirement is currently off in Claude's reported effective readback for `foundation`. The `.github` repository's code owners do not transfer here. | Owner selects owners and authorized ruleset change with readback. |
| R-03 An older approval might remain effective after a new push | Medium, behavior unverified | Stale-review dismissal is off, but Claude's readback confirms **last-pusher approval is required**, which may mitigate the risk. GitHub documentation does not settle from this evidence whether an approval submitted before a later push remains effective. | Run V-06 before claiming the risk exists or selecting additional protection. |
| R-04 Secret push-protection bypass by Write accounts | High if misconfigured | Detects only covered secret types; default bypass can be invoked by Write users. | Owner inspect delegated bypass, writer privileges, alerts, and approved exceptions. |
| R-05 Agent runtime/source attribution mismatch | Medium | Session, connector, or user-account attribution may conceal the actual model drafter or leak inappropriate email metadata. | Verify identity on each commit/PR; move toward limited vendor GitHub Apps only after approved research. |
| R-06 Untrusted content or external Git history carried into public org | High if exposed | Review processes cannot undo all public disclosure after pushing. | Integrate FND-03's content/provenance screening; future security controls must be independently tested. |

These severities are **agent conclusions**, not owner-ratified organizational risk tolerances.

## 7. Minimal configuration trajectory (not authorization)

1. **Keep now:** Distinct agent identities, human-only approval **by policy**, reviewed PRs, explicit source records, and currently effective protections. Do not weaken or bypass protections to make work easier.
2. **Read before mutate:** Owner verifies current effective rulesets, collaborator roles, code-owner settings, and push-protection bypass conditions. Save sanitized evidence in a reviewed change.
3. **Decide enforcement:** Compare approaches to preventing agent merges and unauthorized branch updates under the actual plan/account constraints. Never assert that code-owner approval is equivalent to restricting the merge actor.
4. **Test in isolation:** Prove negative paths using disposable resources and no real sensitive data. Record both actual denials and unexpected permissions.
5. **Promote only after verified:** Owner approves a narrowly scoped settings change, an independent reviewer confirms findings, and an exact readback demonstrates the resulting control. Preserve a rollback procedure.
6. **Later:** Replace interim user-account credentials with separate scoped provider-operated integrations only after a complete permission threat assessment and a model-independent dispatcher design; see deferred [discovery #12](https://github.com/applied-unknowns/foundation/issues/12).

**No current permissions, rulesets, organization settings, tokens, continuous integration (CI), or deployment systems are modified by FND-04.**

## 8. Acceptance and open decisions

FND-04 can be reviewed as a **permission-model proposal** when every role is labeled as a Set rule, observed permission, documented capability, or unknown; the validation matrix is reproducible; and major technical-policy divergences are visible. It is not evidence that unattended autonomy is safe.

**Owner actions for later, not assumed:** Choose technical merge enforcement for agent Write accounts, decide code owner protection and stale-review handling, examine secret-protection bypass scope, and approve any isolated negative-test environment. Such decisions belong in the canonical [`OPEN.md`](OPEN.md) through a separately scoped reviewed PR; this FND-04 branch does not edit it.

**Review:** Claude, as first independent reviewer; Justin, as final approver/merger. A nonblocking disagreement may be preserved; material unverified privilege assumptions cannot be silently dismissed.

**Primary references:**
- [GitHub repository roles](https://docs.github.com/en/organizations/managing-user-access-to-your-organizations-repositories/managing-repository-roles/repository-roles-for-an-organization)
- [GitHub available ruleset rules](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/available-rules-for-rulesets)
- [GitHub ruleset bypass and restrictions](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/creating-rulesets-for-a-repository)
- [GitHub code owners](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners)
- [GitHub push protection](https://docs.github.com/en/code-security/concepts/secret-security/push-protection)
- [FND-01 charter](CHARTER.md); [organization instructions](https://github.com/applied-unknowns/.github/blob/main/AGENTS.md); [organization governance](https://github.com/applied-unknowns/.github/blob/main/GOVERNANCE.md).
