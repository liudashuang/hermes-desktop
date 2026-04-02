# Contributing

This project is a desktop wrapper around Hermes Agent built with Electron, React, and TypeScript. Contributions are welcome for UI improvements, installer flow, Hermes integration, profile management, and packaging.

## Before You Start

- Read the project overview in [README.md](/Users/fathah/Desktop/projects/opensource/hermes-desktop/README.md)
- Keep changes focused and easy to review
- Prefer small pull requests over large mixed-purpose ones
- If your change affects onboarding, installation, or provider setup, test that flow end to end when possible

## Local Setup

### Prerequisites

- Node.js
- npm
- A Unix-like shell environment

Install dependencies:

```bash
npm install
```

Start the app in development mode:

```bash
npm run dev
```

## Development Workflow

Lint your changes:

```bash
npm run lint
```

Run TypeScript checks:

```bash
npm run typecheck
```

Build the app bundle:

```bash
npm run build
```

Platform packaging commands:

```bash
npm run build:mac
npm run build:win
npm run build:linux
```

## Project Layout

```text
src/main/                Electron main process, native integration, IPC handlers
src/preload/             Safe API bridge exposed to the renderer
src/renderer/src/        React UI, screens, styling, and client logic
resources/               Icons and packaged assets
build/                   Packaging configuration and platform resources
```

## Contribution Guidelines

### Keep Main, Preload, and Renderer Boundaries Clear

- Put OS access, process spawning, filesystem access, and Electron IPC handlers in `src/main/`
- Expose renderer-safe APIs from `src/preload/`
- Keep React components and presentation logic in `src/renderer/src/`
- Do not access Node or Electron internals directly from renderer components when a preload bridge is the safer fit

### Follow Existing Patterns

- Match the existing TypeScript style and naming conventions
- Keep components small and focused
- Reuse existing IPC and config patterns before introducing new abstractions
- Prefer extending current screens and modules over duplicating similar logic

### UI Changes

- Test both the initial setup flow and the main app layout if your change affects navigation or onboarding
- Preserve desktop behaviors like streamed chat updates, profile switching, and menu shortcuts
- Avoid introducing visual changes that break smaller window sizes

### Installer and Hermes Integration Changes

- Be careful with anything that touches `~/.hermes`, config files, or spawned Hermes processes
- Prefer additive, reversible changes in install and setup flows
- If you change provider handling or environment variables, verify the corresponding setup screen and main-process integration still align

## Pull Request Checklist

Before opening a PR, try to make sure:

- The app starts in development mode
- `npm run lint` passes
- `npm run typecheck` passes
- `npm run build` succeeds for your environment if your change could affect bundling
- Documentation is updated when behavior or setup changes
- Screenshots or short notes are included for visible UI changes

## Testing Notes

This repo currently has linting, typechecking, and build validation scripts, but no dedicated automated test suite in the app itself.

That means contributors should lean on:

- Manual verification in the desktop UI
- Linting with `npm run lint`
- Type safety checks with `npm run typecheck`
- Bundle validation with `npm run build`

## Good First Contribution Areas

- Polish onboarding and setup copy
- Improve settings and profile UX
- Refine chat and session management behavior
- Improve error handling around install and provider configuration
- Tighten packaging and release ergonomics
- Expand contributor and user-facing documentation

## Reporting Issues

When reporting a bug or opening a PR, it helps to include:

- Your OS and version
- Node.js version
- What command you ran
- What you expected to happen
- What actually happened
- Screenshots or logs for UI and installer issues

## Questions

If a change has unclear product or architecture impact, open an issue or draft PR early and describe the approach before investing in a large refactor.
