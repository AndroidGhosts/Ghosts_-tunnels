# Android_Ghosts Tunnels

Experimental ARM64 Android tunnel client branded **Android_Ghosts**. The build assembles the checked-in Android source archive and applies the UI/core integration patches from `.github/workflows/build-arm64.yml`.

## Latest verified build

- Build: [GitHub Actions run #40217237989](https://github.com/AndroidGhosts/Ghosts_-tunnels/actions/runs/40217237989)
- Artifact: `Android_Ghosts-Tunnels-ARM64-debug-APK`
- APK: `app-arm64-v8a-debug.apk`
- Size: **10,351,401 bytes (9.87 MiB)** — below 10 MiB, but slightly above 10,000,000 decimal bytes.
- SHA-256: `bdce55eee5ae8ab8eb5fafec868a2bbe9f2d7a7d7b6c94f85c024116ae069808`

The APK is a **debug build signed with the Android debug key**, intended for device testing. It is not a Play Store release. Production release signing, release validation, and a test on a real device with server credentials are still required.

## Engine status

- **DNSTT:** the existing Go client is included and builds. Compilation does not prove a successful connection to a real DNSTT server.
- **Hysteria 2:** the official Hysteria 2 core client is linked into the native Go library. The profile supports server/authentication/TLS SNI, optional Salamander obfuscation, bandwidth caps, per-profile DNS upstream/cache controls, and IPv6 policy. End-to-end server connectivity and routing still need device testing.
- **Hysteria 1:** **not enabled**. Its profile editor and URI import are present, but the legacy QUIC dependency graph did not compile reliably with the current Go dependencies. The UI intentionally blocks connection rather than claiming this engine works.
- **OpenVPN:** **not enabled**. The profile editor and `.ovpn` text/import are present, but OpenVPN 3/JNI engine integration and VPN-service handoff have not been completed. The UI intentionally blocks connection.

Multi-profile aggregation is DNSTT-only in this preview. Do not interpret protocol selectors or profile fields as proof of a working engine.

## Validation still required

Before treating this app as a production VPN client, test on an Android device with valid server credentials: connect/disconnect, IPv4 and IPv6 routes, DNS resolution, UDP and TCP traffic, traffic counters, reconnection, VPN permission handling, and clean shutdown. Hysteria 1 and OpenVPN must not be marked ready until their engines are genuinely integrated and tested. Keep server passwords, private keys, and credentials out of commits and build logs.

Project: [AndroidGhosts/Ghosts_-tunnels](https://github.com/AndroidGhosts/Ghosts_-tunnels)  
Telegram: [Android_Ghosts](https://t.me/Android_Ghosts)
