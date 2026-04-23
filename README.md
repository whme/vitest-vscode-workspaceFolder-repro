# vitest-vscode-workspaceFolder-repro

Minimal reproduction for [vitest-dev/vscode](https://github.com/vitest-dev/vscode): the Vitest VS Code extension does not resolve `${workspaceFolder}` in `vitest.rootConfig` (and other path-valued settings).

## Setup

```bash
pnpm install
```

## Reproduce

1. Open this directory in VS Code with the [Vitest extension](https://marketplace.visualstudio.com/items?itemName=vitest.explorer) installed.
2. Open the Testing panel or run "Vitest: Show Output Channel".
3. Observe: the extension fails to discover tests because `${workspaceFolder}` in `.vscode/settings.json` is not resolved.
4. Replace the `vitest.rootConfig` value in `.vscode/settings.json` with an absolute path (e.g. `/home/you/vitest-vscode-workspaceFolder-repro/config/vitest.config.ts`) — tests are discovered correctly.

## Why the config is in `config/`

The Vitest config is placed in `config/vitest.config.ts` (not the project root) so the extension's default config search does not find it. This forces the extension to rely on `vitest.rootConfig`, which is exactly the setting that fails to resolve `${workspaceFolder}`.
