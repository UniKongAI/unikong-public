# Whim — Desktop Releases

Public distribution channel for [Whim](https://unikong.ai) desktop builds on **Windows**: the installers and the in-app auto-update feed live here. **No source code** — the application source is private ([`UniKongAI/whim-app`](https://github.com/UniKongAI/whim-app)).

## Download

| Channel | File | Stable link |
|---|---|---|
| **Recommended** — guided installer | `whim-setup.exe` (Inno Setup, per-machine) | [latest/download/whim-setup.exe](https://github.com/UniKongAI/whim-releases/releases/latest/download/whim-setup.exe) |
| Enterprise / IT (GPO, Intune) | `whim.msi` (WiX MSI, per-machine, in-place major upgrade) | [latest/download/whim.msi](https://github.com/UniKongAI/whim-releases/releases/latest/download/whim.msi) |

Both install per-machine to Program Files (one UAC prompt), register the `whim://` SSO protocol handler, and uninstall cleanly via Add/Remove Programs.

## Auto-update

Whim's in-app updater (WinSparkle) polls `appcast-windows.xml` from this repo's latest release, verifies the entry's **EdDSA signature** against the public key shipped inside the app, downloads `whim-setup.exe`, and runs it as a silent in-place upgrade (one UAC prompt — per-machine install). A tampered feed or binary will not install.

- Feed URL: `https://github.com/UniKongAI/whim-releases/releases/latest/download/appcast-windows.xml`
- Manual check: **Whim → Settings → Check for updates**

## Release conventions

- Each release is tagged to match the app version, e.g. `v1.1.0-b97`.
- Assets keep **canonical names** (`whim-setup.exe`, `whim.msi`, `appcast-windows.xml`) so the `releases/latest/download/...` links never change; the appcast pins its enclosure to the tag-scoped URL so historical entries stay valid.
- Artifacts are built and signed locally, then published with `gh release upload` — there is no CI in this repo.

---

© UniKong · <https://unikong.ai>
