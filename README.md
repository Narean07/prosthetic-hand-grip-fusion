# Sensor Fusion-Based Tremor Suppression with a Wrist Exoskeleton

**MDM2 Case Study: Assistive Robotics for Improvement of Life Quality** (TH Deggendorf, WS 2026/27)
Track: Software & Simulation · Supervisor: Dr. Heidari

**Team:** Narean Ravichandra · Guttikonda Ayyappa Reddy

## Overview
Pathological tremor (4–12 Hz) in Parkinson's disease and essential tremor makes daily tasks like eating, drinking and writing difficult.
This project simulates a 2-DOF wrist exoskeleton (flexion/extension and radial/ulnar deviation) that **fuses IMU and sEMG signals** to estimate tremor and cancel it while preserving the patient's voluntary movement.

## Approach
1. **Model:** Euler–Lagrange dynamics of the wrist plus exoskeleton, with anthropometric parameters
2. **Signals:** synthetic voluntary tasks with superimposed tremor, sensor noise and drift; public Ninapro sEMG data
3. **Estimators compared:**
   - IMU band-pass filter (baseline)
   - Weighted-frequency Fourier linear combiner (WFLC)
   - Kalman-filter IMU + sEMG fusion (main contribution)
4. **Control:** tremor-cancelling impedance controller driven by each estimate

## Target KPIs
| KPI | Target |
|---|---|
| Tremor power reduction (4–12 Hz) | ≥ 80 % |
| Voluntary-motion tracking error | ≤ 5° RMS |
| Tremor estimation delay | ≤ 30 ms |
| Peak actuator torque | ≤ 2 N·m |

## Repository structure
```
src/
  model/        wrist + exoskeleton dynamics
  signals/      voluntary motion, tremor, IMU/sEMG sensor models
  estimation/   band-pass, WFLC, Kalman fusion
  control/      tremor suppression controllers
experiments/    scripts that reproduce every result
data/           dataset download scripts (raw data not committed)
results/        figures and demo videos
docs/           proposal, bibliography, report, slides
tests/          unit tests
```

## Getting started
```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
```

## Milestones
| Phase | Date | Deliverable |
|---|---|---|
| P1 | 2026-10-21 | Proposal |
| P2 | 2026-11-04 | Literature map, bibliography, wrist model |
| P3 | 2026-11-18 / 12-02 | Baseline estimators; Kalman fusion + controller |
| P4 | 2026-12-16 | Demo, experiments & analysis |
| P5 | 2027-01-13 | Final report & presentation |

## Key references
- Rocon et al. (2007). Design and validation of a rehabilitation robotic exoskeleton for tremor assessment and suppression. *IEEE TNSRE*.
- Riviere, Rader & Thakor (1998). Adaptive canceling of physiological tremor for improved precision in microsurgery. *IEEE TBME*.
- Atzori et al. (2014). Electromyography data for non-invasive naturally-controlled robotic hand prostheses. *Scientific Data*.

## License
MIT
