# Publishing & promoting the GitHub repository

This folder is a ready-to-push **landing repository** for Splitter Studio:
README, security notes, contributing guide and issue templates. It gives the
product a credible GitHub presence for stars, feedback and discoverability.

## 1. Create the repository

1. GitHub → New repository → name: `splitter-studio` (public)
2. Description: `Professional tiled printing for oversized images — native Windows app (C# / .NET 10 / WinUI 3). Print huge posters on any printer at 100% scale.`
3. Do **not** initialize with a README (this folder already has one).

## 2. Push

```powershell
cd github-public
git init -b main
git add .
git commit -m "Splitter Studio — official repository"
git remote add origin https://github.com/<your-user>/splitter-studio.git
git push -u origin main
```

## 3. Repository settings that earn stars

- **About panel**: tick *Releases* + *Issues*; website: `https://splitterstudio.mobi24.in`
- **Topics**: `csharp`, `dotnet`, `winui3`, `windows`, `printing`, `poster`,
  `tiling`, `large-format`, `print-preparation`, `libvips`
- **Releases**: create `v1.0.0`, attach `SplitterStudio-Setup-1.0.0.exe` and paste
  the SHA-256 from SECURITY.md into the release notes (GitHub shows download counts —
  social proof).
- **Social preview**: upload `screenshots/app-screenshot.png` (Settings → General).

## 4. Promotion checklist

- [ ] Show HN: "Show HN: I built a native Windows app that prints huge posters on any printer"
- [ ] r/software, r/windowsapps, r/photography, r/AnalogCommunity? (pick 2–3 relevant subs; read rules first)
- [ ] X/Twitter thread with the screenshot + a short screen recording
- [ ] LinkedIn post (print/design/architecture audiences)
- [ ] dev.to / CodeProject write-up: "The math behind tiling a 36×48in poster" —
      engineers star repos that teach something
- [ ] Add the GitHub link to the website footer and the app's About area

## 5. Later: open the source?

Opening `src/` (MIT or GPL) typically multiplies stars and contributions. The
architecture is already clean-layered for public consumption. If you do:
push the full solution next to this README, keep `installer/` and signing keys
private, and replace the License section of README.md accordingly.
