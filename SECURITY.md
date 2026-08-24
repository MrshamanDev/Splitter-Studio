# Security policy

## Verifying the installer

Every official build's SHA-256 checksum is published before release. Verify your
downloaded `SplitterStudio-Setup-1.0.0.exe` before running it:

```powershell
Get-FileHash .\SplitterStudio-Setup-1.0.0.exe -Algorithm SHA256
```

Expected value for **v1.0.0**:

```
4d468e6d545234d4e6c32643f27a8d87a690aaab51d057fd3ec999e6b8a97149
```

Public multi-engine scan report:

https://www.virustotal.com/gui/file/4d468e6d545234d4e6c32643f27a8d87a690aaab51d057fd3ec999e6b8a97149/detection

Only download the installer from the official site:
**https://splitterstudio.mobi24.in/download**

If the checksum of your copy differs from the value above, do not run it.

## Why SmartScreen appears

The installer is not code-signed yet, so Microsoft Defender SmartScreen shows a
"Windows protected your PC" prompt. Click **More info** → **Run anyway** after
verifying the checksum. Signing is on the roadmap and will remove this prompt.

## Reporting a vulnerability

Please report security issues privately rather than opening a public issue:

**support@mobi24.in** (subject: `Security`)

Include the version, reproduction steps and any relevant logs
(`%LOCALAPPDATA%\SplitterStudio\logs`). Reports are handled seriously; you will
receive a response, and credit is given in release notes if you wish.
