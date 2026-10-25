# Android_Ghosts Tunnels

An experimental ARM64 Android tunnel client branded **Android_Ghosts**. This branch assembles the project from the checked-in source archive and applies the UI/core patches in `.github/workflows/build-arm64.yml`.

## Build and download

1. Open [GitHub Actions builds](https://github.com/AndroidGhosts/Ghosts_-tunnels/actions).
2. Select the latest successful **Build Android_Ghosts Tunnels ARM64 APK** run on `android-ghosts/ui-build-preview`.
3. Under **Artifacts**, download `Android_Ghosts-Tunnels-ARM64-debug-APK` and extract the APK.

The output is an **ARM64 debug APK** (`app-arm64-v8a-debug.apk`) signed with the Android debug key. It is for device testing, not a Play Store release. A release build still needs production signing and release validation.

## Current implementation and validation

- **DNSTT core:** included in the native Go/AAR build. CI proves compilation and packaging only; it does not prove a successful connection to a real DNS tunnel server.
- **Hysteria 2:** its Go packages are included in the current native build. End-to-end connection, traffic routing and reconnection need tests against a real Hysteria 2 server.
- **Hysteria 1:** currently **not enabled in the CI build**. The legacy dependency graph does not compile reliably alongside the current Go/QUIC dependencies. Do not treat a visible selector or profile field as a working Hysteria 1 engine.
- **OpenVPN:** requires separate verification of the Android VPN service, `.ovpn` import/authentication, route/DNS handling and a real server connection. A successful APK build alone is not proof that these functions work.

## Size and release notes

The last verified baseline APK was approximately **23.4 MB**. The workflow is testing compressed native-library packaging to reduce download size without removing protocol libraries. The requested **under-10-MB target is not yet verified**.

Before calling this a complete VPN client, test each supported engine on a device with valid server credentials and confirm connection/disconnection, DNS resolution, IPv4/IPv6 routing, traffic counters, reconnection and disconnect cleanup. Do not put private keys, passwords or server credentials in commits or build logs.

Project: [AndroidGhosts/Ghosts_-tunnels](https://github.com/AndroidGhosts/Ghosts_-tunnels)  
Telegram: [Android_Ghosts](https://t.me/Android_Ghosts)
