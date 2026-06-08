# yt-cli

[![License: SSPL](https://img.shields.io/badge/License-SSPL-blue.svg)](https://www.mongodb.com/licensing/server-side-public-license)
[![Dependencies](https://img.shields.io/badge/dependencies-yt--dlp%2C%20fzf%2C%20mpv-orange)](https://github.com/rrvvvr/yt-cli)

A minimal terminal-based YouTube browser built using a Unix pipeline of `yt-dlp`, `fzf`, and `mpv`.

---

## Overview

`yt-cli` is a POSIX shell script that provides a terminal interface for searching and playing YouTube videos. It is designed as a lightweight alternative to the standard YouTube web interface.

The YouTube website requires a browser, JavaScript execution, and renders significant amounts of content unrelated to video playback. `yt-cli` replaces that workflow with a minimal terminal interaction: search, select, and play.

---

## Features

* Search YouTube from the terminal
* Interactive result selection using fuzzy search
* Direct playback via `mpv`
* No browser or graphical interface required

---

## How It Works

`yt-cli` composes three existing command-line tools into a pipeline:

```
yt-dlp  →  fzf  →  mpv
```

1. **`yt-dlp`** retrieves video metadata and stream URLs
2. **`fzf`** presents an interactive, filterable selection interface
3. **`mpv`** handles playback of the selected video

The script coordinates data flow between these tools rather than implementing media functionality directly.

---

## Installation

### Dependencies

The following tools must be installed and available in your `$PATH`:

* [`yt-dlp`](https://github.com/yt-dlp/yt-dlp)
* [`fzf`](https://github.com/junegunn/fzf)
* [`mpv`](https://mpv.io/)

### Setup

```bash
git clone https://github.com/rrvvvr/yt-cli.git
cd yt-cli

mkdir -p ~/.local/bin
cp yt ~/.local/bin/yt
chmod +x ~/.local/bin/yt
```

Ensure `~/.local/bin` is in your `$PATH`:

```bash
export PATH="$HOME/.local/bin:$PATH"
```

---

## Usage

Run from any terminal:

```bash
yt
```

**Workflow:**

1. Enter a search query
2. Navigate results using the keyboard
3. Press `Enter` to play the selected video in `mpv`

---

## Design Decisions

### CLI over Web UI

A terminal-based workflow reduces resource usage and avoids context switching for users already working in a shell environment.

### Unix Pipeline

Each component performs a single task:

* `yt-dlp` for data retrieval
* `fzf` for selection
* `mpv` for playback

This keeps the system modular and leverages well-maintained external tools.

### Scope

`yt-cli` intentionally focuses on search and playback only. It does not attempt to replicate the full YouTube feature set.

---

## Limitations

* No account integration (subscriptions, recommendations, history)
* Depends on external tools (`yt-dlp`, `fzf`, `mpv`)
* May break if upstream tools or YouTube APIs change
* No playlist management or persistent state
* Requires a terminal environment

---

## Non-Goals

* Replacing full-featured media platforms
* Providing a graphical interface
* Supporting account-based or personalized features

---

## License

This project is licensed under the **Server Side Public License (SSPL) v1**. See the `LICENSE` file for details.
