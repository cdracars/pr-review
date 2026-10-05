# PR Review Codex Skill

`pr-review` performs an evidence-based GitHub pull-request review, then publishes one approval or changes-requested decision for the PR's current head.

## Install

In a Codex chat, ask the built-in installer:

> `$skill-installer install the skill from https://github.com/cdracars/pr-review/tree/main/skills/pr-review`

The skill is explicit-only. Invoke it with `$pr-review` and a pull-request URL or number.

`pr-review` uses the local `$code-review` workflow when it is available. Install or otherwise make that skill available for its full two-axis Standards and Spec review.

For a manual installation, copy `skills/pr-review/` into `~/.codex/skills/pr-review/`.

## Decision boundary

The skill requests changes for unresolved P0–P2 findings. It approves only when requirements and verification evidence are sufficient and no P0–P2 findings remain. It avoids duplicate reviews for the same authenticated reviewer and PR head.

## License

This project is licensed under the [MIT License](LICENSE).
