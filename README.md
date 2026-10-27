# DevWS Scoop bucket

First-party [Scoop](https://scoop.sh/) bucket for [DevWS](https://github.com/ekinokss/DevWS),
a configuration-driven workspace orchestrator for Windows.

## Install

Run Scoop from an **elevated PowerShell** under the same Windows account that should own
DevWS:

```powershell
scoop bucket add ekinokss https://github.com/ekinokss/scoop-bucket
scoop install ekinokss/devws
```

The `scoop bucket add` command requires Git. If Scoop reports that Git is required, run
`scoop install git` first.

The current package is DevWS `0.2.0`, installed from the official immutable GitHub Release:

- https://github.com/ekinokss/DevWS/releases/tag/v0.2.0
- `DevWS-Setup.exe` SHA-256:
  `7a87e08bb4b5d802ed3f2cd7566a73242c07965aadae7f003a384e5eaa597dce`

## Update

```powershell
scoop update devws
```

Scoop updates re-run the DevWS setup as an upgrade or same-version repair. The Scoop
uninstaller hook is deliberately skipped during updates, so an update does not perform a
full DevWS uninstall before installing the newer package. Configuration and state are
preserved.

## Uninstall

```powershell
scoop uninstall devws
```

Uninstall uses the protected DevWS setup registered for the current Windows account, not the
temporary Scoop-downloaded installer. It removes DevWS runtime resources and scheduled tasks
while preserving the canonical workspace configuration, state, backups, legacy `.ws` data,
and unrelated integrations. AutoHotkey is not removed.

## Requirements

- Windows 11 x64.
- PowerShell 7 or newer.
- A genuine stable Windows Terminal installation.
- Administrator rights under the same Windows account that should own DevWS.
- A trusted machine-wide AutoHotkey v2 installation, or WinGet/App Installer and network
  access so the DevWS setup can acquire one.

## Elevation and identity

Run Scoop elevated under the account that should own DevWS. DevWS intentionally rejects UAC
elevation that switches to a different Windows account. A standard user must not use another
administrator's credentials and then treat the result as an installation for the original
standard user.

The elevated invocation used by this bucket is the validated path. A non-elevated Scoop
invocation relies on DevWS's own UAC prompt and is not validated for this bucket; treat that
invocation as experimental.

## Unsigned executable

The DevWS executable is unsigned. Microsoft Defender SmartScreen may warn about a downloaded
executable. Install only from the official GitHub Release URL above and verify the published
SHA-256. The Scoop manifest also verifies the hash before running the installer.

## Scope

This repository contains only the Scoop manifest and documentation. It does not contain
DevWS binaries, copies of release assets, or AutoHotkey packages. DevWS handles its own
machine-wide AutoHotkey prerequisite.

## License

The DevWS project is MIT-licensed. See the
[DevWS license](https://github.com/ekinokss/DevWS/blob/main/LICENSE).
