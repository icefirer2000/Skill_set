---
name: visual-app-improver
description: Run and iteratively improve local visual projects and executable applications by observing repeatable states and input sequences, comparing them with requirements or references, fixing editable source, and verifying the result. Use for autonomous visual QA and refinement of web apps, desktop apps, animated interfaces, games, simulations, and 3D visualizations; do not use for non-visual binaries or production deployment.
---

# Visual App Improver

Turn a runnable visual project into a verified final version through an evidence-driven loop: launch, observe, evaluate, edit, rerun, and compare. Adapt the evidence to the target: stable screenshots for static states, and repeatable input traces plus temporal checkpoints for animated or continuously changing scenes.

## Establish the target

1. Resolve the exact project directory, runnable file, or launch command from the user's request or current workspace. Never guess between multiple plausible targets.
2. Read the supplied requirements, effect images, design references, and acceptance criteria. Treat them as the source of truth. If requirements are incomplete, make conservative assumptions that preserve the existing design and disclose them in the final result.
3. Determine whether editable source, assets, or configuration are available. A runnable binary without editable inputs can be assessed, but must not be binary-patched or represented as automatically fixable.
4. Inspect repository status before editing. Preserve user changes, avoid unrelated files, and modify source rather than generated build output when possible.
5. Discover the normal launch procedure from project metadata or documentation. Reuse an already-running development server when it is clearly the intended target; do not start duplicate services unnecessarily.

## Choose the visual surface

- For a browser-rendered project, read [references/web-projects.md](references/web-projects.md) and use the Browser skill for page interaction, screenshots, console inspection, and local web testing.
- For a native desktop program or graphical executable, read [references/desktop-executables.md](references/desktop-executables.md) and use the Computer Use skill for window capture and authorized interaction.
- If the result changes over time or depends on continuous input, physics, simulation, camera movement, or animation timing, read [references/dynamic-scenes.md](references/dynamic-scenes.md). Use its replay and checkpoint protocol instead of treating one screenshot as sufficient evidence.
- For either mode, read [references/visual-evaluation.md](references/visual-evaluation.md) when judging against an effect image, design reference, 3D scene, or detailed visual requirements.
- Prefer structured logs, DOM/accessibility state, application APIs, and test output for semantic facts. Use screenshots for appearance and visible interaction state.

## Preserve authorization boundaries

Running a normal local development command inside the user-provided project is part of this workflow. Do not treat the presence of an arbitrary executable as permission to run it.

Pause before:

- running newly downloaded, unknown, or untrusted software;
- connecting the project to production services or causing external side effects;
- performing account, payment, publishing, deletion, permission, or other sensitive actions;
- installing dependencies when the environment requires approval; or
- making a material product or design choice that cannot be inferred from the requirements.

Follow the active Browser or Computer Use confirmation policy for UI actions. Never weaken security controls to make the project run.

## Capture a stable baseline

1. Start the target and wait until required resources are loaded. For continuously changing scenes, establish a controlled checkpoint rather than waiting for motion to stop. Record launch failures and visible loading states instead of judging a half-loaded result as final UI.
2. Capture the smallest useful set of repeatable states: the default view, required interactions, important responsive sizes, and relevant camera angles or model states. For dynamic behavior, also record the initial conditions, input trace, timing tolerances, and checkpoints needed to reproduce it.
3. Record visible defects and supporting diagnostics such as build errors, console errors, failed resources, layout overflow, or broken interactions.
4. Convert requirements into an acceptance matrix. Mark each criterion `pass`, `partial`, `fail`, or `blocked`, with observable evidence. Distinguish observation from inference.

## Diagnose and prioritize

Rank issues by their effect on the requested outcome:

1. launch, rendering, or interaction failures;
2. missing or incorrect content and assets;
3. geometry, layout, camera, scaling, clipping, and responsiveness;
4. materials, lighting, color, typography, spacing, and visual polish;
5. performance or maintainability issues that visibly affect the experience.

Trace each issue to the smallest plausible source area before editing. Do not rewrite the architecture or replace the design merely because another implementation would be easier.

## Improve in a verification loop

For each coherent group of fixes:

1. Make the smallest source changes that address the highest-priority evidence.
2. Run focused checks or builds proportional to the change.
3. Reload or relaunch the target.
4. Reproduce the same state, viewport, camera, data, and interaction used in the baseline. Replay the same timed input trace when dynamic behavior is in scope.
5. Capture new evidence at the same checkpoints and update the acceptance matrix.
6. Check nearby states for regressions before continuing.

Continue autonomously while safe, relevant changes produce measurable progress. Do not ask the user to approve ordinary local edits one by one.

Stop the loop when one of these is true:

- all material requirements pass;
- the remaining difference is below the requested fidelity threshold and further changes would be speculative;
- two consecutive approaches fail to produce measurable improvement and a different requirement, asset, or user decision is needed;
- editable source or a required dependency is unavailable; or
- further work needs new authorization or would expand the requested scope.

## Deliver the final version

Leave the verified working version in the requested project location. Provide:

- the final runnable result and exact start command;
- final screenshots or temporal checkpoints for the states and sequences used in acceptance;
- a concise list of material fixes;
- tests, builds, interactions, input traces, and measured runtime signals verified;
- remaining deviations or blockers, if any; and
- the location of changed source files or produced artifacts.

"Directly output the final version" means continue through the safe edit-and-verify loop without requiring routine review. It does not waive confirmations, justify hiding unresolved failures, or authorize production deployment.
