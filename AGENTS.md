# AGENTS.md

## Scope

This directory is a checked-out upstream dependency used as the editable `ms-swift` source for the root project.

## Default Rule

- Do not modify files here unless the task explicitly requires a change inside `ms-swift`.
- Prefer fixing integration issues in the root project first when the problem can be solved by registration, config translation, dataset formatting, or wrapper scripts.

## When Changes Here Are Appropriate

- The root project depends on behavior implemented directly inside `swift/*`
- A local registration hook or plugin contract no longer matches current `ms-swift` expectations
- A bug cannot be addressed from `qwen_event/*` or `scripts/*` without patching upstream behavior

## Working Guidance

- Minimize divergence from upstream; keep patches narrow and easy to rebase.
- Avoid broad refactors or style-only changes.
- If you change behavior used by the root project, document the integration assumption in the root repository docs or code comments near the call site.
- Read `README.md` and the relevant `swift/` module before editing.

## Integration Notes For This Repository

- The root `pyproject.toml` installs this directory as editable `ms-swift`.
- Phase 2 training and evaluation may depend on custom registration from the root project even when execution enters `swift`.
- Changes here should usually be paired with targeted validation from `tests/phase2`.

## Validation

- Start with the narrowest root-project Phase 2 test that exercises the integration point.
- Only run broader `ms-swift` tests when the change genuinely targets upstream internals in this submodule.
