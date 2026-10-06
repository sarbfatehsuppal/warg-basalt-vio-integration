# Validation Plan

The task requires testing BasaltVIO's effectiveness, not only confirming that it runs.

## 1. Stationary Drift

Keep the OAK-D stationary for a fixed duration and record estimated position/orientation drift.

Suggested outputs:
- Final displacement magnitude
- Drift over time
- Orientation drift

## 2. Translation Test

Move the camera a known distance along a measured straight path.

Record:
- Ground-truth displacement
- Estimated displacement
- Absolute error
- Relative error

## 3. Rotation Test

Rotate the camera by a known angle with minimal translation.

Record:
- Ground-truth angle
- Estimated angle
- Orientation error
- Position drift introduced during rotation

## 4. Closed-Loop Test

Move the camera through a path and return it to the starting point.

Record:
- Final estimated offset from the origin
- Orientation offset
- Accumulated drift

## Potential Failure Sources

- Camera/IMU calibration
- Camera-to-IMU extrinsics
- Timestamp synchronization
- Stereo frame synchronization
- Coordinate-frame conventions
- Motion blur
- Poor lighting
- Feature-poor environments
- IMU bias/noise
