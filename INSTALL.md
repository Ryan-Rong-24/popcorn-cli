# Installation Guide

This fork adds a `--no-tui` flag for plain text output, useful for CI/CD pipelines and scripting.

## Installation Methods

### Method 1: Install Directly from Fork (Easiest)

Install directly from this fork using Cargo:

```bash
cargo install --git https://github.com/Ryan-Rong-24/popcorn-cli.git
```

This will compile and install `popcorn-cli` to your system (typically `~/.cargo/bin/`).

### Method 2: Clone and Build

Clone the repository and build locally:

```bash
# Clone the fork
git clone https://github.com/Ryan-Rong-24/popcorn-cli.git
cd popcorn-cli

# Build the release version
cargo build --release

# Run directly from the build
./target/release/popcorn-cli --help

# Or install to your system
cargo install --path .
```

### Method 3: Add Fork to Existing Clone

If you already have the original repository cloned:

```bash
# Add this fork as a remote
git remote add ryan-fork https://github.com/Ryan-Rong-24/popcorn-cli.git

# Fetch the changes
git fetch ryan-fork

# Check out the fork's main branch
git checkout ryan-fork/main

# Build
cargo build --release
./target/release/popcorn-cli --help
```

### Method 4: Try Without Installing

Test the fork without installing:

```bash
# Clone the fork
git clone https://github.com/Ryan-Rong-24/popcorn-cli.git
cd popcorn-cli

# Run directly with cargo
cargo run -- --help
cargo run -- submit --help
```

### Method 5: Apply Patch to Existing Source

If you have the source code without git, you can apply the patch file:

1. Download the patch file: [`no-tui-feature.patch`](./no-tui-feature.patch)

2. Apply it to your source:
```bash
cd popcorn-cli/
patch -p1 < no-tui-feature.patch
```

3. Rebuild:
```bash
cargo build --release
```

Alternatively, if you have git available:
```bash
git apply no-tui-feature.patch
cargo build --release
```

## Using the New Feature

Once installed, you can use the `--no-tui` flag:

### With TUI (default behavior)
```bash
popcorn-cli submit --gpu A100 --leaderboard my-leaderboard --mode test submission.py
```

### Without TUI (new feature)
```bash
popcorn-cli submit --gpu A100 --leaderboard my-leaderboard --mode test --no-tui submission.py
```

### Save output to file + stream to terminal
```bash
popcorn-cli submit --gpu A100 --leaderboard my-leaderboard --mode test --no-tui submission.py 2>&1 | tee submission.log
```

## Requirements

- Rust toolchain (rustc, cargo)
- For the patch method: `patch` utility (pre-installed on most Unix systems)

## Verifying Installation

Check that the `--no-tui` flag is available:

```bash
popcorn-cli submit --help | grep no-tui
```

You should see:
```
      --no-tui       Skip the TUI and print results directly to stdout
```

## Troubleshooting

### Cargo not found
Install Rust from [rustup.rs](https://rustup.rs/)

### Build errors
Make sure you have the latest stable Rust:
```bash
rustup update stable
```

### Permission denied during installation
You may need to add `~/.cargo/bin` to your PATH:
```bash
echo 'export PATH="$HOME/.cargo/bin:$PATH"' >> ~/.bashrc  # or ~/.zshrc
source ~/.bashrc  # or ~/.zshrc
```

## What's New in This Fork

- **`--no-tui` flag**: Skip the Terminal UI and print results directly to stdout
- **Plain text output**: Better suited for CI/CD pipelines and scripting
- **Progress logging**: Status updates are printed to stderr during submission
- **File output support**: Works seamlessly with the `-o/--output` flag

## Contributing

Found an issue or want to improve this feature? Open an issue or pull request at:
https://github.com/Ryan-Rong-24/popcorn-cli

