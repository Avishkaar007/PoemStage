# Poem Stage

 ### Live Demo 
https://avishkaar007.github.io/PoemStage/



One HTML file, wrapped as a native desktop app via Tauri. `web/index.html`
is the single source of truth — edit only that file for UI.

Executables like .dmg, .deb, .exe are handled by default by Github and can be accessed in Releases Section.

 Note : Shortcut keys aren't working in native apps , however WebApp is smooth.

#

## One-time local setup ( NOT Compulsory, just for Local Running enthusiasts )

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

