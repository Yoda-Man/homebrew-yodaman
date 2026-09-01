# Yoda-Man Homebrew Tap

Homebrew formulae for [YodaMan](https://github.com/Yoda-Man/yodaman) — local-first
workspace intelligence.

## Install

```bash
brew install Yoda-Man/yodaman/yodaman
```

Or tap first, then install:

```bash
brew tap Yoda-Man/yodaman
brew install yodaman
```

## After installing

YodaMan needs a local model runner and three companion tools. Install them with:

```bash
yodaman setup
```

Ollama is not installed automatically — it is a system service, so `yodaman setup`
prints the command and leaves the decision to you.

## Maintaining this tap

`Formula/yodaman.rb` is generated in the main repository. After publishing a new
version to npm, run there:

```bash
node scripts/brew-formula.js
```

That rewrites the `url` and `sha256` from the published tarball, so neither is
ever typed by hand. Copy the result here. `--check` verifies without writing and
exits non-zero when the formula is out of date.

## Licence

MIT — see the [main repository](https://github.com/Yoda-Man/yodaman/blob/main/LICENSE).
