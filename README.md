# yt-cli

A high-performance, POSIX-compliant terminal utility engineered for zero-latency YouTube streaming. This tool optimizes network handshakes to eliminate IPv6 "Happy Eyeballs" delays and introduces managed pipeline architectures to prevent `BrokenPipeError` runtime failures.

## Features

* **Anti-Lag Network Architecture:** Bypasses standard dual-stack resolution overhead to minimize socket timeout delays.
* **Resilient I/O Pipelines:** Structured stream handling utilizing temporary file handshakes, ensuring immunity to system pipe collapses during media playback.
* **Minimal Footprint:** Native shell execution leveraging robust open-source backends without adding heavy language runtime dependencies.

---

## Dependencies

The utility requires the following CLI tools available in your system path or container environment:

* `yt-dlp` (Core media extraction engine)
* `fzf` (Fuzzy-finding interactive terminal UI)
* `mpv` (High-performance media player backend)

---

## Installation

### 1. Local Deployment
Clone the repository and place the executable script into your local binary directory:

```bash
# Clone the repository
git clone git@github.com:rrvvvr/yt-cli.git
cd yt-cli

# Copy the executable to your local path
cp yt ~/.local/bin/yt

# Ensure execution permissions are set
chmod +x ~/.local/bin/yt
```

### 2. Verification
Ensure your local path is exported in your environment configuration (`.bashrc` or `.zshrc`). Verify the installation by querying the command:

```bash
which yt
```

---

## Usage

Execute the utility directly from your terminal session:

```bash
yt
```

### Operational Workflow:
1. **Search:** Input your search query into the interactive `fzf` prompt.
2. **Select:** Navigate the matching metadata results using the arrow keys or `Ctrl+N` / `Ctrl+P`.
3. **Stream:** Press `Enter` to initiate the hardened, crash-proof pipeline streaming directly into `mpv`.

---

## Licensing

This repository is licensed under the **Server Side Public License (SSPL) v1**. 

### Compliance Requirements
By downloading, optimizing, or deploying this software, you agree to the explicit terms of the SSPL v1. Notably:
* You may use this software locally and modify it freely for personal workflows.
* If you make the functionality of this program or any modified version available to third parties as a service (e.g., hosting a cloud-based terminal-streaming infrastructure), you **must make the Service Source Code available via network download** to everyone, entirely free of charge, under the terms of this license.

For the full legal text, please refer to the accompanying `LICENSE` file in this repository.
