# Visual evaluation

Use this rubric when the target must match an effect image, mockup, video frame, 3D reference, or detailed visual specification.

## Build an acceptance matrix

Translate the reference into testable criteria before editing. Cover only categories relevant to the target:

- composition, hierarchy, and overall silhouette;
- geometry, alignment, spacing, sizing, and clipping;
- camera position, projection, field of view, framing, and object scale;
- color, typography, icons, images, and content accuracy;
- materials, lighting, shadows, reflections, transparency, and background;
- responsive behavior and high-DPI rendering;
- interaction feedback, animation timing, transitions, and state changes;
- loading completeness, visible errors, and perceived stability.

For each criterion record:

- expected result;
- observed result;
- status: `pass`, `partial`, `fail`, or `blocked`;
- evidence source, such as screenshot, interaction, log, or test; and
- the smallest likely source area to inspect.

## Compare consistently

- Use the same viewport, window size, application state, data, camera pose, and zoom for before/after comparisons.
- Wait for fonts, images, models, textures, shaders, and animations to reach the intended stable state.
- Separate genuine defects from capture differences such as DPI scaling, browser chrome, compression, color management, or a mismatched camera.
- Use exact pixel comparison only when the target is expected to be deterministic and pixel-matched. Otherwise compare structure and perceptually important differences.
- Do not infer invisible functionality from a screenshot. Verify interactions directly and use logs or structured state for semantic facts.

## Prioritize useful changes

- Fix large structural and functional mismatches before fine polish.
- Prefer changes that improve multiple failed criteria without expanding scope.
- Preserve intentional existing behavior that the reference does not contradict.
- Treat subjective taste as a weak signal unless the user supplied a clear visual direction.

## Final evidence

The final set should include the smallest number of screenshots that proves the accepted states. Report unresolved differences honestly, including whether they stem from missing assets, unavailable source, runtime limitations, or ambiguous requirements.
