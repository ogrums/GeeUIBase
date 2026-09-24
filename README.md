# GeeUIBase

Shared Android libraries for the Letianpai desktop robot. This repository is not a product app. Other apps copy the command names and gesture steps defined here.

## Modules

| Module | Package | Role |
|---|---|---|
| `CommandLib` | `com.renhejia.robot.commandlib` | Command strings, MCU/AT ids, sensor names, package names of other robot apps, Gson models |
| `GestureFactory` | `com.renhejia.robot.gesturefactory` | Turns a gesture name into a list of `GestureData` steps |
| `library` | `top.keepempty.sph.library` | `LogUtil` only. The serial-port CMake block in Gradle is commented out |
| `app` | `com.geeui.base` | Empty sample activity |

## What a gesture step contains

`GestureData` is one step. It can carry a face, TTS text, ear (antenna) motion, foot motion, a sound effect, an antenna light, an interval, and an end flag.

`GestureManager.getInstance().getRobotGesture(name)` returns that list. Names in `GestureConsts` include `startup`, `shutdown`, `batlower`, `standby`, `wakeup`, `hand_recognition`, and `Fallprevention`. `GestureCenter` builds those sequences. `FixedGestureCenter` holds a fixed set of about forty gestures.

## Names other repos depend on

- `CommandConsts` — command types: voice, foot engine, ear engine, visual, speech, video call, remote view, wake-up.
- `MCUCommandConsts` — `controlMotion`, `controlAntennaMotion`, `controlAntennaLight`, `powerControl`, `resetMcu`, factory and TRTC strings.
- `ATCmdConsts` — integer ids for `AT+MOVEW` (forward, back, turn, shake, stamp, stand). The MCU firmware uses the same names.
- `SensorConsts` — `light`, `touch`, `cliff`, `suspend`, `waggle`, `down`, `IR`, `tof`. Touch tap / double-tap / long-press are 1 / 2 / 3.
- `PackageConsts` — hard-coded package and class names (`com.geeui.face`, launcher, speech, alarm, weather, OTA, and others).

There is no AIDL, HTTP client, or serial port in this tree. Cross-app coupling is these strings.

## Comment glossary

| Where | Chinese | English |
|---|---|---|
| `GestureManager` | 姿态管理 / 获取姿态 | Gesture management / get the gesture |
| `GestureCenter` | 姿态中心 | Gesture center |
| `GestureCenter` | 开机 / 关机 / 低电量 / 待机 | Power-on / power-off / low battery / standby |
| `GestureCenter` | 避障 / 摇晃 / 落地 / 倒下 | Obstacle avoidance / shake / landed / fallen over |
| `GestureConsts` | 悬崖姿态 | Cliff gesture |
| `FixedGestureCenter` | 固定的四十几个姿态 | A fixed set of about forty gestures |
| `CommandConsts` | 足部引擎 / 耳朵引擎 | Foot engine / ear engine |
| `SensorConsts` | 红外灯，上桩用 / 红外，测距用 | IR lamp used for docking / IR used for ranging |

## Build

Android Gradle Plugin 7.3.1. `CommandLib` and `library` use minSdk 26. `GestureFactory` uses minSdk 21 and depends on `CommandLib`.
