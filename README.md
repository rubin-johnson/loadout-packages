# loadout-packages

A [kanon](https://github.com/nicholasgasior/kanon) manifest repository for distributing [loadout](https://github.com/rubin-johnson/loadout) packages — versioned Claude Code configuration bundles.

## Available packages

| Package | Description |
|---------|-------------|
| `token-miser` | Minimize token usage — terse output, lazy file reading, no extras |
| `thorough` | Maximize correctness — read everything, explain reasoning, verify |
| `tdd-strict` | Strict TDD — write failing test first, then make it pass |

## Consuming packages

Add a `.kanon` file to your project:

```
GITBASE=https://github.com/rubin-johnson/
KANON_SOURCE_packages_URL=https://github.com/rubin-johnson/loadout-packages.git
KANON_SOURCE_packages_REVISION=refs/tags/0.1.0
KANON_SOURCE_packages_PATH=repo-specs/meta.xml
```

Then run:

```
kanon install
```

Packages appear in `.packages/` as synced directories. Reference them with loadout:

```
loadout apply .packages/token-miser
```

## Adding a package

1. Create a directory with `manifest.yaml` and `CLAUDE.md`
2. Add a `<project>` entry in `repo-specs/packages.xml`
3. Tag a new release

## How it fits together

- **kanon** distributes versioned packages from this manifest repo
- **loadout** applies packages (injects CLAUDE.md rules into a project)
- **token_miser** measures the cost impact of different configurations

The pipeline: kanon distributes -> loadout applies -> token_miser measures.
