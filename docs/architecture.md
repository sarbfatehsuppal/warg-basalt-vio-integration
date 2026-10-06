# Architecture

## High-Level Data Flow

```text
OAK-D Left Camera  ─┐
                    ├──> BasaltVIO ───> 6-DoF pose / transform
OAK-D Right Camera ─┤
                    │
OAK-D IMU ──────────┘
```

The integration goal is to connect the OAK-D stereo image streams and IMU measurements to BasaltVIO, then expose the resulting pose estimate to WARG's autonomy stack.

## Components

### OAK-D
Provides:
- Left/right stereo image streams
- Accelerometer data
- Gyroscope data

### BasaltVIO
Consumes synchronized visual and inertial measurements and estimates the camera's motion over time.

### WARG Autonomy Stack
The final integration should make the estimated pose usable by the relevant airside/autonomy components.

## Open Questions

- Where is the existing OAK-D DepthAI pipeline created?
- Are the stereo streams already synchronized/rectified?
- Is an IMU node already present?
- What pose/odometry interface should BasaltVIO publish into?
- What coordinate frame does WARG expect?
