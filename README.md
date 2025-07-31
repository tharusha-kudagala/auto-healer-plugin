# 🤖 AI Auto-Healer GitHub Action

This GitHub Action sends your repository to a locally running AI fixer service (at nefraverse server) to automatically detect and resolve JavaScript/TypeScript build errors using LLMs like Mistral or DeepSeek via Ollama.

---

## 🚀 How It Works

1. Takes the current repository and branch.
2. Sends a `POST` request to your AI fixer server.
3. The fixer clones the repo, installs dependencies, tries to build, and applies auto-fixes.
4. If successful, it creates a Pull Request with the fixes.

---

## 📦 Inputs

| Name     | Description                          | Required | Default             |
|----------|--------------------------------------|----------|---------------------|
| `pat`    | GitHub Personal Access Token (Secret) | ✅ Yes   | —                   |
| `branch` | Branch to analyze                    | ❌ No     | `${{ github.ref_name }}` |

> 🔐 Your `pat` must have `repo` scope to create pull requests.

---

## 🛠️ Usage

```yaml
name: Run AI Fixer

on:
  workflow_dispatch:

jobs:
  auto-heal:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Run Auto-Healer
        uses: tharusha-kudagala/ai-auto-healer@v0.1
        with:
          pat: ${{ secrets.GH_PAT }}
          branch: main
