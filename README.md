# Prcept AI Homebrew tap

Homebrew formulae for [Brasskey](https://github.com/Prcept-AI/brasskey): run, benchmark and
secure open models on your own hardware.

```bash
brew install prcept-ai/tap/brasskey
brasskey doctor
```

Install by the full name, as above. Homebrew then trusts this formula, and `brew upgrade` keeps
it current. If you ran `brew tap prcept-ai/tap` first, `brew install brasskey` asks you to run
`brew trust --formula prcept-ai/tap/brasskey` before it installs.

Bottles (prebuilt packages) are built here by GitHub Actions for macOS on Apple Silicon and for
Linux (x86_64 and arm64), with build provenance. Other systems build from source, which needs
Rust and takes a few minutes. To check a bottle:

```bash
gh release download brasskey-<version> -R Prcept-AI/homebrew-tap -p '*.bottle.tar.gz'
gh attestation verify brasskey-<version>.arm64_sequoia.bottle.tar.gz --repo Prcept-AI/homebrew-tap
```

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
