# Prcept AI Homebrew tap

Homebrew formulae for [Brasskey](https://github.com/Prcept-AI/brasskey): run, benchmark and
secure open models on your own hardware.

```bash
brew install prcept-ai/tap/brasskey
brasskey doctor
```

Bottles (prebuilt packages) are built here by GitHub Actions for macOS on Apple Silicon and for
Linux (x86_64 and arm64), with build provenance. Other systems build from source, which needs
Rust and takes a few minutes.

## How the formula is made

`Formula/brasskey.rb` is generated for each Brasskey release by
[`scripts/homebrew_formula.py`](https://github.com/Prcept-AI/brasskey/blob/main/scripts/homebrew_formula.py)
from Brasskey's `uv.lock`: every Python dependency is pinned to the version Brasskey's CI tests,
by URL and SHA-256. Pydantic, cryptography and certifi come from homebrew-core.

To update it: generate the formula for the new version, open a pull request (CI builds and tests
the bottles), then run the `brew pr-pull` workflow with the pull request number to publish the
bottles and merge.

## License

The formulae are Apache-2.0, like Brasskey (see [LICENSE](LICENSE)).
