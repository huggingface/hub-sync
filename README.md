# hub-sync action

A GitHub Action that syncs your repository to Hugging Face Hub 🤗

Uses the official HF CLI via `uvx` for fast, reliable deployments to Spaces, Models, or Datasets.

## Quick Start

Add your HF token as a GitHub secret (`HF_TOKEN`), then:

```yaml
name: Sync to Hugging Face
on:
  push:
    branches: [main]

jobs:
  sync:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: huggingface/hub-sync@main
        with:
          github_repo_id: ${{ github.repository }}
          huggingface_repo_id: username/repo-name
          hf_token: ${{ secrets.HF_TOKEN }}
```

## Usage

### All Options

```yaml
- uses: huggingface/huggingface-sync-action@main
  with:
    # Required
    github_repo_id: ${{ github.repository }}
    huggingface_repo_id: username/repo-name
    hf_token: ${{ secrets.HF_TOKEN }}
    
    # Optional
    repo_type: space              # space | model | dataset (default: space)
    space_sdk: gradio             # gradio | streamlit | docker | static (default: gradio)
    private: false                # Create as private (default: false)
    subdirectory: ''              # Sync only this folder (default: '' = root)
```

## Features

- **Automatic exclusions** — `.github/` and `.git/` filtered via `--exclude`
- **True mirroring** — deletes removed files from HF using `--delete="*"`
- **Subdirectory support** — perfect for monorepos
- **Custom commit messages** — synced commits say "Sync from GitHub via huggingface-sync-action"
