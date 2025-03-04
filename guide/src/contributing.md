# Contributing

Contributions are welcome, and they are greatly appreciated!

You can contribute in many ways:

## Types of Contributions

### Report Bugs

Report bugs at [https://github.com/PyO3/maturin/issues](https://github.com/PyO3/maturin/issues).

### Fix Bugs

Look through the GitHub issues for bugs. Anything tagged with `bug`
and `help wanted` is open to whoever wants to implement it.

### Implement Features

Look through the GitHub issues for features.

### Write Documentation

Maturin could always use more documentation, whether as part of the official
guide, in docstrings or even on the web in blog posts, articles and such.

### Submit Feedback

The best way to send feedback is to start a new discussion
at [https://github.com/PyO3/maturin/discussions](https://github.com/PyO3/maturin/discussions).

## Get Started!

Ready to contribute? Here's how to setup maturin for local development.

1. Fork the maturin repository on GitHub.
2. Clone your fork locally:
   ```bash
   $ git clone git@github.com:your_name_here/maturin.git
   ```
3. [Install a stable Rust toolchain](https://www.rust-lang.org/tools/install)
   and of course [Python 3.6 or later is also required](https://realpython.com/installing-python/).
4. Create a branch for local development:
   ```bash
   $ cd maturin
   $ git checkout -b branch-name
   ```
   Now you can make your changes locally.
5. When you're done making changes, format your changes with `cargo fmt`, then
   lint with `cargo clippy` and test them with `cargo test`:
   ```bash
   $ cargo fmt
   $ cargo clippy
   $ cargo test
   ```
   Note that in order to run tests you need to install `virtualenv` and
   `cffi` (`pip3 install cffi virtualenv`).
6. Commit your changes and push your branch to GitHub:
   ```bash
   $ git add .
   $ git Commit
   $ git push origin branch-name
   ```
7. Submit a pull request through the [GitHub website](https://github.com/PyO3/maturin/pulls).

We provides a pre-configured [dev container](https://containers.dev/) that could be used in [Github Codespaces](https://github.com/features/codespaces), [VSCode](https://code.visualstudio.com/), [JetBrains](https://www.jetbrains.com/remote-development/gateway/), [JuptyerLab](https://jupyterlab.readthedocs.io/en/stable/).

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/pyo3/maturin?quickstart=1&machine=standardLinux32gb)

## Pull Request Guidelines

Before you submit a pull request, check that it meets these guidelines:

1. The pull request should include tests if it adds or changes functionalities.
2. Add a [changelog](https://github.com/PyO3/maturin/blob/main/Changelog.md)
   entry.
3. When command line interface changes, run `python3 test-crates/update_readme.py` to update related documentation.

## Code

The main part is the maturin library, which is completely documented and should be well integrable. The accompanying `main.rs` takes care username and password for the pypi upload and otherwise calls into the library.

The `sysconfig` folder contains the output of `python -m sysconfig` for different python versions and platform, which is helpful during development.

You need to install `cffi` and `virtualenv` (`pip install cffi virtualenv`) to run the tests.

You can set the `MATURIN_TEST_PYTHON` environment variable to run the tests against a specific Python version, 
for example `MATURIN_TEST_PYTHON=python3.11 cargo test` will run the tests against Python 3.11.

There are some optional hacks that can speed up the tests (over 80s to 17s on my machine).
1. By running `cargo build --release --manifest-path test-crates/cargo-mock/Cargo.toml` you can activate a cargo cache avoiding to rebuild the pyo3 test crates with every python version.
2. Delete `target/test-cache` to clear the cache (e.g. after changing a test crate) or remove `test-crates/cargo-mock/target/release/cargo` to deactivate it.
3. By running the tests with the `faster-tests` feature, binaries are stripped and wheels are only stored and not compressed.
