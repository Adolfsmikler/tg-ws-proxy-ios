<h1 align="center">TG WS Proxy iOS (Workflow Fix Fork)</h1>

<h4 align="center">Local MTProto proxy for Telegram on iOS featuring a Rust core, Live Activity, and an embedded Silent Audio sandbox bypass. Built via GitHub Actions.</h4>

<p align="center">
  <a href="../README.md">Русский 🇷🇺</a>
</p>

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-GPLv3-blue?style=for-the-badge&logo=gnu&logoColor=white" alt="GPLv3"></a>
  <img src="https://img.shields.io/badge/iOS-17%2B-black?style=for-the-badge&logo=apple&logoColor=white" alt="iOS 17+">
  <img src="https://img.shields.io/badge/Swift-SwiftUI-F05138?style=for-the-badge&logo=swift&logoColor=white" alt="SwiftUI">
  <img src="https://img.shields.io/badge/Core-Rust-000000?style=for-the-badge&logo=rust&logoColor=white" alt="Rust">
</p>

---

**TG WS Proxy iOS** runs the Rust version of TG WS Proxy on an iPhone and provides Telegram with a local MTProto endpoint:

```text
Telegram → 127.0.0.1:1443 → Rust TG WS Proxy → WSS / Cloudflare → Telegram DC
```

> [!CAUTION]
> **This is an experimental networking tool. Use it entirely at your own risk. The application has not undergone a security audit.**

---

## 🤖 AI Disclaimer
> [!NOTE]
> All build script fixes, Xcode 16.2+ compiler patches, iOS sandbox bypasses, and CI/CD automation setups in this fork were implemented in close collaboration with the **Gemini AI**. The author is not responsible for any hidden bugs or future breakages.

---

## ⚡ Fork Features (What's Fixed)
This repository fixes critical compilation errors found in the original project under recent Xcode versions (16.2+), removes the breaking `.glassEffect` UI modifier, and adds automated cloud build scripts via **GitHub Actions** without requiring a physical Mac computer.

---

## 📦 Free Apple ID Sandbox Bypass (Important!)

In the original project, background execution on a free developer account was impossible because the system VPN (`NetworkExtension`) dropped after 8 seconds due to missing paid signature entitlements [creative-writing-pad].

This fork introduces an **Automated Silent Audio Engine Patch** that completely solves this problem [travel]! When building with the **`-c la`** flag, the script automatically injects an infinite silence generator into the Swift code [travel]. To iOS, the app looks like an active music player, which prevents process suspension and allows the Rust core to run indefinitely [travel]!

### ⚠️ Known Trade-offs & Bugs:
1. **Increased Battery Drain:** Because the audio engine and Rust core run continuously in the background, your phone will consume battery significantly faster [travel].
2. **Call Conflicts (Crucial Bug):** Making or receiving a cellular call (or VoIP call in other apps) causes iOS to force-mute our fake audio stream [travel]. **Once the call ends, you must manually restart the proxy (press Stop -> Start)** to restore background privileges.
3. **Media Conflicts:** Music players (Apple Music, YouTube) might briefly suspend the proxy loop when taking over the audio output [travel].

---

## 🧬 Origins, Sources and Credits

This project is the result of combining, modifying, and fixing a chain of open-source solutions:

- [Flowseal/tg-ws-proxy](https://github.com/Flowseal/tg-ws-proxy) — The original concept, the idea of bypassing restrictions via WebSocket, and the baseline proxy core.
- [amurcanov/tg-ws-proxy-android](https://github.com/amurcanov/tg-ws-proxy-android) — The actively maintained Rust core fork and Android version, used in this project as the upstream repository for automated weekly syncs.
- [reekeer/tg-ws-proxy-ios](https://github.com/reekeer/tg-ws-proxy-ios) — The original native Swift/SwiftUI graphical wrapper and Apple framework integration.
-

## 🚀 Cloud Build (GitHub Actions)

You don't need a Mac. Everything is built in the cloud:
1. Navigate to the **Actions** tab of your repository.
2. Select the **Build iOS IPA** workflow and click **Run workflow**.
3. Download the compiled `.ipa` from the **Artifacts** section and install via `iloader` or `Sideloadly` using the `-p side -c la` configuration [creative-writing-pad].

---

<p align="center"><sub>Workflow modification and bugfixes prepared by <a href="https://github.com">Adolfsmikler</a></sub></p>
