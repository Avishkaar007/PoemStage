# Poem Stage

One HTML file, wrapped as a native desktop app via Tauri. `web/index.html`
is the single source of truth — edit only that file.

```
poem-stage-app/
├── web/index.html         ← your app (edit this, nothing else)
├── src-tauri/              ← native desktop wrapper (Mac + Windows)
│   ├── src/main.rs
│   ├── Cargo.toml
│   ├── tauri.conf.json
│   └── capabilities/default.json
├── package.json
└── .github/workflows/      ← left as-is, see note below
```

Android/Capacitor support has been removed to keep this simple — just the
web app and one lightweight desktop wrapper.

## One-time local setup

Tauri needs Rust and (on Mac) the Xcode Command Line Tools — **not** full
Xcode.

```bash
xcode-select --install                                   # Mac only, ~500MB
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh   # installs Rust
```

Then, from the repo root:

```bash
npm install
```

## Running locally

```bash
npm run dev     # opens the desktop app in a native window, live-reloads on change
```

For quick iteration on the poem itself, you can also just open
`web/index.html` directly in a browser — no Rust/Tauri involved at all.

## Building a real .dmg / .exe

```bash
npm run build
```

Output lands in `src-tauri/target/release/bundle/`.

## App icon

There's no icon set yet. Generate one from a single square PNG (1024x1024
recommended):

```bash
npx tauri icon path/to/your-artwork.png
```

This creates `src-tauri/icons/` with all required sizes and formats. Then
add the icon paths back into the `bundle.icon` array in
`src-tauri/tauri.conf.json`.

## About the GitHub Actions workflows

The workflows in `.github/workflows/` were left untouched, since they were
written for the previous Electron + Capacitor setup and reference commands
(`electron-builder`, `cap sync android`) that no longer exist in this repo.
They'll need updating before your next tagged release — happy to do that
whenever you're ready, it's a small change (swap the build step for
`npm run build` and point at `src-tauri/target/release/bundle/` instead).
The web deploy workflow (`deploy-web.yml`) is unaffected and still works
as-is, since `web/` didn't move.
