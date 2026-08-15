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

