# pi-diff-review

This is pure slop, see: https://pi.dev/session/#d4ce533cedbd60040f2622dc3db950e2

It is my hope, that someone takes this idea and makes it gud.

Native diff review window for pi, powered by [Glimpse](https://github.com/hazat/glimpse) and Monaco.

```
pi install git:https://github.com/badlogic/pi-diff-review
```

## What it does

Adds a `/diff-review` command to pi.

The command:

1. opens a native review window
2. lets you switch between `git diff`, `last commit`, and `all files` scopes
3. shows a collapsible sidebar with fuzzy file search
4. shows git status markers in the sidebar for changed files and untracked files
5. lazy-loads file contents on demand as you switch files and scopes
6. lets you draft comments on the original side, modified side, or whole file
7. inserts the resulting feedback prompt into the pi editor when you submit

## Ignored files

Diff Review ignores common lockfiles by default so large generated dependency diffs do not fill the context window:

- `bun.lockb`
- `package-lock.json`
- `pnpm-lock.yaml`
- `poetry.lock`
- `uv.lock`
- `yarn.lock`

Extend the list globally in `~/.pi/agent/settings.json` or per project in `.pi/settings.json`:

```json
{
  "pi-diff-review": {
    "ignoredFiles": [
      "vendor/generated.json",
      "large-fixture.csv"
    ]
  }
}
```

Entries are case-insensitive. Use either a basename (`uv.lock`) or a repository-relative path (`fixtures/huge.json`). Project settings extend global settings; they do not replace the built-in ignores.

## Requirements

- macOS, Linux, or Windows
- Node.js 20+
- `pi` installed
- internet access for the Tailwind and Monaco CDNs used by the review window

### Windows notes

Glimpse now supports Windows. To build the native host during install you need:

- .NET 8 SDK
- Microsoft Edge WebView2 Runtime
