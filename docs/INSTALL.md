# Install

This repository is intentionally lightweight. The public demo uses only the Python standard library.

## Requirements

- Python 3.10 or newer
- Git
- No package install is required for the public demo

Check Python:

```bash
python --version
```

On some systems, use:

```bash
python3 --version
```

## Clone

```bash
git clone https://github.com/cbcraftlab/agent-execution-safety.git
cd agent-execution-safety
```

## Run The Built-In Safe Demo

```bash
python scripts/run_public_demo.py \
  --testset examples/testsets/demo-destructive-action.json \
  --events examples/events/demo-safe-events.jsonl \
  --out out/demo-safe
```

Expected:

```text
decision: recommended
score: 100
```

## Run The Built-In Unsafe Demo

The unsafe fixture intentionally exits with code `1` because it finds a critical blocker.

```bash
python scripts/run_public_demo.py \
  --testset examples/testsets/demo-destructive-action.json \
  --events examples/events/demo-unsafe-events.jsonl \
  --out out/demo-unsafe || true
```

Expected:

```text
decision: not_recommended
score: 40
```

## Optional Virtual Environment

No dependencies are required, but a virtual environment is fine if your workflow expects one.

```bash
python -m venv .venv
source .venv/bin/activate
```

Windows PowerShell:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

## Next Step

To test your own agent, continue with [TEST_YOUR_AGENT.md](TEST_YOUR_AGENT.md).

