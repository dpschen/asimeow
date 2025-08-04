# Asimeow – Codex Prompt

_A Rust CLI that automates macOS **Time Machine** exclusions for dev projects._

## 🗂️ Project snapshot
- **Language / Edition:** Rust 2021
- **Primary binary:** `src/main.rs`
- **Build:** `cargo build --workspace --release`
- **Test:** `cargo test --workspace --all-features --quiet`
- **Lint:** `cargo clippy --workspace --all-features -- -D warnings`
- **Format:** `cargo fmt --all -- --check`
- **Docs:** `cargo doc --workspace --no-deps`

## ✅ What Codex should do
1. Fix bugs surfaced by failing tests or clippy lints.  
2. Add small features behind the existing `clap` sub-command structure.  
3. Improve inline docs and ./_docs markdown.  
4. Keep the binary **cross-compilable** (Linux CI must pass even if `tmutil` is macOS-only).

## ❌ What Codex must NOT do
- Do **not** rename public structs or CLI flags without an explicit task.  
- Do **not** introduce `unsafe` Rust unless absolutely required and documented.  
- Do **not** add new dependencies over level 0 without prior approval (`anyhow`, `clap`, `serde`, `glob` are OK).

## 🧪 Runbook (Codex: copy-paste these)
```bash
# unit + integration tests
cargo test --workspace --all-features --quiet
# lints must be clean
cargo clippy --workspace --all-features -- -D warnings
# formatting
cargo fmt --all -- --check
```

## ✍️ Commit & PR style
- Follow **Conventional Commits** (`feat:`, `fix:`, `chore:`).  
- One logical change per commit; squash-merge is OK.  
- Commit message body should contain _why_, not _how_.

## 💡 Coding conventions
- Use iterator adapters over manual loops where practical.
- Prefer `&Path`/`&PathBuf` over `String` for file paths.
- All public APIs require doc comments (`/// …`).
- Prefer simple code; avoid extra layers.
- Duplication OK when clearer than abstraction.

## 🪤 Common pitfalls
- `explorer::State` uses `RwLock`; avoid dead-locks by keeping critical sections small.  
- Tests run on Linux CI; direct calls to `tmutil` must be behind `#[cfg(target_os = "macos")]`.  
- The default config file lives in `~/.config/asimeow/config.yaml`; use `expand_tilde` helper.

## 🤝 Reviewer checklist (for Codex and humans)
- [ ] Tests & clippy pass  
- [ ] No new `unsafe` blocks  
- [ ] Commit messages follow spec  
- [ ] Feature docs updated (`README.md` or `_docs/`)
