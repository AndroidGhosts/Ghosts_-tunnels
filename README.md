# Android_Ghosts Tunnels

Experimental Android tunnel client branded **Android_Ghosts**. The GitHub Actions workflow builds the Android app from the checked-in source archive and applies the UI/core integration patches. The workflow now requests native Go bindings for ARM64, ARMv7, x86_64 and x86, and checks that all four native library folders are present in the APK before publishing artifacts. Treat multi-ABI support as unverified until that workflow passes.

## Build status

The previous verified artifact is an ARM64-only debug APK from [GitHub Actions run #40217237989](https://github.com/AndroidGhosts/Ghosts_-tunnels/actions/runs/40217237989), 10,351,401 bytes (9.87 MiB), SHA-256 `bdce55eee5ae8ab8eb5fafec868a2bbe9f2d7a7d7b6c94f85c024116ae069808`. A workflow update now requests all four Android ABIs and fails the build if any native ABI is absent. Do not treat that as verified until the new run succeeds.

All APKs produced by this workflow are **debug builds signed with the Android debug key**, intended for device testing, not Play Store release. Release signing and real-device testing with server credentials are still required.

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
