# Mobile Hacking from Zero

A hands-on Android app security series that starts from nothing and builds the whole
skill set one lesson at a time — from *"how do I even get an APK?"* to bypassing SSL
pinning and writing a professional report.

Each lesson is a standalone writeup. Lessons that teach a technique you can only
practice against a running target ship with a deliberately vulnerable **challenge app**
in the [Challenge Lab](#challenge-lab).

> **Scope & ethics.** Everything here uses apps built for training or that you own.
> Only ever reverse engineer or test an app you own or have written authorization to test.

---

## Field Notes — the lessons

Foundations first (how to acquire and read an app), then static techniques, then dynamic ones.

| # | Lesson | Type | Status |
|---|--------|------|--------|
| 00 | Setup & scope — the lab and toolchain | foundations | planned |
| 01 | [Getting the app](writeups/01-getting-the-app.md) | foundations | **published** |
| 02 | The manifest | foundations | planned |
| 03 | The code (jadx) | foundations | planned |
| 04 | Resources & assets | foundations | planned |
| 05 | Native libraries (Ghidra) | static | planned |
| 06 | Local storage (/data/data) | dynamic | planned |
| 07 | SSL pinning bypass | dynamic | planned |
| 08 | Root & debugger detection bypass | dynamic | planned |
| 09 | Runtime hooking with Frida | dynamic | planned |
| 10 | Automated triage (MobSF, apkleaks) | recon | planned |
| 11 | Writing the report | reporting | planned |

## Challenge Lab

Deliberately vulnerable practice apps — one per technique that needs a target. Static ones
are solved by reading the file; dynamic ones need the app running with Frida or Burp.
**APKs are published on this repo's [Releases](../../releases) page**, not in the source tree.

| App | Type | Teaches | Pairs with |
|-----|------|---------|------------|
| LeakyLogin | static | hardcoded secrets, base64, SQLite | Lesson 03–04 |
| NativeSafe | static | a secret hidden in a native `.so` | Lesson 05 |
| FireLeak | recon | leaked backend keys & cloud misconfig | Lesson 10 |
| VaultDB | dynamic | insecure local storage | Lesson 06 |
| PinnedApp | dynamic | SSL pinning to bypass | Lesson 07 |
| RootCheck | dynamic | root/debugger detection to defeat | Lesson 08 |
| HookMe | dynamic | a function to hook with Frida | Lesson 09 |

## How to use this repo

1. Read a lesson in [`writeups/`](writeups/).
2. If it has a challenge app, download the APK from [Releases](../../releases).
3. Work it yourself first; the writeup is the walkthrough.

## Author

Mbongeni Moyo — mobile & application security research.

## License

Writeups: CC BY 4.0. Challenge app source: MIT. See [LICENSE](LICENSE).
