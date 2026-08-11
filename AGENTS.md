# Repository Guidelines

## Project Structure & Module Organization

This repository contains independent, notebook-led fine-tuning experiments:

- `Dental-LLM/`: dental prescription notebook and its JSON dataset.
- `Gemma-Moderation/`: Gemma 4 12B French message-moderation project.
- `README.md`: repository-level overview.

Keep project-specific notebooks, small configuration files, and documentation inside their project directory. Do not commit downloaded models, checkpoints, virtual environments, notebook checkpoints, or experiment logs; the root `.gitignore` excludes these artifacts. If reusable Python code is introduced, place it in `<project>/src/` and tests in `<project>/tests/`.

## Environment & Development Commands

There is no repository-wide build step. For Gemma moderation, create an isolated environment from the repository root:

```bash
cd Gemma-Moderation
uv venv .venv --python 3.12
source .venv/bin/activate
uv pip install unsloth unsloth-zoo datasets huggingface-hub pandas numpy scikit-learn matplotlib seaborn tqdm ipykernel
python -m ipykernel install --user --name gemma-moderation --display-name "Python 3.12 (Gemma Moderation)"
hf auth login
```

Select that kernel in VS Code before running the notebook. Validate notebook JSON without executing training using `python -m json.tool <notebook>.ipynb >/dev/null`.

## Coding Style & Naming Conventions

Use four-space indentation and PEP 8 for Python. Prefer `snake_case` for variables, functions, modules, and notebook filenames. Organize notebooks into short, ordered sections: environment, imports, data inspection, preparation, baseline, training, and evaluation. Keep credentials in environment variables; never embed Hugging Face tokens in cells or outputs.

## Testing Guidelines

This is a learning repository, so automated tests are not required for every notebook change. Work cell by cell and use lightweight sanity checks: inspect a few dataset rows, verify types and shapes, and trial training on 50–200 examples before starting a costly full run. Clear outputs containing secrets, large logs, or machine-specific paths. Add `pytest` tests only when reusable Python code moves into `src/`; place them under `tests/` using `test_*.py` names. Automated tests must never download full models or launch full training.

## Commit & Pull Request Guidelines

History uses short, imperative messages such as `chore: add gitignore` and `add: dental`. Prefer `<type>: <summary>` with types such as `add`, `chore`, `docs`, `fix`, or `test`. Keep commits scoped to one project. Pull requests should explain the learning objective, dataset or model changes, verification performed, and expected memory/storage impact. Include screenshots only for meaningful notebook visualizations.
