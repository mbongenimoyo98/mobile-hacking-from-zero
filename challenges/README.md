# Challenge Lab

Source for the deliberately vulnerable practice apps. Built APKs are attached to this
repo's **Releases**, so you can download and analyze them without building anything.

Each challenge folder (added as we build them) contains:

- `README.md` — what it teaches and the ground rules (no spoilers)
- the app source
- a `SOLUTION.md` — the full walkthrough (don't open until you've tried it)

| App | Type | Teaches |
|-----|------|---------|
| leakylogin | static | hardcoded secrets, base64, SQLite |
| nativesafe | static | a secret in a native `.so` |
| fireleak | recon | leaked backend keys & cloud misconfig |
| vaultdb | dynamic | insecure local storage |
| pinnedapp | dynamic | SSL pinning |
| rootcheck | dynamic | root/debugger detection |
| hookme | dynamic | a function to hook with Frida |

**Warning:** these apps are intentionally insecure. Install them only on a throwaway
emulator or test device, never on a phone with real data.
