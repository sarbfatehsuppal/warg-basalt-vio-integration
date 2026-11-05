# WARG BasaltVIO Integration

Project notes and validation workspace for my visual-inertial odometry contribution to the Waterloo Aerial Robotics Group (WARG).

## Official WARG Contribution

The implementation is in the official UWARG autonomy repository:

- [Draft pull request #231 — Add initial OAK-D BasaltVIO integration and tests](https://github.com/UWARG/autonomy-monorepo/pull/231)
- [Implementation snapshot in the camera module](https://github.com/UWARG/autonomy-monorepo/tree/5d035b50788e7b24d8c23277d15cb383e8fca3d6/camera)
- [Task #193 — Add Visual Odometry via BasaltVIO](https://github.com/UWARG/autonomy-monorepo/issues/193)

This repository holds project notes and future experiment results. The source changes are maintained in WARG's repository.

## Project Goal

Integrate BasaltVIO with the OAK-D stereo camera and IMU pipeline to expose local position and orientation estimates for GPS-denied navigation research.

## Current Status

**Software implementation and non-hardware validation complete; camera testing pending.**

The contribution has not been merged. Real-camera startup, calibration, tracking accuracy, drift, and runtime performance have not yet been validated.

## Implemented

- Optional BasaltVIO support in the Python OAK-D camera module.
- Shared stereo image streams for depth processing and VIO, plus raw accelerometer and gyroscope inputs.
- A `VioPose` data structure containing position, orientation, SDK timestamp, and host receipt time.
- Nonblocking pose polling with invalid-message handling and quaternion normalization.
- Pipeline and queue cleanup.
- A CSV recorder with environment/status manifests, interruption handling, silence detection, and no-overwrite protection.
- Offline analysis for measured stationary, translation, rotation, and return-to-start trials.
- SDK/hardware preflight and a complete camera-test procedure.

## Local Software Checks

- **49 hardware-free tests passed locally and in Linux GitHub Actions CI.**
- Ruff checks passed for the changed Python files.
- Python syntax checks passed.
- `git diff --check` passed.
- The recording tool's `--help` command was verified.

The automated tests use SDK doubles and known synthetic geometry, plus real SDK point/quaternion accessors. They check pipeline connections, pose conversion, timestamps, invalid data, bounded shutdown, CSV/manifest recording, failure handling, and analysis mathematics. They do not establish actual device operation, calibration, synchronization quality, or physical tracking accuracy.

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

## Camera Test Handoff

- [Setup and application API](https://github.com/UWARG/autonomy-monorepo/blob/basalt-vio-integration/camera/README.md)
- [Camera test procedure, trial commands, and report template](https://github.com/UWARG/autonomy-monorepo/blob/basalt-vio-integration/camera/vio_hardware_validation.md)
- [Passing Linux CI run](https://github.com/UWARG/autonomy-monorepo/actions/runs/42114463207)

The remaining validation requires the actual camera at the next test session. The PR is still a draft, and effectiveness results have not been measured.
