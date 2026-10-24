# Data

This project uses the **MeganePro** dataset (Cognolato et al., 2020, *Scientific Data*):
sEMG, accelerometer, eye-tracker gaze and scene-camera video recorded during grasping,
from transradial amputees and able-bodied subjects.

Raw data is **not** committed to this repository (size and licence).

1. Download MeganePro from the source linked in Cognolato et al. (2020).
2. Place the files in `data/raw/` (ignored by git).
3. Run `python experiments/prepare_data.py` to build the processed dataset.

Please cite the dataset in any use of this code.
