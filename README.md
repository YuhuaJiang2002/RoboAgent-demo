# RoboAgent Demo

**[Open the interactive demo](https://yuhuajiang2002.github.io/RoboAgent-demo/)**

A browser-based execution lab for RoboAgent, with a three-dimensional virtual
arm, orbit and top views, playback controls, a step inspector, and JSON export.

The three episodes replay actual `roboagent.core.run_task` records from an
in-memory two-joint robot:

- **Inspection pose:** feedback-driven movement to a joint target.
- **Transfer pose:** a second start/target configuration.
- **Out-of-bounds action:** the execution guard rejects the candidate before dispatch.

The demo performs zero physical robot commands and zero model-service calls.
Its geometry illustrates the recorded joint angles, not a calibrated digital
twin or a physics simulation.

## Trace Format

`episodes.json` contains the source module, recording mode, generation date,
action-space contract, and each episode's core trace.

| Field | Meaning |
| --- | --- |
| `observation` | Joint state, camera payloads, and observation timestamp. Demo camera payloads are empty. |
| `decision` | Selected policy, subtask instruction, or observed completion. |
| `proposed` | Validated policy action chunk, in declared units and axis order. |
| `attempted` | The bounded prefix dispatched to the in-memory robot. |
| `feedback` | The simulated controller's result. |
| `error` | A recorded execution or validation failure. |

The rejected episode also preserves its invalid `candidate` separately; it is
never relabeled as an executed action. Browser animation time is presentation
time, not model inference latency or real robot timing.

## Provenance

The trace exporter, frontend source, and tests are maintained in
[RoboAgent](https://github.com/YuhuaJiang2002/RoboAgent) under that repository's
access controls. This repository contains the static release only. GitHub Pages
publishes the `main` branch from the repository root.

Existing project licensing is preserved in [LICENSE](LICENSE). Three.js,
Lucide, and font license notices are included in
[THIRD_PARTY_NOTICES.txt](THIRD_PARTY_NOTICES.txt).
