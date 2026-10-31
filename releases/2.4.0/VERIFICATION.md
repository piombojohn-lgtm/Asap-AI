# Asap Ai 2.4.0 installer verification

Verified October 30, 2026 on the development Windows PC using isolated application data and temporary project folders. Validation occurred before publication.

## Release artifact

- File: `AsapAi-2.4.0-Setup-x64.exe`
- Size: 180,069,531 bytes (about 180 MB / 172 MiB)
- SHA-256: `ae5e57825fb3ddae6d1ed6b0ec8f324e3adb51d6e4a1b29d676a542e22592273`
- Authenticode: **NotSigned**
- Payload: 126 inventoried application/runtime/license files; the installer also generates its ownership marker and uninstaller.

## Passed

- Native self-contained Windows publish and NSIS compilation.
- Fresh installation into a path containing spaces; all installed file lengths and SHA-256 hashes match the release inventory; Windows uninstall registration points to the correct directory.
- Update/reinstall of the same build preserves data and user-added files. Locked-file update and uninstall attempts abort before changing installed files; checksums are unchanged afterward.
- Successful uninstall removes package files and registration, while preserving added files and data outside the application directory. These lifecycle tests deliberately skip Start menu shortcut creation to leave the developer's shortcuts untouched.
- 24 checks against the actually installed payload: fresh per-user boot, generic profile, all seven plugins disabled/read-only, automatic memory off, model catalog, local memory-hook trust, terminal launch description, profile/project/chat persistence after process restarts, real project read/versioned save, stale-save rejection, filename/text search with matching line, and a real local Ollama response.
- The installed runtime works with only bundled Node and Windows directories on PATH. Existing developer settings/profile/memory/credential-metadata hashes remain unchanged.
- 17 data-root checks, 23 distribution-initialization checks, 13 native setup-state checks, and 67 backend/filesystem regression checks. Two junction tests initially required permissions unavailable inside the sandbox; both passed outside it. NuGet vulnerability lookup was unavailable during one native test build; compilation/tests still passed.
- Live native first-run guide displayed and acknowledged successfully. Its model refresh control and the persisted acknowledgment were exercised. Other workflows were checked through the installed backend and automated tests.
- Packaged model setup cancellation exits successfully without starting a download.
- Production allowlist and text scan exclude developer credentials, profiles, conversations, personal settings, model weights, logs, PDBs and development installation paths. Runtime and asset licenses are included.

## Limits

- This is not a clean virtual-machine or second-PC validation. Tests used the already installed Ollama service and existing local model weights. A fresh Ollama installation and the full approximately 13 GB download were not repeated.
- Optional online provider tools, provider sign-ins, plugin authorization and account-specific model access were not exercised. These require each recipient's own setup.
- Git and project language SDKs are separate dependencies. The private bundled Node runtime is for app helpers, not a general project SDK.
- The installer is unsigned. Windows may show unknown-publisher/SmartScreen warnings. No publisher certificate was purchased or configured.
- Updates are manual. The current release preserves user data on uninstall and does not remove Ollama or downloaded models.

This report describes the tested release artifact. It does not certify every hardware configuration, optional provider, or third-party service.
