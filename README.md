# kubeflow/trainer#4240 reproduction

Runs the `examples/local/local-container-mnist.ipynb` training setup from
kubeflow/trainer (two containers, `torchrun --rdzv-backend=static`, gloo on CPU)
in a loop on GitHub-hosted runners, and captures `ps`, per-thread kernel wait
channels and `py-spy dump --native --locals` for every Python process when a run hangs.

- `repro/run_once.sh`: one run, prints a `RESULT` line (OK, SLOW, HANG, NOFINISH, FAILED, ERROR).
- `repro/train.py`: the training function from the notebook.
- `.github/workflows/hang-repro.yaml`: 10 shards per PyTorch image, 120 minutes each.

Results are in each run's artifacts (`repro-<torch>-shard<n>`).
See https://github.com/kubeflow/trainer/issues/4240.
