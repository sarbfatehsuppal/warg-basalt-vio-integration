# WARG BasaltVIO Integration

Project notes and validation workspace for my visual-inertial odometry contribution to the Waterloo Aerial Robotics Group (WARG).

## Official WARG Contribution

The implementation is in the official UWARG autonomy repository:

- [Draft pull request #231 — Add initial OAK-D BasaltVIO integration and tests](https://github.com/UWARG/autonomy-monorepo/pull/231)
- [Implementation snapshot in the camera module](https://github.com/UWARG/autonomy-monorepo/tree/eaf085f641effa3436bc88653069244cdf0adaf6/camera)
- [Task #193 — Add Visual Odometry via BasaltVIO](https://github.com/UWARG/autonomy-monorepo/issues/193)

This repository holds project notes and future experiment results. The source changes are maintained in WARG's repository.

## Project Goal

Integrate BasaltVIO with the OAK-D stereo camera and IMU pipeline to expose local position and orientation estimates for GPS-denied navigation research.

## Current Status

**Initial implementation submitted as a draft PR; hardware validation pending.**

The contribution has not been merged. Real-camera startup, calibration, tracking accuracy, drift, and runtime performance have not yet been validated.

## Implemented

- Optional BasaltVIO support in the Python OAK-D camera module.
- Shared stereo image streams for depth processing and VIO, plus raw accelerometer and gyroscope inputs.
- A `VioPose` data structure containing position, orientation, SDK timestamp, and host receipt time.
- Nonblocking pose polling with invalid-message handling and quaternion normalization.
- Pipeline and queue cleanup.
- A CSV recording tool for hardware trials.

## Local Software Checks

- **16 hardware-free unit tests passed.**
- Ruff checks passed for the changed Python files.
- Python syntax checks passed.
- `git diff --check` passed.
- The recording tool's `--help` command was verified.

The unit tests use mock messages and queues. They check pose conversion, timestamps, invalid data, bounded polling, and cleanup. They do not validate real SDK pipeline wiring, sensor synchronization, calibration, or physical tracking accuracy.

Development environment: Ubuntu 24.04 on WSL 2, Python 3.12, DepthAI 3.10.0 with BasaltVIO available.

## Remaining Hardware Work

- Configure OAK-D USB access through WSL, or use a suitable Linux test computer.
- Run the official BasaltVIO example and the integration with an actual camera.
- Check RGB/depth capture alongside VIO.
- Record stationary, measured-translation, rotation, and return-to-start trials.
- Investigate timestamps, calibration, coordinate frames, pose gaps, and runtime load.
- Document measured results, fix issues, and finish review of the WARG PR.

No physical accuracy or drift measurements are reported yet.

## Repository Structure

```text
docs/           Project architecture, setup notes, and test plan
scripts/        Standalone utilities and analysis scripts
experiments/    Raw experiment notes/data by test type
results/        Processed results and summary tables
plots/          Figures generated from validation data
```

## Related Resources

- [UWARG autonomy monorepo](https://github.com/UWARG/autonomy-monorepo)
- [Luxonis BasaltVIO example](https://docs.luxonis.com/software-v3/depthai/examples/vslam/basalt_vio)
