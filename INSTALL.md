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

3. Everything in the Brewfile:

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
brew bundle dump --formula --cask --tap --mas --force
```

Keep all four type flags: naming any type drops the rest.

## Traps

- A dump rewrites the whole file from what is installed, so a line removed by
  hand only lasts until the next dump. Uninstall the package instead.
- `brew bundle cleanup` without `--force` only lists what it would remove when
  it is not run in a terminal. In a terminal it asks, and `y` uninstalls
  everything not in the Brewfile, App Store apps included, and resets the tap
  trust store. Run it as `brew bundle cleanup </dev/null`.
- `brew bundle remove <name>` without a type also deletes unrelated lines that
  mention the name, such as `brew "yq" # like "jq"`. Pass `--formula` or
  `--cask`.
- `brew bundle add --install <name>` installs what is already in the Brewfile,
  then adds the entry. It does not install `<name>`, and `add` cannot add App
  Store apps at all.
