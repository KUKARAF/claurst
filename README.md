# CLAURST

An Azure-focused rewrite of the Claurst terminal coding agent, built in Rust.

This fork is configured to run against Azure OpenAI deployments. Secrets (API keys, endpoints) are managed via a [kv](https://kv.osmosis.page) server — **an account on kv.osmosis.page is required to use this build.**

## Setup

The following secrets must be present in your kv store:

| Key | Description |
|-----|-------------|
| `OFFENLEGUNG_API_ENDPOINT` | Full Azure OpenAI chat completions URL (includes deployment and api-version) |
| `OFFENLEGUNG_API_KEY` | Azure OpenAI API key |

The binary fetches these at startup via the `kv` CLI. Install the kv CLI and authenticate with your osmosis.page account before running.

## Install

Download the latest x86_64 Linux binary from [GitHub Releases](https://github.com/KUKARAF/claurst/releases/tag/latest):

```bash
wget -O ~/.local/bin/claurst https://github.com/KUKARAF/claurst/releases/download/latest/claurst
chmod +x ~/.local/bin/claurst
claurst
```

## Build from source

```bash
git clone https://github.com/KUKARAF/claurst.git
cd claurst/src-rust
cargo build --release --package claurst
```

## Azure model token limits

Queried directly from the Azure API and hardcoded:

| Model | Max completion tokens | Parameter |
|-------|-----------------------|-----------|
| `gpt-5` | 128 000 | `max_completion_tokens` |
| `gpt-5-chat`, `gpt-5.2-chat`, `gpt-5.3-codex`, `gpt-5.4`, `gpt-4.1`, `gpt-4o`, `gpt-4o-mini` | 16 384 | `max_tokens` |
