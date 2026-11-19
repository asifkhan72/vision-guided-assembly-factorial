# Vision-guided assembly: replicated full-factorial experiment

Data, part CAD, and analysis code for the article *Assembly Success in a Vision-Guided
Robot Cell: A Replicated Full-Factorial Study* by Md Asif Khan Sharon and Amit J. Lopes.

The experiment was run in a UR3e cell with a Robotiq wrist camera and a Robotiq 2F-85
gripper. Four factors were varied in a full-factorial design: part color (lime green,
pink, red, royal blue), part configuration (rectangular, trapezium, cylindrical,
hexagonal), ambient illuminance (110 and 360 lx), and scanning height (250 and 300 mm).
Each of the 64 conditions was run twice, with ten assembly attempts per run, giving 128
runs and 1280 attempts. Every attempt was recorded as a completed assembly or as a
failure in one of four categories.

## Contents

| Path | Description |
|---|---|
| `data/attempt_level_outcomes.csv` | One row per attempt (1280 rows): outcome, failure category, and recorded completion time. |
| `data/run_level_counts.csv` | One row per ten-attempt run (128 rows): successes and failures by category. |
| `data/instrument_specific_power_ratios.csv` | Reflected-power measurements for the four part colors. |
| `raw/Experimentation1.xlsm` | Original experiment workbook. |
| `cad/` | STL files for the top and bottom part of each configuration. |
| `analysis.ipynb` | Reproduces the statistics, tables, and in-text numbers of the article and its Supplementary Material. |

## Data

All three CSV files were taken from the original workbook. Sheet `Final` holds the 128
runs in the order they were performed, with one column per attempt. A completed attempt
contains its completion time; a failed attempt is left blank and colored by failure
category, with the legend in the same sheet. `attempt_level_outcomes.csv` writes these
colors out as categories, and `run_level_counts.csv` sums the attempts within each run.

**Factor columns** (both outcome files)

| Column | Meaning |
|---|---|
| `Sl` | Run number, in the order the runs were performed (1–128) |
| `Color` | Part color |
| `Config` | Part configuration |
| `Ambient` | Ambient illuminance (lx) |
| `Height` | Scanning height, camera to background (mm) |
| `Rep` | Replicate run of the condition (1 or 2) |

**`attempt_level_outcomes.csv`**

| Column | Meaning |
|---|---|
| `Attempt` | Attempt number within the run (1–10) |
| `Success` | 1 if the assembly was completed, 0 otherwise |
| `Failure_category` | Blank for completed attempts; otherwise `bottom_part_not_recognized`, `wrong_orientation`, `mating_failed_correct_orientation`, or `could_not_focus` |
| `Completion_time_s` | Completion time recorded for a completed attempt (s); blank for failed attempts |

**`run_level_counts.csv`**

| Column | Meaning |
|---|---|
| `Success` | Completed assemblies out of 10 |
| `Recog`, `Orient`, `Mate`, `Focus` | Failures by category, in the order listed above |

**`instrument_specific_power_ratios.csv`** gives, for each color, the reference and
sample power (µW) at 450, 550, and 650 nm, the ratio of sample to reference power at each
setting (%), the mean ratio, and the color's assembly success rate (%).

## Reproducing the analysis

Requirements: Python 3.10 or later and the packages in `requirements.txt`.

```
pip install -r requirements.txt
jupyter notebook analysis.ipynb
```

Run all cells with the repository folder as the working directory. The notebook first
checks that the attempt-level records sum to the run-level counts. Each reported value is
then compared with the number printed in the article, and the last cell reports how many
match. Tables are written to `results/`. Random seeds are fixed in the notebook.

## CAD

`cad/` contains one STL file for the top and one for the bottom part of each
configuration, in millimetres. Parts were printed in PLA on a MakerBot Sketch.

## License

The code in `analysis.ipynb` is released under the MIT License (`LICENSE`). The data,
CAD files, and workbook are released under the Creative Commons Attribution 4.0
International License (`LICENSE-DATA`).

## Citation

If you use these files, please cite the article above.
