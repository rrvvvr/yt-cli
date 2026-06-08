# yt-cli

[![License: SSPL](https://img.shields.io/badge/License-SSPL-blue.svg)](https://www.mongodb.com/licensing/server-side-public-license)
[![Dependencies](https://img.shields.io/badge/dependencies-yt--dlp%2C%20fzf%2C%20mpv-orange)](https://github.com/rrvvvr/yt-cli)

## Overview

`yt-cli` is a POSIX shell script that provides a terminal interface for searching and playing YouTube videos. It is intended as a lightweight alternative to using the YouTube website directly.

The YouTube web interface requires a browser, JavaScript execution, and renders significant amounts of page content unrelated to video playback. `yt-cli` replaces that interaction with a minimal terminal workflow: search, select, and play.

---

## Features

- Search YouTube from the terminal
- Browse results interactively using fuzzy search
- Play selected videos directly via `mpv`
- No browser or web UI required

---

## How It Works

`yt-cli` connects three existing command-line tools in a Unix pipeline:

```
yt-dlp  -->  fzf  -->  mpv
```

1. **`yt-dlp`** queries YouTube and returns video metadata (titles, URLs, and related identifiers).
2. **`fzf`** receives that metadata and displays it as an interactive, filterable list in the terminal.
3. **`mpv`** receives the selected video URL and handles playback.

The script itself contains no media logic. It coordinates input and output between these three tools.

---

## Installation

### Dependencies

The following tools must be installed and available in your `$PATH`:

- [`yt-dlp`](https://github.com/yt-dlp/yt-dlp) — fetches video metadata and stream URLs
- [`fzf`](https://github.com/junegunn/fzf) — interactive terminal selection
- [`mpv`](https://mpv.io/) — video playback

### Setup

```bash
git clone https://github.com/rrvvvr/yt-cli.git
cd yt-cli

mkdir -p ~/.local/bin
cp yt ~/.local/bin/yt
chmod +x ~/.local/bin/yt
```

Ensure `~/.local/bin` is in your `$PATH`. Add the following to your `.bashrc` or `.zshrc` if it is not already present:

```bash
export PATH="$HOME/.local/bin:$PATH"
```

---

## Usage

Run the script from any terminal:

```bash
yt
```

**Workflow:**

1. Type a search query at the prompt.
2. Use the arrow keys or `Ctrl+N` / `Ctrl+P` to move through results.
3. Press `Enter` to play the selected video in `mpv`.

---

## Design Decisions

### CLI over web UI

A shell script has a smaller resource footprint than a browser-based interface. For users who spend most of their time in the terminal, a CLI workflow avoids switching contexts to a browser.

### Unix pipeline

Rather than implementing search or playback directly, `yt-cli` delegates each task to a dedicated tool. This keeps the script short, makes each component independently replaceable, and relies on tools that are already well-tested and maintained upstream.

### Scope

`yt-cli` is intentionally narrow in scope. It handles search and playback only. Features such as account integration, playlist management, and download management are outside the current scope.

---

## Limitations

- **No account integration:** The tool does not support YouTube login. Personalized recommendations, subscriptions, and watch history are not available.
- **External dependencies:** The tool depends on `yt-dlp`, `fzf`, and `mpv`. If any of these are unavailable or change in a breaking way, the script will stop working.
- **Platform breakage:** YouTube periodically changes its internal structure. When this happens, `yt-dlp` may stop returning results until it is updated. Run `yt-dlp -U` to update it.
- **Codec and hardware support:** Playback quality and format support depend on the `mpv` build and the host system's available hardware acceleration.
- **Terminal environment required:** This tool has no graphical interface and requires a terminal emulator to run.

---

## License

This project is licensed under the **Server Side Public License (SSPL) v1**. See the `LICENSE` file for the full license text.
