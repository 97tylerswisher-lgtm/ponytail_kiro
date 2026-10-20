# ponytail (Kiro trim)

A trimmed fork of [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail) for
the Kiro IDE on a machine with no extension installs. The upstream ruleset is kept whole;
everything that only serves other harnesses is removed. This repo's `main` is the trimmed
tree; upstream history is retained beneath it. The rule text tracks upstream v5.3.2 (updated
2026-10-19).

## What is here

| Path | What it is |
| --- | --- |
| `.kiro/steering/ponytail.md` | the ruleset, loaded every turn (`inclusion: always`) |
| `.kiro/steering/platform-native.md` | the native-vs-dependency reference, loaded on request (`inclusion: manual`) |
| `.kiro/skills/ponytail/` | the canonical skill text; Kiro exposes it as `/ponytail` |
| `.kiro/skills/ponytail-review/` | review a change for bugs, safety, real load, missing tests, speed and needless code; reads the code the change touches, not only the diff |
| `.kiro/skills/ponytail-audit/` | the same checks over a whole repo, ranked, with what to fix first |
| `.kiro/skills/ponytail-debt/` | list the `shortcut:` comments (and older `ponytail:` ones) left behind as a debt ledger |
| `AGENTS.md` | the ruleset for tools that read only `AGENTS.md` |

## What was removed and why

Adapters for other harnesses (plugin manifests, rules copies, command files), the Node hooks
and MCP server (they re-serve the same skill text that always-on steering already carries),
the `ponytail-gain` and `ponytail-help` skills (they cite removed benchmarks and plugin
paths), the v5 band, board and SessionStart codebase map (Claude Code hooks and mods; Kiro has
neither), benchmarks, tests, examples, assets, and publish scripts.

## Use

Clone this repo, or copy `.kiro/steering/` and `.kiro/skills/` into a project that already
has a `.kiro/` folder. Pairs with the `agent-harness-foundation` repo.

## Updating from upstream

The kept files are verbatim upstream copies, so an update is a copy, not a merge (a merge
conflicts on every deleted file). Upstream keeps the skills under `skills/`; this tree keeps them
under `.kiro/skills/`.

```powershell
git remote add upstream https://github.com/DietrichGebert/ponytail.git
git fetch upstream
cmd /c "git show upstream/main:.kiro/steering/ponytail.md > .kiro\steering\ponytail.md"
cmd /c "git show upstream/main:AGENTS.md > AGENTS.md"
foreach ($s in 'ponytail','ponytail-review','ponytail-audit','ponytail-debt') {
  cmd /c "git show upstream/main:skills/$s/SKILL.md > .kiro\skills\$s\SKILL.md"
}
```

The `cmd /c` redirect writes the bytes as git gives them. PowerShell 5.1 `Set-Content` and `>` add a
byte-order mark, which can hide the `---` front matter from Kiro. Then check the new text for links to removed files (`ponytail-help`, `ponytail-gain`, hooks,
benchmarks). `platform-native.md` is this tree's own file and is not in upstream.

## License

MIT, unchanged from upstream. See `LICENSE`.
