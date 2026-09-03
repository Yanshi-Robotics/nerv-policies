# G1 flat parity policy, seed 42

This is the first registered locomotion policy for Anima One. It controls the Unitree G1 29-DoF
model in velocity-tracking tasks and exposes three bounded capabilities: `move_forward`,
`turn_left`, and `turn_right`.

The primary runtime artifact is `policy.onnx`. `model_9999.pt` is retained only as the original
training checkpoint for traceability and must be loaded only in a trusted Python environment. The
runtime contract fixes all 29 policy joints, the 480-dimensional observation, five history frames,
the 29-dimensional action, and the 50 Hz policy loop.

The release is copied byte-for-byte from the previously verified seed-42 release. Its four frozen
MuJoCo gates pass without the per-foot contact veto. This evidence establishes a sim2sim policy
baseline; it is not evidence of sim2real behavior, real-hardware safety, or a new full training
reproduction inside Anima One.

The source run's final checkpoint, ONNX export, contract, agent configuration, and legacy
environment snapshot are retained in the immutable Hugging Face release. Historical TensorBoard
events, intermediate checkpoints, play video, and local Git snapshot were not copied into Anima
One's `train/local/` directory. The legacy environment snapshot contains an old absolute asset path
and is retained only as evidence; clean retraining uses Anima One's tracked resource lock and
fetcher.

Training and evaluation lineage are recorded in `manifest.yaml`. The new Hugging Face tag remains
immutable once published.

On 2026-08-28, the same immutable ONNX artifact passed the four frozen gates again and passed a
separate capability contract covering 0.3 and 0.6 m/s forward command caps plus both turn
directions. It then completed a real APT AWI/MCP network acceptance of `move_forward`, `turn_left`,
and `turn_right`. A separate two-iteration GPU smoke proved the Anima One training, export, and
evaluation wiring; that smoke policy failed behavior acceptance and was not registered. See
`evidence/acceptance-2026-08-28.json` for the compact durable record.
