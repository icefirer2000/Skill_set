# Desktop programs and executable files

Use this mode for native desktop applications, graphical tools, packaged games, and other locally runnable visual programs.

## Trust and editability

- Resolve the exact executable from the user-provided project or build output. Never choose among similarly named binaries by guesswork.
- Prefer building and launching from available source. Treat a newly downloaded or unknown executable as untrusted and obtain any required confirmation before running it.
- If only a binary is available, perform visual and functional assessment but do not patch executable bytes, decompile proprietary software, or promise a corrected build. Improvements may target editable configuration or assets only when the user placed them in scope.

## Launch and target selection

- Launch the exact path through the shell when authorized; do not automate a terminal or the Windows Run dialog through Computer Use.
- Use the Computer Use skill to list returned applications or windows and select exactly one target. Do not construct or guess window handles.
- Keep the target visible on the active Windows desktop when required. Capture the application window rather than unrelated desktop content unless the task specifically requires a full-screen result.
- Account for launchers, splash screens, modal dialogs, and secondary windows. Wait for the actual working view before establishing the baseline.

## Observation and interaction

- Capture the initial view and every required interaction state at a stable size and position.
- Use accessibility information for semantic controls when available and screenshots for visual judgment.
- Interact only with the authorized target application. Do not automate authentication dialogs, security tools, password managers, or the ChatGPT/Codex interface.
- Follow action-time confirmation requirements for deletion, submission, uploads, purchases, permission changes, and other consequential actions.

## Rebuild and verify

- Modify editable source, resources, or configuration, then use the project's normal build pipeline.
- Keep build outputs separate from user-authored source and do not overwrite an unrelated installed copy.
- Relaunch the newly built artifact and verify its version or build path before judging the change.
- Reproduce the same window dimensions, application state, and input sequence for before/after evidence.
- Close only processes started by this workflow, and only when their identity is known and closing them will not discard unsaved user work.
