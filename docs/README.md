<h1 align="center">TG WS Proxy iOS (Workflow Fix Fork)</h1>

<h4 align="center">Local MTProto proxy for Telegram on iOS featuring a Rust core, WidgetKit, Live Activity, and optional Packet Tunnel. Built via GitHub Actions.</h4>

<p align="center">
  <a href="README.md">Русский</a>
</p>

<p align="center">
  <a href="LICENSE"><img src="https://shields.io" alt="GPLv3"></a>
  <img src="https://shields.io" alt="iOS 17+">
  <img src="https://shields.io" alt="SwiftUI">
  <img src="https://shields.io" alt="Rust">
</p>

---

**TG WS Proxy iOS** runs the Rust version of TG WS Proxy on an iPhone and provides Telegram with a local MTProto endpoint:

```text
Telegram → 127.0.0.1:1443 → Rust TG WS Proxy → WSS / Cloudflare → Telegram DC
```

> [!CAUTION]
> **This is an experimental networking tool. It works, but an incorrect Packet Tunnel configuration can completely "kill" the internet connection on your device until you disable the VPN, reinstall the app, or reboot your iPhone. The application has not undergone a security audit. Use it entirely at your own risk and do not install IPAs from untrusted sources.**

---

## 🤖 AI Disclaimer
> [!NOTE]
> All build script fixes, Xcode 16.2+ compiler patches, iOS sandbox bypasses, and CI/CD automation setups in this fork were implemented in close collaboration with the **Gemini AI**. While every effort was made to achieve stability, the author is not responsible for any hidden bugs, Rust core memory leaks, or future breakages caused by Apple updates. Use at your own risk!

---

## ⚡ Fork Features (Build Fixes)
This repository fixes critical compilation errors found in the original project under recent Xcode versions (16.2+), removes the breaking `.glassEffect` UI modifier, and adds automated cloud build scripts via **GitHub Actions** without requiring a physical Mac computer.

---

## ✨ Features

- Local MTProto proxy powered by Rust;
- Cloudflare Workers, custom domain, and an updateable domain list;
- WebSocket pool sizes of `2`, `4`, or `6`;
- Traffic statistics, pool state, logs, and diagnostics;
- Optional Liquid Glass toggle;
- Live Activity and Dynamic Island bundled into a single `la` component;
- Interactive Home Screen Widget;
- System toggle for Control Center;
- App Intents and Siri Shortcuts;
- Deep links for starting, stopping, and configuring;
- RU/EN user interface;
- Automatic fallback to loopback mode if the Packet Tunnel is unavailable.

---

## 📦 Sideload Restrictions on a Free Apple ID (Important!)

When attempting to use this app with a free developer account (Free Apple ID) via `iloader` or `Sideloadly`, you will encounter the following iOS sandbox limitations:

1. **App ID Limit (0 available error):** Building a full version with all extensions enabled (`-c wd,la,cc,vpn`) requires registering multiple unique identifiers with Apple. Due to free account constraints, installation may fail. **Solution:** Use a brand-new, clean Apple ID.
2. **The "8-Second" Issue (VPN Drop):** If you compile the full version using the `vpn` flag, the app will launch successfully, but traffic will completely die after 8–30 seconds. iOS blocks network setting initialization (`NetworkExtension`) for free certificates and drops the socket. Continuous operation in VPN mode on a free account is **only possible by constantly restarting the app manually**.
3. **Recommended Stable Mode:** For a seamless experience without drops, compile the project with the **`-c la`** flag (Live Activity only) paired with the background audio player disguise patch (`audio`). Connect Telegram locally by manually pointing your proxy settings to **`127.0.0.1:1443`**.

---

## 🚀 Cloud Build (GitHub Actions)

You don't need a Mac or a local Xcode installation. Everything is built in the cloud:
1. Navigate to the **Actions** tab of your repository.
2. Select the **Build iOS IPA** workflow.
3. Click the **Run workflow** button.

You can customize the build flags inside `.github/workflows/build.yml`:
- `-c la` — Lightweight stable version featuring Live Activity (Recommended).
- `-c wd,la,cc,vpn` — Full ultimate version (Requires a paid developer account or TrollStore).

The compiled `.ipa` file will be available for download in the **Artifacts** section once the build successfully finishes.

---

## 🧬 Origins and Credits

- [Flowseal/tg-ws-proxy](https://github.com) — Original project and core concept;
- [amurcanov/tg-ws-proxy-android](https://github.com) — Rust core and Android fork used as upstream;
- [IMDelewer/tg-ws-proxy-ios](https://github.com) — Original iOS wrapper and Apple framework integration.

---

## 🔗 Deep links
```text
tgwsproxy://home
tgwsproxy://settings
tgwsproxy://?action=start
tgwsproxy://?action=stop
```
*(The full list of deep links is available in the original project documentation).*

---

## ⚖️ Licenses

- This combined project and all modifications are distributed under the [GPLv3](LICENSE) license.
- Telegram and Apple names are trademarks of their respective owners. This project is not affiliated with Telegram FZ-LLC or Apple Inc.

<p align="center"><sub>Workflow modification and bugfixes prepared by <a href="https://github.com">Adolfsmikler</a></sub></p>
