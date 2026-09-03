# ponytail (Kiro trim)

A trimmed fork of [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail) for
the Kiro IDE on a machine with no extension installs. The upstream ruleset is kept whole;
everything that only serves other harnesses is removed. This repo's `main` is the trimmed
tree; upstream history is retained beneath it.

## What is here

| Path | What it is |
| --- | --- |
| `.kiro/steering/ponytail.md` | the ruleset, loaded every turn (`inclusion: always`) |
| `.kiro/steering/platform-native.md` | the native-vs-dependency reference, loaded on request (`inclusion: manual`) |
| `.kiro/skills/ponytail/` | the canonical skill text; Kiro exposes it as `/ponytail` |
| `.kiro/skills/ponytail-review/` | review a diff for code that should not have been written |
| `.kiro/skills/ponytail-audit/` | the same review over a whole repo |
| `.kiro/skills/ponytail-debt/` | list the `ponytail:` comments left behind as a debt ledger |
| `AGENTS.md` | the ruleset for tools that read only `AGENTS.md` |

## What was removed and why

Adapters for other harnesses (plugin manifests, rules copies, command files), the Node hooks
and MCP server (they re-serve the same skill text that always-on steering already carries),
the `ponytail-gain` and `ponytail-help` skills (they cite removed benchmarks and plugin
paths), benchmarks, tests, examples, assets, and publish scripts.

## Use

Clone this repo, or copy `.kiro/steering/` and `.kiro/skills/` into a project that already
has a `.kiro/` folder. Pairs with the `agent-harness-foundation` repo.

## Updating from upstream

```powershell
git remote add upstream https://github.com/DietrichGebert/ponytail.git
git fetch upstream
git merge upstream/main
```

Resolve conflicts by keeping the deletions in this tree.

## License

MIT, unchanged from upstream. See `LICENSE`.
