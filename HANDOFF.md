# unikong-public — Handoff (2026-06-06)

> A session-handoff to **re-align everything** around this repo. Written at the
> `whim-releases → unikong-public` rename so the next session picks up with full
> context. Read top to bottom, then work the **Open decisions** + **Pending refs**.

## What this repo is (now)

`UniKongAI/unikong-public` (**PUBLIC**) is the **org-level public distribution
channel** for UniKong products. Renamed from `whim-releases` on **2026-06-06**
(GitHub rename + local clone moved + remote URL updated; the old `whim-releases`
name **redirects**, so already-shipped binaries keep resolving).

Today it carries **Whim desktop (Windows)**:
- `whim-setup.exe` (Inno Setup, consumer) + `whim.msi` (WiX, enterprise) installers
- the **WinSparkle EdDSA-signed appcast** that whim-app's in-app updater polls
- a **multilingual download README** ("Whim for Windows", EN + 12 SEA/N-Asian langs)

Stable download URLs (used by the website, the README, and the app's updater):
- `https://github.com/UniKongAI/unikong-public/releases/latest/download/whim-setup.exe`
- `…/whim.msi`

## How it got here

- **Auto-update Track A locked (2026-06-03):** WinSparkle (Windows) + Sparkle
  (macOS, planned). EXE = update channel, MSI = enterprise-only. See whim-doc
  `RELEASES.md` + the `project-whim-desktop-autoupdate` memory.
- **whim-app build 102 (`b65f5d4`, Morgan)** shipped the **in-app WinSparkle
  updater** (`lib/core/updates/desktop_updater.dart`, `windows/runner/
  flutter_window.cpp`, vendored `WinSparkle.dll`, Settings → Check for updates,
  **Windows-only** gate). Its appcast/feed URL points at this repo.
- **unikong-website** gained a `WhimDownload` section on `products/whim` (3
  platform cards) — Windows live → this repo's `latest/download`; Android/Apple
  "Coming soon" pending store links. (Uncommitted; live on the local docker dev
  server at `localhost:3000`.)
- **Renamed `whim-releases → unikong-public`** to make it org-level (the suite:
  Whim + the IdP being built).

## ⚠️ Open decisions to re-align

1. **Multi-product `latest/download` collision.** GitHub Releases `latest` is
   **repo-wide**. The clean `…/latest/download/whim-setup.exe` URLs (website,
   README, app updater) work **only while Whim is the newest release in the
   repo**. The moment a 2nd product (the IdP) publishes a release here, `latest`
   can resolve to the wrong product. **Decide before a 2nd product ships:**
   per-product release tags + tag-pinned URLs, OR keep GitHub Releases Whim-only
   (other products as repo files/subdirs or their own `*-public` repo), OR split
   back to per-product repos.
2. **Repo layout for "org-level".** README is currently a Whim-Windows page (now
   multilingual). If this stays org-level, it likely wants a product index +
   per-product subdirs (`whim/`, `idp/`, …) for non-release assets.
3. **Windows code-signing cert** still absent → SmartScreen "unknown publisher"
   on first run of `whim-setup.exe`. Buy an Authenticode cert? (Also the
   prerequisite for any MSIX / App-Installer silent path.)
4. **macOS + Linux auto-update** not built — WinSparkle is Windows-only. macOS =
   Sparkle (notarized `.app`, arm64-only); Linux = AppImage + zsync. Both pending
   per the Track-A plan.

## Pending refs (rename swept locally — NOT committed/pushed)

The `whim-releases → unikong-public` rename was swept across these; all are
**uncommitted**, awaiting this re-align session (whim-app needs **push approval +
a Morgan sync** — it's his shipped feed URL):

| Repo | File | Change | Status |
|---|---|---|---|
| whim-app | `windows/runner/flutter_window.cpp` | WinSparkle feed URL → unikong-public | ⏸ local · **needs push approval + Morgan sync** (shipped 102 still uses whim-releases via redirect) |
| whim-app | `README.md` | desktop channel name | ⏸ local |
| unikong-website | `nuxt.config.ts`, `app/components/WhimDownload.vue` | download URLs + comments | ⏸ local (part of the live download-section work) |
| whim-doc | `RELEASES.md` | build-98 note channel name | ⏸ local |
| memory | `project-whim-desktop-autoupdate`, `MEMORY.md` | repo name | ⏸ pending |

## Still pending (product)

- **Play Store + Apple TestFlight URLs** — to provide; the website download
  cards show "Coming soon" until then
  (`nuxt.config runtimeConfig.public.downloads.{android,apple}` / `NUXT_PUBLIC_DL_*`).
- **Appcast generation/signing** — confirm the EdDSA keypair + a published
  `appcast-windows.xml` in this repo's releases match what whim-app's WinSparkle
  expects. The Windows installers **and** appcast are built on the `unk-pkn-lt001`
  Windows laptop (`flutter build windows` can't run on the Mac).
- **build-102 artifacts** — iOS IPA (→ Transporter) + macOS arm64 `.app`
  (→ Archive) built 2026-06-06; Android 102 already shipped; **Windows 102
  installers still to be built** on the laptop.

## Pointers
- Auto-update plan + build ledger: whim-doc `RELEASES.md` (builds 96–102),
  `satellite-repos.md`, the `project-whim-desktop-autoupdate` memory.
- Windows build host: `unk-pkn-lt001` (tailnet, SSH). Build env: `~/.cargo/bin`
  on PATH + `OPENSSL_ROOT_DIR=…/vcpkg/installed/x64-windows-static-md`.
- whim-app installers: `windows/installer/whim.iss` (Inno — has the `WizardSilent`
  + taskkill silent-update fixes) and `whim.wxs` (WiX MSI).

## Working rules

- **unikong-public is NOT an auto-push repo** — commit *and* push only with
  Steven's explicit approval (only `whim-doc` + `unikong-bridge` auto-push).
- Same for any cross-repo ref updates this session touches (whim-app especially —
  its WinSparkle feed URL is Morgan's shipped code; sync with him before pushing).
- This is a **re-alignment** session: settle the Open decisions above with Steven
  before mass-editing; surface choices one at a time.

---
_Created 2026-06-06 to anchor the unikong-public re-alignment session._
