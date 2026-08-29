# Data Directory (`/data`)

This directory is designated for datasets used for AI model training, benchmarking, and signal validation.

## Benchmark Dataset: CWRU Bearing Dataset

Due to lack of immediate access to live industrial motor hardware during initial development, model validation will utilize the **Case Western Reserve University (CWRU) Bearing Dataset**:
- **Source**: Case Western Reserve University Bearing Data Center
- **Signal Types**: Accelerometer vibration signals (Drive End & Fan End)
- **Fault Conditions**: Normal baseline data, Inner Race Faults, Outer Race Faults, Ball Element Faults
- **Fault Severities**: 0.007", 0.014", 0.021", 0.028" damage diameters under various motor loads (0 to 3 HP)

## Planned Subdirectory Structure (Phase 2)
```
data/
├── raw/         # Raw CWRU .mat or .csv files (git ignored)
├── processed/   # Extracted feature arrays & windowed datasets (git ignored)
└── README.md    # Dataset documentation
```

---
> **Note**: Raw and processed dataset files are automatically excluded from Git tracking via `.gitignore`.
