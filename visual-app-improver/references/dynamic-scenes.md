# Dynamic scenes and controllable applications

Use this mode when acceptance depends on change over time: animation, continuous input, camera motion, physics, particles, simulation, media playback, game state, or other behavior that cannot be proved by one settled screenshot.

The goal is repeatability, not artificial determinism. Choose the lightest evidence method that can distinguish a real improvement from a different moment in the run.

## Classify reproducibility

Choose one level before comparing results:

1. **Deterministic checkpoint** — the target can load a known state and pause or advance to a known time or frame. Use this for exact visual comparison when available.
2. **Replayable sequence** — the same initial state and bounded input trace produce materially equivalent checkpoints, even if individual particles or physics details vary.
3. **Observational sample** — behavior cannot be replayed reliably. Run several bounded trials and assess explicit invariants or measured ranges instead of pixel equality.

Do not label a dynamic result deterministic merely because two captures look similar.

## Define the scenario

Record only the conditions needed to reproduce the requirement:

- build or executable identity and launch arguments;
- viewport or window size, display scaling, graphics quality, and input device;
- scene, level, dataset, user state, random seed, and initial camera or actor pose;
- whether focus, pointer lock, fullscreen, audio, or network access matters;
- ordered inputs with durations or event-relative timing; and
- named checkpoints with observable expected results and tolerances.

A concise trace may look like:

```text
setup: scene=training, seed=42, 1440x900, camera=default
checkpoint A: after assets-ready, idle pose and HUD complete
input: hold Forward for 1.0-1.2 s; release; rotate camera right about 30 degrees
checkpoint B: actor clear of spawn, walk cycle active, camera unobstructed
input: trigger Jump once; wait for grounded state
checkpoint C: actor grounded, animation returned to locomotion, no penetration
```

Prefer observable events such as `assets-ready`, `grounded`, or a visible state transition over unbounded sleeps. Use bounded timing tolerances when no state signal is available.

## Add test control only when justified

When editable source is available and ordinary interaction cannot reproduce the scene well enough, add the smallest development-only control seam that improves verification. Suitable controls include:

- a fixed random seed or recorded data fixture;
- a query parameter, launch flag, or debug command that loads a named scene;
- pause, resume, fixed time step, or single-frame advance;
- a known camera or actor pose;
- input recording and replay; or
- structured state and frame-timing output.

Keep these controls opt-in, local to development or testing, and separate from normal user behavior. Do not expose privileged state, weaken security checks, connect to production, or redesign application architecture solely for capture convenience. Document any test hook left in source.

## Capture temporal evidence

Use the smallest combination that proves the behavior:

- keyframes at setup, transition, representative motion, and final state;
- a short recording or ordered screenshot sequence when continuity or timing matters;
- structured application state for position, selection, collision, mode, or readiness;
- console, engine, resource, crash, or shader diagnostics; and
- measured frame-time or latency data when performance is an acceptance criterion.

Align before-and-after evidence by scenario and event checkpoint, not merely by wall-clock time after launch. Exact pixel comparison is appropriate only for deterministic frames with equivalent rendering conditions.

Do not convert impressions such as “feels smooth” or “responds instantly” into numeric claims. Report frame rate, frame time, dropped frames, input latency, memory, or loading duration only when an appropriate tool or application instrumentation measured them.

## Evaluate behavior

Select only criteria relevant to the request:

- animation start and completion, easing, blending, loop seams, and return to idle;
- visible input response, held-input continuity, simultaneous controls, focus, and pointer lock;
- camera framing, follow behavior, orbit limits, occlusion, clipping, shake, and reset;
- collision, grounding, boundaries, spawn, reset, pause, win, fail, and recovery states;
- particle, shader, lighting, skeletal, or procedural continuity;
- state transitions and whether visual feedback agrees with structured state;
- resizing, fullscreen changes, high-DPI behavior, and device-specific input; and
- stutter, long frames, resource churn, or degradation across a representative bounded run.

Separate correctness from product feel. Broken transitions, missed input, camera clipping, and state disagreement are observable defects. Difficulty, pacing, responsiveness preference, and “fun” require user criteria or an established design reference before material tuning.

## Handle non-determinism

- Fix seeds, time steps, fixtures, or initial states when the project already supports them or a small test seam is justified.
- If physics, procedural generation, async loading, or scheduling still varies, compare invariants and tolerances across repeated trials. Do not chase incidental particle positions or sub-frame differences.
- For networked or multiplayer behavior, isolate a local or mock environment when available. Do not create accounts, contact live players, send production traffic, or mutate remote state without specific authorization.
- When the automation surface cannot generate required reflex timing, analog input, multiple simultaneous controls, or reliable pointer lock, use an in-project replay/test harness or focused engine tests. Mark the scenario blocked if neither path exists; do not approximate it and claim a pass.

## Verify each change

After a coherent fix:

1. restore the same build, scenario, seed or fixture, viewport, camera, and initial state;
2. replay the same inputs within the recorded timing tolerance;
3. capture the same checkpoints and runtime signals;
4. compare required temporal and visual criteria;
5. repeat variable trials when the conclusion depends on non-deterministic behavior; and
6. test adjacent transitions, reset paths, and idle behavior for regressions.

Stop adding instrumentation or retries when they no longer improve confidence in a stated requirement. Report the reproducibility level, trials performed, measured signals, and any scenario that remained blocked.
