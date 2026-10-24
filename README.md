# Arm-Position-Robust Grip Selection for Myoelectric Prosthetic Hands via sEMG–IMU–Gaze–Vision Sensor Fusion

**MDM2 Case Study: Assistive Robotics for Improvement of Life Quality** (TH Deggendorf, WS 2026/27)
Track: Software & Simulation · Supervisor: Dr. Heidari

**Team:** Narean Ravichandra · Guttikonda Ayyappa Reddy      📄 **Proposal:** [One-Page Proposal (PDF)](docs/proposal/OnePage_Proposal_Prosthetic_Hand_Sensor_Fusion.pdf)

## Problem
Multi-grip myoelectric hands select a grip by classifying forearm sEMG trained in one arm posture. When a transradial amputee raises or extends the forearm, the sEMG patterns shift (the **limb-position effect**), the hand opens into the wrong grip, and the object is dropped. Unreliable control is a main reason users abandon electric prostheses.

## Solution
Fuse four sensor types so the hand selects the correct grip in every arm position:

| Input | Raw data | Processing | Output |
|---|---|---|---|
| sEMG (12 ch, ~2 kHz) | Forearm muscle activity | 20–450 Hz band-pass, 50 Hz notch, 200 ms windows / 50 ms step, MAV/WL/ZC/SSC features → classifier | Grip probabilities from muscles |
| Accelerometers / IMU | Forearm acceleration | Gravity vector → orientation; acceleration onset → reach phase | Arm position + reach timing |
| Eye tracker (100 Hz) | Gaze point in scene | Fixation detection (≥ 200 ms) | Target object location |
| Scene camera (25 fps) | Egocentric video | 224×224 crop at gaze → YOLOv8 object detection | Object class → grip prior |
| **Fusion** | All of the above | Bayesian decision fusion: P(grip) ∝ P_vision^wv · P_EMG+IMU^we, reliability-weighted, fallback if vision drops out | **One of 5 grips:** power, lateral, tripod, pinch, open palm |

## Data
**MeganePro** (Cognolato et al., 2020, *Scientific Data*): sEMG, accelerometer, gaze and scene video from transradial amputees and able-bodied subjects. Evaluated with leave-one-subject-out testing. Raw data is not committed; see `data/README.md` for download instructions.

## Target KPIs (amputee subjects)
| KPI | Target |
|---|---|
| Grip-selection accuracy | ≥ 90 %, and ≥ 15 pp above sEMG-only |
| Accuracy drop between forearm-orientation bins | ≤ 5 pp |
| Decision timing | Within the first 50 % of the reach phase |
| Processing time per decision | ≤ 50 ms |

## Versions (one per milestone)
| Version | Sensors | Purpose |
|---|---|---|
| v0 | sEMG | Baseline; quantifies the limb-position effect |
| v1 | sEMG + IMU | Arm-position compensation |
| v2 | sEMG + IMU + gaze + camera | Full Bayesian fusion |
| v3 | v2 + robustness | Electrode-shift and vision-dropout tests, demo video |

## Repository structure
```
src/
  emg/          sEMG filtering, windowing, feature extraction
  imu/          orientation, reach-phase detection
  vision/       gaze fixation, YOLOv8 object detection, object→grip prior
  fusion/       Bayesian decision fusion, reliability weighting
  evaluation/   leave-one-subject-out, metrics, plots
experiments/    scripts reproducing every result (v0–v3)
data/           download instructions (raw data not committed)
results/        figures and demo video
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
| P1 | 2026-10-24 | Proposal |
| P2 | 2026-11-04 | Literature map, bibliography, sEMG-only baseline (v0) |
| P3 | 2026-11-18 / 12-02 | IMU + gaze/vision pipeline (v1); Bayesian fusion (v2) |
| P4 | 2026-12-16 | Robustness experiments, demo video (v3) |
| P5 | 2027-01-13 | Final report & presentation |

## Key references
- Fougner et al. (2011). Resolving the limb position effect in myoelectric pattern recognition. *IEEE TNSRE*.
- Markovic et al. (2014). Stereovision and augmented reality for closed-loop control of grasping in hand prostheses. *Journal of Neural Engineering*.
- Cognolato et al. (2020). Gaze, visual, myoelectric, and inertial data of grasps for intelligent prosthetics. *Scientific Data*.
- Biddiss & Chau (2007). Upper limb prosthesis use and abandonment: a survey of the last 25 years. *Prosthetics and Orthotics International*.

## License
MIT
