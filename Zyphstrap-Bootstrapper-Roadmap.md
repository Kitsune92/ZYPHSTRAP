# Zyphstrap — Bootstrapper Roadmap & Architecture

**Scope note:** This plan covers only the bootstrapper/launcher half of the original idea — the part modeled on Bloxstrap. It does **not** include any network proxy, real-time asset interception, live-game asset replacement, or a paid "hack client." Those pieces are explicitly out of scope and not addressed anywhere below. Everything here operates on the local client install (shortcuts, launch flags, local FFlag config, presence integration) — it never touches network traffic between the client and Roblox's servers.

---

## 1. Product Summary

Zyphstrap is a Roblox bootstrapper — a replacement launcher that sits between "click play" and the actual Roblox client process. It manages the local install, applies user-selected Fast Flags (client-side config values Roblox itself exposes), and adds quality-of-life features like Discord Rich Presence. It does not modify game files, inject into game memory, or intercept network traffic.

**Comparable to:** Bloxstrap, Fishstrap — bootstrapper-class tools, not mod/cheat tools.

---

## 2. In-Scope Features

### 2.1 Core Bootstrapping
- Download/update management for the Roblox client (mirrors Bloxstrap's version-fetch logic against Roblox's public deployment endpoints)
- Custom install location
- Launch argument handling (join links, protocol handler registration)
- Clean uninstall / repair install

### 2.2 FFlag Configuration UI
- Every flag presented as a plain-language toggle or dropdown — never raw key/value text
- Each flag ships with a one-line, non-technical description of what it visually/behaviorally changes
- Flags grouped by category (Rendering, UI, Performance, Experimental)
- "Experimental/unverified" flags visually separated and require an extra confirmation click, since undocumented flags can destabilize the client
- Reset-to-default button, and a diff view showing exactly what's changed from stock

### 2.3 Discord Rich Presence
- Shows current game/place name and session duration
- Optional "join" button using Roblox's standard join-link format
- User-toggleable per-game or globally off

### 2.4 Visual/Launcher-Level Customization (non-gameplay)
This is the safe subset of "customization" — things that change the *launcher's own UI* or trigger *Roblox's own supported client theme/UI settings*, not in-game 3D assets:
- Launcher theme (dark/light/custom accent colors)
- Custom desktop/start-menu icon for the shortcut
- Splash screen customization during boot

### 2.5 Onboarding & Support
- First-run guided tutorial (3–5 step walkthrough: install path, first FFlag toggle, Discord RPC opt-in)
- In-app links: Discord server, support email, website, YouTube, TikTok
- Searchable in-app FAQ / knowledge base pulled from a JSON manifest (easy to update without shipping a new build)
- Optional embedded tutorial video player (YouTube embed or local video) for each major feature

### 2.6 Diagnostics & Support Tooling
- "Copy diagnostic info" button (OS version, client version, active flags) for support tickets — no telemetry sent automatically, opt-in only
- Crash log viewer with a plain-English summary above the raw log

---

## 3. Explicitly Out of Scope

Stating this clearly so it's easy to keep the project honest as it grows:
- ❌ No local proxy or network traffic interception
- ❌ No real-time asset replacement (textures, meshes, sounds, animations) for any live game
- ❌ No game-specific "changers" tied to a particular title's assets
- ❌ No paid or free "hack client" of any kind
- ❌ No modification of anything that affects other players' experience or in-game fairness

---

## 4. UI/UX Structure

**Main window — left nav:**
1. **Home** — current install status, quick launch, version info
2. **FFlags** — categorized toggle list with search bar and descriptions
3. **Appearance** — launcher theme, icon, splash screen
4. **Integrations** — Discord RPC settings
5. **Help** — tutorials, FAQ, support links, diagnostics export

**Design principles (per your "clear interface" requirement):**
- Every setting visible without nested menus more than one level deep
- Plain-English descriptions above/beside every toggle, no jargon without a tooltip
- Search bar at the top of the FFlag page (Rivals-scale flag lists can get long even without game-specific modules)

---

## 5. Technical Architecture

**Stack (mirroring Bloxstrap's proven approach):**
- **Language/Framework:** C# / .NET 8, WPF or Avalonia for UI
- **Update mechanism:** Poll Roblox's public client-version API, download and verify via published checksums, no unofficial mirrors
- **Config storage:** Local JSON/XML config for FFlag state, versioned so updates can migrate old configs
- **Discord RPC:** Discord's official RPC SDK/IPC pipe — local only, no external server
- **Packaging:** MSI or Inno Setup installer with the first-run tutorial baked in

**Repo structure (suggested):**
```
/Zyphstrap
  /src
    /Bootstrapper       (download, install, launch logic)
    /FFlagManager        (flag definitions, UI bindings, validation)
    /RichPresence         (Discord IPC integration)
    /UI                   (views, theming)
  /resources
    /flag-manifest.json   (flag name, category, description, default)
    /faq.json
  /installer
```

---

## 6. Roadmap

**Phase 1 — Core Bootstrapper (4–6 weeks)**
- Install/update/launch pipeline
- Basic FFlag toggle UI (no descriptions yet, just functional)
- Minimal settings persistence

**Phase 2 — Polish & Content (3–4 weeks)**
- Full flag descriptions written for every exposed flag
- Discord Rich Presence integration
- Theming and splash screen customization
- First-run tutorial flow

**Phase 3 — Support Infrastructure (parallel, ongoing)**
- Discord server setup
- Support email
- FAQ manifest + in-app help center
- Initial tutorial video scripts (one per major feature: install, FFlag basics, RPC setup)

**Phase 4 — Public Beta**
- Closed beta with a small group for crash/stability feedback
- Diagnostic export tooling validated against real support tickets
- Public launch + first YouTube/TikTok walkthroughs

**Phase 5 — Iteration**
- Expand flag manifest as new Roblox flags are documented publicly
- Community-requested launcher theming options
- Ongoing update-pipeline maintenance as Roblox's client evolves

---

## 7. Promo/Support Notes

- One shared support email + linked social accounts (YouTube/TikTok) works fine for a project this size — just make sure whoever manages it has 2FA on, since it'll be a public point of contact.
- In-app links (Discord, socials, email) should live in a single "Help" panel rather than scattered across the UI, per the "clear interface" goal.

---

*This document intentionally excludes any proxy, asset-interception, or third-party hack-client component. If you want, a follow-up doc could go deeper on the FFlag manifest structure or the update-pipeline security model.*
