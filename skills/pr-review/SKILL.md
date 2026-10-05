---
name: pr-review
description: Review a GitHub pull request with the local code-review workflow, then publish one GitHub approval or changes-requested review. Use only when the user explicitly asks to review and publish a decision.
---

Review a pull request rigorously, then submit exactly one decision for its current head commit.

## Prepare

1. Resolve the PR number or URL and read its metadata, changed files, commits, body, linked issues, existing reviews, and discussion with `gh`.
   Rename the current chat to `PR #<number> review` with the chat-title tool. Continue if the title update is unavailable.
2. Identify its base and head SHAs. Fetch the PR ref if needed, without changing the user's checkout. Compare the merge base with the head using the base branch and PR ref.
3. Read the repository's `AGENTS.md` and applicable local instructions. Follow any requirement-source rules there, including GitHub issues and Jira tickets.
4. Read and apply the local `code-review` skill. Preserve its independent Standards and Spec axes and its requirement for parallel reviewers where delegation is available.

## Decide

Treat every unresolved finding as a concrete, evidence-backed review item with a priority.

- Request changes when there is at least one unresolved P0, P1, or P2 finding.
- Approve only when no P0–P2 findings remain, the requirement context is sufficient to evaluate the change, and relevant verification evidence supports the result. P3 findings may be included as non-blocking follow-ups in an approval.
- When requirements, access, or verification evidence is materially insufficient, publish nothing. Explain the smallest missing item instead.

Before publishing, identify the authenticated GitHub user and inspect submitted reviews. If that user already has a review on the PR's current head commit, do not submit a duplicate; report the existing review and its state instead.

## Publish

Submit one `gh pr review` for the current head only:

- For requested changes, use `--request-changes` with a concise Markdown body. Include each blocking finding's priority, file/line when applicable, issue, impact, requested change, and needed tests.
- For approval, use `--approve` with a concise body that names the comparison, verification performed, and any P3 follow-ups.

Do not publish an approval or changes request for a stale head, and do not use a general PR comment as a substitute for the decision. If the head changes while reviewing, restart from the new head.

## Title the outcome

Update the current chat title after the decision:

- `PR #<number> — Changes requested`
- `PR #<number> — Approved`
- `PR #<number> review — evidence needed` when no review was published

Title updates describe only the current review and are non-blocking if unavailable.

## Finish

Report the published review state and URL, the reviewed head SHA, the decision rationale, and verification performed. If nothing was published, state why. Never implement fixes or merge the PR as part of this skill.
