# Formula Specification

## Purpose
`Formula/yodaman.rb` is the Homebrew formula for YodaMan. It installs the published npm package with Homebrew's Node, links its executables, tells the user how to install the companion tools, and tests the installed CLI. It is a copy of `packaging/homebrew/yodaman.rb` in YodaMan core.

## Requirements

### Requirement: Install from the published npm tarball
The formula SHALL install the `yodaman` package from the npm registry tarball named by its `url`, and MUST verify it against `sha256`. The url SHALL have the form `https://registry.npmjs.org/yodaman/-/yodaman-<version>.tgz`, so Homebrew reads the version from it.

#### Scenario: Install
- **WHEN** the user runs `brew install Yoda-Man/yodaman/yodaman`
- **THEN** Homebrew downloads `https://registry.npmjs.org/yodaman/-/yodaman-0.6.6.tgz` and checks its sha256 `895a858f74fb125a31ce979d90649bc6d625c656cd28eb1a5b164296abbc0e87`

#### Scenario: Tap first
- **WHEN** the user runs `brew tap Yoda-Man/yodaman` and then `brew install yodaman`
- **THEN** the same formula installs

### Requirement: Node dependency and npm install
The formula SHALL depend on Homebrew's `node` and SHALL install with `npm install` and Homebrew's `std_npm_args`, then symlink every file in `libexec/bin` into Homebrew's `bin`.

#### Scenario: Executables linked
- **WHEN** the install finishes
- **THEN** `yodaman` and `yodaman-mcp` are on the user's PATH through Homebrew's `bin`

### Requirement: Companion tools are not installed by the formula
The formula MUST install YodaMan only. Its caveats SHALL tell the user to run `yodaman setup` for the local model runner and three companion tools, and SHALL say that Ollama is not installed automatically because it is a system service.

#### Scenario: Caveats after install
- **WHEN** the install finishes
- **THEN** Homebrew prints that YodaMan needs a local model runner and three companion tools, installed with `yodaman setup`
- **AND** it says `yodaman setup` prints the Ollama command and leaves the decision to the user

### Requirement: Formula test
`brew test yodaman` SHALL run the installed CLI rather than only check files: `yodaman --version` MUST print the formula's version, `yodaman --help` MUST mention `yodaman setup`, and the `yodaman-mcp` executable MUST exist.

#### Scenario: Test passes
- **WHEN** the user runs `brew test yodaman` on a good install
- **THEN** the version output matches the formula version, the help output contains `yodaman setup`, and `bin/yodaman-mcp` exists

#### Scenario: A subcommand that starts the runtime
- **WHEN** `--version` or `--help` would start the runtime instead of exiting
- **THEN** the test hangs instead of passing, which is why both are exercised

### Requirement: Formula metadata
The formula SHALL declare the class `Yodaman`, the description `Local-first workspace intelligence: semantic search, knowledge graph, spec drift`, the homepage `https://github.com/Yoda-Man/yodaman` and the licence `MIT`.

#### Scenario: brew info
- **WHEN** the user runs `brew info yodaman`
- **THEN** it shows that description, homepage and licence
