# WARG BasaltVIO Integration

Visual-inertial odometry integration and validation using **BasaltVIO** and an **OAK-D stereo camera + IMU** for the Waterloo Aerial Robotics Group (WARG) autonomy stack.

> This repository is a personal project log and validation workspace for my WARG contribution. Production changes belong in the official UWARG `autonomy-monorepo`.

## Project Goal

Integrate BasaltVIO with the OAK-D camera pipeline so stereo imagery and IMU measurements can produce real-time 6-DoF pose estimates for GPS-denied UAV navigation.

## Planned Work

- Understand WARG's existing OAK-D / airside camera pipeline
- Run the official BasaltVIO + OAK-D example
- Integrate stereo camera and IMU data with BasaltVIO
- Expose pose / transform output for the autonomy stack
- Validate stationary drift, translation, rotation, and closed-loop behavior
- Document calibration, synchronization, coordinate-frame, and runtime issues
- Record test results and plots

## Repository Structure

```text
docs/           Project architecture, setup notes, and test plan
scripts/        Standalone utilities and analysis scripts
experiments/    Raw experiment notes/data by test type
results/        Processed results and summary tables
plots/          Figures generated from validation data
```

## Related WARG Work

- UWARG autonomy monorepo: https://github.com/UWARG/autonomy-monorepo
- WARG task: https://github.com/UWARG/autonomy-monorepo/issues/193

## Status

In development.
