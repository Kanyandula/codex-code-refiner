# Codex Code Refiner

A Codex skill that reviews recently changed code and applies clear, behavior-preserving refinement fixes.

It uses four review lenses: reuse existing helpers, simplify control flow, remove material inefficiencies, and check that abstractions are at the right level. It edits the code when an improvement is clear and reports uncertain opportunities instead of guessing. This is a focused cleanup pass, not a general correctness or security review.

The workflow is inspired by the documented cleanup behavior of Claude Code's `/simplify` skill. This project is independent and is not affiliated with or endorsed by Anthropic.

## Install with Codex

Install the skill from this public repository with Codex's skill installer:

```text
$skill-installer Install the skill at skills/code-refiner from Kanyandula/codex-code-refiner
```

Or run the bundled installer helper:

```sh
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo Kanyandula/codex-code-refiner \
  --path skills/code-refiner
```

Start a fresh Codex session after installation. Invoke the skill in the CLI with:

```text
$code-refiner
```

You can add a target or focus, for example: `$code-refiner Focus on simplifying the retry logic in src/client.ts`.

## Manual install

Clone the repository and copy the skill folder into Codex's user skills directory:

```sh
git clone https://github.com/Kanyandula/codex-code-refiner.git
mkdir -p ~/.codex/skills
cp -R codex-code-refiner/skills/code-refiner ~/.codex/skills/
```

## Contents

- `skills/code-refiner/SKILL.md` — skill instructions
- `skills/code-refiner/agents/openai.yaml` — Codex display metadata and invocation prompt

## License

MIT. See [LICENSE](LICENSE).
