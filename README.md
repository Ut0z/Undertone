<p align="center"><img src="src/main/resources/assets/spotifyglass/icon.png" width="128" alt="Undertone icon"></p>

# Undertone

A compact music HUD for **Minecraft Java 1.21.8 on Windows 10/11**, built with Fabric. See your current track, colorful artwork, progress and available lyrics without leaving the game.

## Features

- Works with Windows media sessions from desktop players and supported browser websites, including Spotify and SoundCloud when they publish media metadata.
- Smooth text, rounded corners and an adjustable monochrome background. Album artwork stays in color.
- Available synced lyrics scroll smoothly. Timed instrumental gaps can show three softly pulsing dots.
- HUD size stays independent of Minecraft's GUI scale.
- Drag the visible HUD with the left mouse button in the Escape menu, Minecraft Options or Undertone settings. Release to save its position.
- Mod Menu sliders for size, corner radius, background opacity and position, plus HUD/lyrics toggles.

## Requirements and installation

| Requirement | Version |
| --- | --- |
| Minecraft Java | 1.21.8 |
| Platform | Windows 10/11 |
| Java | 21 |
| Loader | Fabric Loader 0.16.14 or newer |
| Required mod | [Fabric API for 1.21.8](https://modrinth.com/mod/fabric-api/versions?g=1.21.8) |
| Recommended mod | [Mod Menu for 1.21.8](https://modrinth.com/mod/modmenu/versions?g=1.21.8) |

1. Install Fabric for Minecraft 1.21.8.
2. Put the Undertone JAR and Fabric API in your instance's `mods` folder. Add Mod Menu to access the settings screen.
3. Remove previous Undertone/Spotify Glass JARs before updating; install only one version.
4. Start music in a compatible app or browser, then enter a world.
5. Open **Mods → Undertone → Configure** to adjust the HUD.

The internal mod ID remains `spotifyglass` so existing settings continue to work. The current version is **1.5.1**. This repository does not contain the withdrawn AI-lyrics experiment.

## Player and lyrics limitations

Windows must expose the player as a media session. Website/browser support and the supplied title, artist, cover and timeline vary. The HUD may identify the browser rather than the website. Playing sessions take priority over paused sessions; Windows' current session breaks ties. Browser videos can also appear.

No lyrics match means the lyrics area is hidden. Plain lyrics without timestamps are displayed but are not accurately synchronized. Timed empty lines or music markers are required to detect instrumental gaps; the mod does not listen to or analyze audio. Long text is shortened to fit. No blur effect is included.

## Privacy

**Lyrics are enabled by default.** To find lyrics, Undertone sends the track title, artist and available album/duration to [LRCLIB](https://lrclib.net) over HTTPS. The service also receives ordinary connection information such as the requesting IP address. Turn **Lyrics: OFF** to stop new requests; an in-flight request may finish.

Player metadata and artwork are read locally through Windows. No microphone capture, system-audio recording, AI API, account login, telemetry or analytics service is included. The Windows bridge runs a hidden PowerShell helper with process-local `ExecutionPolicy Bypass`; it does not change the system's execution policy. See [PRIVACY.md](PRIVACY.md).

## Build from source

Install JDK 21, then run:

```powershell
.\gradlew.bat build
```

On a Unix build machine, use `sh ./gradlew build`. Build output is in `build/libs/`; install the JAR without `-sources`. Running the media integration requires Windows even if compilation succeeds elsewhere. First build downloads Gradle and dependencies.

To launch a development client on Windows:

```powershell
.\gradlew.bat runClient
```

The development instance lives in the ignored `run/` directory. Do not commit it.

## Validation and contributing

Eight Java tests cover lyric parsing/timing and animation sizing/timing. Eight Windows PowerShell checks cover player selection and labels:

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File src/test/powershell/MediaSelection.Tests.ps1
```

The build passes locally. A Windows probe detected a browser session with artwork. This is not a guarantee of compatibility with every player; HUD dragging has not yet received an interactive in-game verification. See [CONTRIBUTING.md](CONTRIBUTING.md), [CHANGELOG.md](CHANGELOG.md) and [SECURITY.md](SECURITY.md).

## License, credits and creation disclosure

Source code is available under the [MIT license](LICENSE). This project was developed substantially with generative-AI assistance; the icon was generated with AI. Documentation was also AI-assisted. This describes how the project was created, **not an AI feature in the mod**. See [CREDITS.md](CREDITS.md).

Independent project. Not affiliated with or endorsed by Mojang, Microsoft, Spotify, SoundCloud, Fabric, Modrinth or LRCLIB.
