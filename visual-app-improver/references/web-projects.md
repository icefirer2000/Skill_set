# Web projects

Use this mode for local sites, browser applications, WebGL scenes, and browser-based 3D visualizations.

## Launch and lifecycle

- Find the intended command from `package.json`, lockfiles, framework configuration, project documentation, or an existing running process.
- Prefer the repository's package manager and existing scripts. Do not change package managers or regenerate lockfiles without a concrete need.
- Start the development server in a persistent terminal session and retain its session or process identity. Reuse it for later reloads.
- Wait for the actual listening URL and successful compilation before opening the page. Do not infer a port solely from framework defaults.
- Do not kill unrelated processes or broad groups of runtimes. Stop only a process started by this workflow when cleanup is appropriate and its identity is known.

## Browser observation

- Use the Browser skill and its documented runtime. Prefer the in-app browser for local web testing unless the user explicitly chooses another browser.
- Inspect the rendered page, not just source files. Capture screenshots at the same viewports and state after every meaningful change.
- Check console output, failed requests, missing assets, hydration errors, uncaught exceptions, and obvious performance stalls when those signals are available.
- Exercise the user-visible path needed to reach each required state. Do not mark an interaction as working based only on the presence of a handler in source.

## State matrix

Choose only states relevant to the request. Common examples are:

- initial load and settled default view;
- primary navigation or interaction;
- loading, empty, error, modal, or selected states;
- desktop and narrow/mobile layouts when responsiveness matters;
- hover, focus, keyboard, or reduced-motion behavior when required.

For WebGL or 3D scenes, also verify:

- model and texture loading;
- initial camera framing, scale, near/far clipping, and controls;
- representative orbit, zoom, selection, and reset states;
- lighting, materials, shadows, transparency, and background contrast;
- resizing and high-DPI behavior; and
- frame stability during representative interaction, without claiming a precise performance result unless it was measured.

## Editing and regression

- Fix source components, styles, shaders, scene configuration, assets, or build settings rather than the generated bundle.
- Preserve existing interaction semantics unless the requirements call for a change.
- Reproduce the same URL, viewport, state, and camera pose for before/after comparison.
- Run the project's focused tests or build after code changes, then perform visual verification. A passing build does not replace visual review.
