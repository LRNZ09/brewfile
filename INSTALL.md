# Install

On a blank Mac, in order.

1. [Homebrew](https://brew.sh). It also installs the Xcode Command Line Tools,
   which provide `git`. Follow the "Next steps" it prints to put `brew` on
   `PATH`:

   ```sh
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

2. Sign in to the App Store. `mas` cannot sign in for you, and it cannot buy an
   app this Apple ID does not already own.

3. Everything in the Brewfile. On a Mac with entries of its own, write them to
   `Brewfile.local` in the clone before installing. It is not in git, so
   nothing restores it:

   ```sh
   git clone https://github.com/LRNZ09/brewfile.git
   cd brewfile
   brew bundle install
   ```

## Updating the Brewfile

From the repo root. `lefthook install` is needed once per clone, so gitleaks
scans each commit as well as every push:

```sh
lefthook install
```

Record each install or uninstall as it happens. Add `--file=Brewfile.local` to
any of these to keep the entry off GitHub:

```sh
brew bundle add <formula>
brew bundle add --cask <cask>
brew bundle remove --formula <formula>
brew bundle remove --cask <cask>
```

App Store apps have no `add`: write the `mas "<name>", id: <id>` line by hand,
with the id from `mas list`. `brew bundle remove --mas "<name>"` does work.

To find what was missed:

```sh
brew bundle cleanup </dev/null   # installed, but in neither file
brew bundle check --verbose      # in a file, but missing or outdated
```

## Traps

- Do not run `brew bundle dump --force` here. It rewrites the whole file from
  what is installed, which publishes every entry in `Brewfile.local` and drops
  the lines that read it.
- `brew bundle add` appends to the end of the file, not in order. Move the line
  by hand to keep the file sorted.
- A private entry from its own tap needs that `tap` line in `Brewfile.local`
  too, or the tap is still published.
- `brew bundle cleanup` without `--force` only lists what it would remove when
  it is not run in a terminal. In a terminal it asks, and `y` uninstalls
  everything not in the Brewfile, App Store apps included, and resets the tap
  trust store. Run it as `brew bundle cleanup </dev/null`.
- `brew bundle remove <name>` without a type also deletes unrelated lines that
  mention the name, such as `brew "yq" # like "jq"`. Pass `--formula` or
  `--cask`.
- `brew bundle add --install <name>` installs what is already in the Brewfile,
  then adds the entry. It does not install `<name>`.
