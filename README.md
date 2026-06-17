# hdiff

A terminal pager for unified diff output — colored, with keyboard navigation between change chunks.

If you've ever piped `helmfile diff`, `git diff --no-color`, or any other unified diff to `less` and found yourself searching for `@@` over and over, this is the fix.

## What it does

`hdiff` reads a unified diff from stdin, colors it, and drops you into an interactive pager:

- `+` lines in green, `-` lines in red, `@@` hunk headers in cyan, file/section headers in yellow
- Contiguous blocks of changes are treated as a single **chunk** — `n`/`N` jumps between them directly, skipping unchanged context
- Mouse wheel scrolling works out of the box
- Terminal state (raw mode, mouse reporting) is always restored on exit, even on Ctrl-C

It's particularly useful for `helmfile diff` output, which mixes Kubernetes YAML changes across many resources in one stream. `n` takes you straight from one changed resource block to the next.

## Usage

```
<any-diff-command> | hdiff
```

Examples:

```bash
helmfile diff | hdiff
git diff | hdiff
kubectl diff -f manifest.yaml | hdiff
```

## Key bindings

| Key | Action |
|---|---|
| `n` | Next chunk |
| `N` | Previous chunk |
| `j` / `↓` | Scroll down one line |
| `k` / `↑` | Scroll up one line |
| `Space` / `Page Down` | Page down |
| `b` / `Page Up` | Page up |
| Mouse wheel | Scroll |
| `q` | Quit |

## Install

Using [bbin](https://github.com/babashka/bbin):

```bash
 bbin install io.github.tkrueger/hdiff
```

## Requirements

- [Babashka](https://babashka.org/) `bb` on your PATH
