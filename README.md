# Qwen3 Abliterated Local Test (8B + 14B)

On-demand / every-15-min testing of two **abliterated (uncensored)** Qwen3 GGUF models on GitHub-hosted runners (CPU-only, no local storage used).

| Job | Model (Ollama tag) | Size | Runs on |
|---|---|---|---|
| `qwen-8b` | `hf.co/richardyoung/Qwen3-8B-Abliterated-GGUF:Q4_K_M` | 5.0 GB | CPU (runner 16GB RAM / ~14GB free disk) |
| `qwen-14b` | `hf.co/richardyoung/Qwen3-14B-Abliterated-GGUF:Q4_K_M` | 9.1 GB | CPU |

Each model runs in its **own job** (matrix) so every runner has a fresh ~14GB disk — the 27B FP8 (30.9GB) cannot fit on free GitHub runners.

## How it works

1. `actions/checkout` → clone repo
2. Install Ollama (`curl -fsSL https://ollama.com/install.sh | sh`)
3. `ollama pull <tag>` — downloads the abliterated GGUF
4. Runs a test battery (refusal probe + reasoning + tool-call JSON) with a 5-min timeout per prompt
5. Commits results to `results/run-<name>.md`

## Trigger

- **Manual:** Actions → *Qwen3 Abliterated Local Test* → *Run workflow*
- **Scheduled:** every 15 minutes (`cron: */15`)

## Results

Appended to `results/run-8b.md` and `results/run-14b.md` with a UTC timestamp per run.

## Not on GitHub (hard constraint)

| Model | Size | Why it can't run on free runners |
|---|---|---|
| Qwen3.8-27B Uncensored FP8 | 30.9 GB | Exceeds 16GB RAM and ~14GB free disk; no GPU on hosted runners |