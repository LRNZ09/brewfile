# brewfile

The Homebrew formulae, casks and Mac App Store apps this Mac is rebuilt from,
in one [Brewfile](Brewfile). The commands to install it are in
[INSTALL.md](INSTALL.md).

Entries for one Mac only, such as work or personal apps, go in `Brewfile.local`
next to it. The Brewfile reads that file when it exists, and git ignores it, so
those entries are never published.

## Why it is not synced automatically

Homebrew has no hook that runs after `brew install` or `brew uninstall`, and
its maintainers have declined to add one. What is left is a `brew` wrapper,
which misses other shells and App Store installs, or a scheduled dump, which
needs its own launchd job. Neither is worth the complexity here, so each change
is recorded by hand with the commands in [INSTALL.md](INSTALL.md).

`brew bundle dump` is not used either. It rewrites the whole file from what is
installed, so every private entry would land in the public one.
