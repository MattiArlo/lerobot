# SO-101 Real-Time Hand Teleoperation (Vision-Based)

Control an **SO-101 Follower Robot Arm** in real time using webcam hand gestures with bumpless safety controls.

---

## Features

- **Side-by-Side Clean Layout**: The HUD dashboard is on the **LEFT** (380px), leaving the entire right area open and unobstructed for your right hand.
- **Freely Resizable Window**: Window uses `cv2.WINDOW_NORMAL` — click and drag window edges or maximize to full screen.
- **Responsive 2D Pinch Tracking**: Fast, sensitive pinch detection that closes to 0% and opens to 100%.
- **Center Neutral Target Box**: Guided starting area in the center of the camera view.
- **Bumpless Engagement (No Snapping/Jumping)**: A software slew-rate limiter smoothly ramps the arm at a safe speed from its current pose to the hand target.
- **True Physical Handedness**: Detected on raw camera frames so your right hand is always recognized correctly.
- **Hand Swap `[H]`**: Quickly toggle tracking between Right and Left hand.

---

## How to Start & Operate Correctly

### 1. Startup Sequence
1. Launch the visualizer:
   ```bash
   conda activate lerobot
   python examples/vision_hand_teleop/visualizer.py --robot --port /dev/ttyACM1
   ```
   *(Or omit `--robot` to test safely in simulation first).*
2. **Hold your right hand up inside the center target box** on the screen with your palm facing the camera.
3. The box border turns **glowing green** (`READY: Hand in Neutral Zone`).
4. **Press `[C]`**: Sets your hand's current position and depth as the zero/neutral reference pose.
5. **Hold `[SPACE]`** (or press **`[T]`** to toggle):
   - The clutch badge turns **Green (`[ CLUTCH ENGAGED - ACTIVE ]`)**.
   - The arm will **gently and smoothly glide** to match your hand without any sudden jerk.

---

## Hand Movement Mapping

| Gesture | Robot Motion |
|---|---|
| **Move Hand Left / Right** | Rotates base (`shoulder_pan`) |
| **Move Hand Up / Down** | Lifts arm up or down (`shoulder_lift`) |
| **Push Hand Closer to Camera** | Extends reach forward (`elbow_flex`) |
| **Pull Hand Back Towards Body** | Retracts elbow (`elbow_flex`) |
| **Rotate Palm Clockwise / Counter-Clockwise** | Rotates wrist (`wrist_roll`) |
| **Tilt Fingers Down / Up** | Tilts gripper pitch (`wrist_flex`) |
| **Pinch Thumb & Index Tips Together** | Closes gripper (0% pinch) |
| **Separate Thumb & Index** | Opens gripper (100% open) |

---

## Keyboard Controls

| Key | Function |
|---|---|
| **`[SPACE]`** (Hold) | Engage clutch (streams motion to follower arm) |
| **`[T]`** | Toggle continuous tracking ON / OFF |
| **`[C]`** | Re-zero/calibrate current hand position as neutral `(0, 0)` |
| **`[H]`** | Swap target hand (`Right` <-> `Left`) |
| **`[Q]`** or **`[ESC]`** | Quit visualizer and disable arm torque |
