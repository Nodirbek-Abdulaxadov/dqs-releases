# dqs-releases

Public download mirror for **DQS — Dental Queue System**. The source code lives in
the private `musanna-soft/dqs` repository; this repo only hosts release artifacts
so the [landing page](https://dqs.1kb.uz) can serve anonymous downloads via the
GitHub Releases API.

> **Do not commit code or large files here.** Only releases (artifacts) live in
> this repo. The git tree itself stays empty apart from this README.

## Asset naming convention

The landing page (`Landing/src/components/Downloads.tsx` in `dqs`) matches assets
by these regex patterns. **Stick to these names** or the download buttons will
fall back to "Coming soon".

| Component       | Filename pattern                          | Example                              |
| --------------- | ----------------------------------------- | ------------------------------------ |
| DQS Desktop     | `dqs-desktop-*.exe` / `*.msi` / `*.zip`   | `dqs-desktop-v0.1.0-beta.exe`        |
| PrinterExpert   | `printerexpert-*.exe` / `*.msi` / `*.zip` | `printerexpert-v0.1.0-beta.exe`      |
| DQS Dentist     | `dqs-dentist-*.apk` (or any `.apk`)       | `dqs-dentist-v0.1.0-beta.apk`        |

## Publishing a release

```bash
# 1. Build artifacts locally from the `dqs` repo
#    (Desktop: dotnet publish, PrinterExpert: dotnet publish,
#     Mobile:  dotnet publish -f net9.0-android)
# 2. Collect them into ./out/

gh release create v0.1.0-beta \
  --repo Nodirbek-Abdulaxadov/dqs-releases \
  --title "DQS v0.1.0-beta" \
  --notes "First public beta — Desktop, PrinterExpert and Dentist Android app." \
  ./out/dqs-desktop-v0.1.0-beta.exe \
  ./out/printerexpert-v0.1.0-beta.exe \
  ./out/dqs-dentist-v0.1.0-beta.apk
```

> **Important:** do **not** check the "Set as a pre-release" box. The landing
> calls `/releases/latest`, which skips pre-releases and returns 404 — every
> download button reverts to "Coming soon" until a non-prerelease exists.

## Versioning

Tags follow `vMAJOR.MINOR.PATCH[-suffix]`:

- `v0.1.0-beta` — current public beta
- `v1.0.0` — first stable
- Suffixes (`-beta`, `-rc.1`) are fine and still treated as the latest as long
  as the release is **not** marked as pre-release in the GitHub UI.
