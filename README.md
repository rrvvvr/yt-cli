# yt-cli

A minimalist, pipeline-driven terminal utility for searching and streaming YouTube media.

[![License: SSPL](https://img.shields.io/badge/License-SSPL-blue.svg)](https://www.mongodb.com/licensing/server-side-public-license)
[![Dependencies](https://img.shields.io/badge/dependencies-yt--dlp%2C%20fzf%2C%20mpv-orange)](https://github.com/rrvvvr/yt-cli)

## Overview

`yt-cli` is a lightweight POSIX-compliant shell utility designed to provide a high-performance interface for browsing and consuming video content.

Traditional web interfaces introduce significant computational overhead, DOM rendering lag, and tracking telemetry. This project addresses those inefficiencies by leveraging native terminal data-streams to interface with web-hosted media, adhering strictly to the Unix philosophy of tool composition.

## Key Features

- **Interactive Search Filtering:** Real-time metadata parsing and fuzzy listing directly inside the terminal buffer.
- **Zero-Bloat Playback:** Decoupled media decoding via the `mpv` hardware-accelerated rendering engine.
- **Network Optimization:** Hardened socket and handshake configuration to minimize DNS resolution delays and Happy Eyeballs (IPv4/IPv6) connection timeouts.
- **Managed Stream Pipes:** Robust I/O handling designed to manage terminal signals gracefully and prevent execution crashes from downstream pipeline breaks.

---

## Technical Architecture

The architecture relies on standard Unix streams (`stdout`, `stdin`) to link three single-purpose utilities into a unified data processing pipeline:

```
User Query --> yt-dlp (Metadata) --> fzf (Video URL) --> mpv
```

1. **Ingestion & Extraction (`yt-dlp`):** Queries remote architectures to retrieve video identifiers and raw text metadata.
2. **Interactive Selection (`fzf`):** Captures the metadata stream, formatting it dynamically into a fuzzy-matching CLI menu.
3. **Stream Playback (`mpv`):** Resolves the target network URL and streams direct codecs to a decoupled rendering window.

---

## Installation

### Prerequisites

Ensure the following packages are installed and available in your `$PATH`:

- [`yt-dlp`](https://github.com/yt-dlp/yt-dlp) — Stream extraction engine
- [`fzf`](https://github.com/junegunn/fzf) — Fuzzy-finding interface
- [`mpv`](https://mpv.io/) — Media player backend

### Setup

Clone the repository and install the binary to your local environment:

```bash
# Clone via HTTPS
git clone https://github.com/rrvvvr/yt-cli.git
cd yt-cli

# Create local bin directory if it doesn't exist
mkdir -p ~/.local/bin

# Copy and set execution permissions
cp yt ~/.local/bin/yt
chmod +x ~/.local/bin/yt
```

> **Note:** Ensure `~/.local/bin` is exported in your environment configuration file (`.bashrc` or `.zshrc`).

---

## Usage

Initialize the search pipeline directly from any active terminal instance:

```bash
yt
```

### Workflow

1. **Search:** Type your query directly into the interactive prompt.
2. **Navigate:** Use arrow keys or shell bindings (`Ctrl+N` / `Ctrl+P`) to browse results.
3. **Stream:** Press `Enter` to initiate media decoding in an isolated playback thread.

---

## Design Decisions

### Performance Over UI

Choosing a CLI framework eliminates the extensive memory allocations and rendering cycles required by modern Electron-based applications. This ensures highly predictable CPU profiles and minimal RAM usage during search operations.

### Tool Orchestration

Instead of a monolithic application, `yt-cli` acts as an orchestrator for mature, audited binaries. This modularity ensures the project remains small, maintainable, and deeply integrated with standard OS subsystems.

---

## Limitations

- **No Account Integration:** Features like algorithmic recommendations and proprietary playlist synchronization are intentionally omitted to prioritize privacy and speed.
- **Upstream Dependency:** Structural changes to external web platforms can lead to breakages until your local `yt-dlp` instance is updated (`yt-dlp -U`).
- **Codec Support:** Playback performance is bound strictly to the host system's hardware acceleration profiles within `mpv`.

---

## License

This project is licensed under the **Server Side Public License (SSPL) v1**.

By utilizing this software, you agree to the terms regarding local distribution and the requirements for open-source backend disclosure if the functionality is provided as a service. Please consult the accompanying `LICENSE` file for full statutory parameters.
