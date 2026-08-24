<div align="center">

# Splitter Studio

**Professional tiled printing for oversized images — a native Windows application.**

Turn a 36 × 48 inch poster into twelve perfectly calculated A3 sheets, print them
at 100 % scale on the printer you already own, and assemble a seamless full-size print.

[![Windows 10|11](https://img.shields.io/badge/Windows-10%2019041%2B%20%7C%2011-0078d4?logo=windows11&logoColor=white)](#requirements)
[![.NET 10](https://img.shields.io/badge/.NET-10-512bd4?logo=dotnet&logoColor=white)](#building-from-source)
[![WinUI 3](https://img.shields.io/badge/UI-WinUI%203%20·%20Windows%20App%20SDK-0078d4)](#architecture)
[![Tests](https://img.shields.io/badge/tests-105%20passing-2ea44f)](#verified-by-tests)
[![v1.0.0](https://img.shields.io/badge/release-v1.0.0-orange)](#download)
[![VirusTotal](https://img.shields.io/badge/VirusTotal-checksum-54a943?logo=virustotal&logoColor=white)](SECURITY.md)

**[Download the installer](https://splitterstudio.mobi24.in/download)** · [Documentation](https://splitterstudio.mobi24.in/docs) · [Report an issue](../../issues)

</div>

---

![Splitter Studio application screenshot](screenshots/app-screenshot.png)

## Why

Every printer has a maximum paper size. Your artwork doesn't.

Splitter Studio divides oversized images into **exactly calculated tiles** — A0 through A5,
Letter, Legal, Tabloid, Ledger or custom sheets — with the margins, overlap, bleed, crop
marks and labels needed to assemble a physically accurate poster at full size. It is a
real native Windows desktop application (WinUI 3 / .NET 10): no browser, no localhost
server, no Python, no Docker, no telemetry. Your images never leave your computer.

## Highlights

| | |
|---|---|
| **Exact tile mathematics** | Every tile is an integer-exact pixel region. Adjacent tiles share boundaries with no missing or duplicated pixels — verified by automated reconstruction tests. |
| **Two planning modes** | Enter the final poster size and the sheet grid is derived for you, or lay out a manual rows × columns grid. |
| **Recommended layouts** | Practical grid options ranked by sheet count and paper waste, one click to apply. |
| **Live preview** | Zoomable tile grid with overlap strips highlighted, tile labels, and hover inspection of exact pixel regions. |
| **Print-shop output** | PNG / JPEG / TIFF tiles, ZIP packaging with contact sheet, assembly map and a print-instructions PDF. |
| **Honest printing** | Tiles print at 100 % scale through the real Windows print system. Status comes from the spooler — submitted, spooling, printing, completed, failed, unknown. The app never claims a sheet printed when it cannot know. |
| **Projects** | Versioned `.splitterproject` files store the complete configuration; reopen and regenerate anytime. |
| **Local-first** | Fully offline. No account, no upload step, no analytics. |

## The quality guarantee

```
ORIGINAL SOURCE  →  EXACT TILE EXTRACTION  →  LOSSLESS / USER-SELECTED EXPORT
```

- The preview is a low-resolution proxy for the UI **only** — exports are always
  extracted from the original file, never from the preview.
- The original image is never modified, re-encoded or replaced.
- If your source resolution is below the requested DPI, Splitter Studio warns you
  instead of silently upscaling.
- Physical math uses exact decimal arithmetic end-to-end (mm ⇄ inch ⇄ pixels ⇄ DPI).

### Verified by tests

The test suite (105 tests) includes **raster reconstruction**: tiles are reassembled
and compared against the original — dimensions and pixel data must match **exactly**
when overlap is disabled, across grid shapes, non-divisible dimensions and multiple
DPI values. Physical-dimension tests verify the full chain
*pixels → DPI → paper → printable area → tile size* to sub-pixel tolerance.

## Download

Grab the installer from the official site:

**https://splitterstudio.mobi24.in/download**

Verify it before running (expected on first launch — see [SECURITY.md](SECURITY.md)):

```
SHA-256: 4d468e6d545234d4e6c32643f27a8d87a690aaab51d057fd3ec999e6b8a97149
```

## Requirements

- Windows 10 (version 2004 / 19041 or newer) or Windows 11, 64-bit
- ~300 MB disk space + space for your generated tiles
- No runtime prerequisites — .NET 10 and the Windows App SDK ship inside the installer

## Building from source

Requires the .NET 10 SDK.

```powershell
git clone <this repository>
cd splitter-studio
dotnet build Splitter.sln -c Release
dotnet test  Splitter.sln
dotnet run --project src/SplitterStudio.App
```

Publish a self-contained build (no runtime needed on target machines):

```powershell
dotnet publish src/SplitterStudio.App -c Release -r win-x64 --self-contained true -p:Platform=x64 -o artifacts/publish
```

## Architecture

```
┌────────────────────────────────────────────────────┐
│  SplitterStudio.App (WinUI 3 · Win2D preview)      │
├────────────────────────────────────────────────────┤
│  SplitterStudio.Application (service contracts)    │
├──────────────────┬─────────────────────────────────┤
│  Domain          │  Infrastructure                 │
│  · Length/DPI    │  · libvips imaging (NetVips)    │
│  · Paper catalog │  · GDI+ sheet composer          │
│  · Tiling engine │  · ZIP / PDF / contact sheet    │
│  · Calculator    │  · winspool print service       │
│  · Optimizer     │  · JSON projects + Serilog      │
└──────────────────┴─────────────────────────────────┘
```

- **Domain** is dependency-free: pure decimal/integer math, fully unit-testable.
- **Infrastructure** wraps libvips (streaming region extraction — huge images never
  get fully duplicated in memory), GDI+ for mark composition, and winspool.drv
  for honest print-queue status.
- **App** is the WinUI 3 presentation layer with a Win2D-powered preview canvas.

## Roadmap

- [ ] Code-signed installer (removes the SmartScreen prompt)
- [ ] Automatic update channel
- [ ] Batch processing of multiple images
- [ ] Seam close-up preview mode
- [ ] Additional installer locales

## Support & feedback

- Problems or ideas → [open an issue](../../issues/new/choose)
- Direct contact → **support@mobi24.in**
- Full documentation → https://splitterstudio.mobi24.in/docs

## License

Proprietary — © 2026 Splitter Software. The installer may be freely downloaded and
used; redistribution of modified builds is not permitted. The issue tracker is open
to everyone.

<div align="center">
<sub>Built with C#, .NET 10, WinUI 3, libvips, Win2D and PDFsharp.</sub>
</div>
