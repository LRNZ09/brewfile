# brewfile

The Homebrew formulae, casks and Mac App Store apps this Mac is rebuilt from,
in one [Brewfile](Brewfile). The commands to install it are in
[INSTALL.md](INSTALL.md).

## Why it is not synced automatically

Homebrew has no hook that runs after `brew install` or `brew uninstall`, and
its maintainers have declined to add one. What is left is a `brew` wrapper,
which misses other shells and App Store installs, or a scheduled dump, which
needs its own launchd job. Neither is worth the complexity here, so the
Brewfile is re-dumped by hand with the command in [INSTALL.md](INSTALL.md).
