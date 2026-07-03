# Roadmap / Improvement Backlog

Open tasks for the Attention-Based BCI project. Checkboxes so progress is visible in-repo.

Current baseline (single-subject BIJVZD, ATCNet, local, 1 seed): **10 epochs → 82.8% test accuracy, κ=0.657**.

## Correctness (highest priority)
- [ ] **Honest test metrics — don't SMOTE the test set.** Trials are pre-oversampled, so the held-out test split is synthetic and mildly optimistic. Apply SMOTE to the *training* split only; needs the raw pre-SMOTE trials.
- [ ] **Fit `StandardScaler` after the train/val split.** Standardization currently runs before `train()` splits off validation, so validation stats leak into the scaler. Split first, fit on train only.
- [ ] **Exception-safe file handles.** Wrap the `best models.txt` / `log.txt` opens in `with`/`try-finally` so a training error can't leak handles or truncate logs.

## Modeling / experiments
- [ ] Full 50-epoch, multi-seed training on the SLURM cluster; report mean ± std.
- [ ] Re-enable `EarlyStopping` (currently commented out) using the existing `patience` config.
- [ ] Multi-subject support: implement the subject→code mapping (only BIJVZD wired today) and add per-subject + LOSO (cross-subject) evaluation.
- [ ] Baseline comparison table: ATCNet vs ShallowConvNet vs EEGNet vs SVM on the same split.
- [ ] Light hyperparameter sweep (learning rate, dropout, `n_windows`).

## Engineering / repo quality
- [ ] Load each subject's `.npy` once — `load_ELIS_data` currently reads the full file twice (separate train and test calls).
- [ ] Move the hardcoded `run()` config to CLI args / a YAML file.
- [ ] Add `pytest` tests for split invariants (disjoint, stratified, correct shapes).
- [ ] Add a GitHub Actions CI (lint + tests).
- [ ] Pin dependency versions in `requirements.txt`.

## Docs
- [ ] Add the dataset access link + preprocessing notes to the README.
- [ ] Add a results table (accuracy / κ per subject) to the README.
