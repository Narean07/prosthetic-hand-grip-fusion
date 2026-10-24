# Experiments

| Script | Version | Sensors |
|---|---|---|
| `v0_emg_baseline.py` | v0 | sEMG only (LDA) |
| `v1_emg_imu.py` | v1 | sEMG + IMU |
| `v2_full_fusion.py` | v2 | sEMG + IMU + gaze + scene camera (Bayesian fusion) |
| `v3_robustness.py` | v3 | v2 with electrode-shift and vision-dropout tests |

Each script runs leave-one-subject-out evaluation and saves results to `results/`.
