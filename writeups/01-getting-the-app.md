# Stage 1 — Getting the App

*Mobile Hacking from Zero · the first lesson*

This is the first in a hands-on series on taking Android apps apart to find security
problems. It starts from zero — no prior reverse-engineering experience assumed — and
builds one stage at a time until you can go from *"here's an app"* to a finished report.

The whole series is **static-first**: we learn as much as possible by reading the app's
file *at rest*, before ever running it. That turns out to be most of the work, and it's
the safest place to start.

**Stage 1 has one job:** get the app's file onto your computer and open it up. By the end
you'll be able to acquire an app two different ways, unpack it, and recognize every part
inside.

> **Scope and ethics (read this once).** Only ever do this to apps you own, apps built for
> training, or apps you have explicit written authorization to test. Reverse engineering
> someone else's app without permission can be illegal.

## What you're getting

An Android app ships as a single file called an **APK** (Android Package). Despite the
name, an APK is just a **ZIP archive** with a `.apk` extension. Inside it is everything the
app needs: its compiled code, images and text, settings, and signature.

That's the key insight the whole series hangs on: because an APK is a zip, you can **unzip
it and read what's inside** without running anything.

So Stage 1 is two moves:

1. Get the APK onto your computer.
2. Unzip it so you can see its contents.

## Route A — download a prebuilt APK

The easy route, used for training apps and CTF challenges. The APK is handed to you
directly — usually a project's GitHub **Releases** page.

```bash
cd ~/Downloads
ls -lh *.apk          # confirm the file & its name
```

## Route B — pull it from a device

The real-world way. The tool is **adb** (Android Debug Bridge), which runs on *your
computer* and talks to a connected device or emulator.

> **Watch your prompt.** `adb` lives on your computer, not the phone. Run `adb` commands
> from your terminal. When a command puts you *inside* the device (the prompt changes to
> something like `emu64xa:/ $`), drop the `adb shell` part.

**1. Find the package name** (apps are identified by `com.example.app`, not their display name):

```bash
adb shell pm list packages | grep -i <keyword>
```

**2. Find where the APK lives on the device:**

```bash
adb shell pm path <package.name>
```

It prints something like `package:/data/app/~~aBcD==/<pkg>-xyz==/base.apk`. The part after
`package:` is the path. Copy it exactly — those random folder names change every install.

**3. Copy it to your computer** (quote the path; the last word is the name it's saved as):

```bash
adb pull "/data/app/~~aBcD==/<pkg>-xyz==/base.apk" app.apk
pwd ; ls -lh *.apk
```

## Unzip it

An APK is a zip — so unzip it into its **own clean folder**, never your home directory.

```bash
mkdir app_extracted
cd app_extracted
unzip ~/Downloads/<your-app>.apk
ls -la
```

## First look — the anatomy of an APK

You don't analyze anything yet — the goal is to **recognize the pieces**.

| Part | What it is | Covered in |
|------|------------|-----------|
| `AndroidManifest.xml` | The app's blueprint: components, permissions, settings | Stage 2 |
| `classes.dex` | The app's compiled code (there may be several) | Stage 3 |
| `resources.arsc` + `res/` | Compiled resources: strings, images, layouts | Stage 4 |
| `assets/` | Raw bundled files: config, data, hidden things | Stage 4 |
| `lib/` | Native code libraries (`.so`, compiled C/C++) | Stage 5 |
| `META-INF/` | The app's digital signature | (signing) |

Two things to notice already: how many `classes*.dex` files there are and whether `lib/`
exists (native code), and what's in `assets/` (a `flutter_assets/` folder means a Flutter
app; an oversized file is always worth a second look).

## Recap & what's next

You can now acquire an app two ways, unzip it into a clean folder, and name every part
inside. You haven't "hacked" anything yet — you've opened the box. But every finding in
this series comes from reading one of these pieces.

**Stage 2 — The manifest.** We start reading, with the single best first file to open.

## Appendix — commands used

```bash
# Route A: a downloaded APK
cd ~/Downloads
ls -lh *.apk

# Route B: pull from a device
adb shell pm list packages | grep -i <keyword>
adb shell pm path <package.name>
adb pull "<the-path-it-printed>" app.apk
pwd ; ls -lh *.apk

# Unpack (both routes)
mkdir app_extracted && cd app_extracted
unzip ~/Downloads/<your-app>.apk
ls -la
```
