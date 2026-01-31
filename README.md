
# RetroAchievements Library Validator (Cross-Platform Fork)

This project validates ROM files against the RetroAchievements by hashing local ROMs and comparing them to known hashes from the RetroAchievements API.

This fork focuses on **cross-platform compatibility**, allowing the script to run natively on **Linux, macOS, and Windows** without requiring Windows-only binaries or Wine.

---

## Key Features

- Cross-platform Powershell (Linux / macOS / Windows)
- Native MD5 hashing using 'Get-FileHash'
- Optional legacy support for 'RAHasher.exe'
- RetroAchievements API integration
- CSV exported of matched / unmatched ROMs
- Progress reporting per system and ROM

---

## Hashing Modes

This script supports **two hashing modes**, configurable via a toggle.

### Native MD5 Hashing (Default)

```powershell
$USE_NATIVE_HASHING = $true
```

- Uses PowerShell's built-in ```Get-FileHash```
- Fully cross-platform
- No external dependencies
- Fast and reliable
- Works well for most cartridge-based systems

Tested systems include:
- NES
- SNES
- Game Boy / GBC / GBA
- Nintendo 64
- GameCube
- PSP (ISO files)

> Note: Disc-based systems (e.g. PS1/PS2 BIN+CUE layouts) may require special handling

---

### Legacy RAHasher Mode (Windows Only)

```powershell
$USE_NATIVE_HASHING = $false
```

- Uses RAHASHER.exe
- Windows-only
- Requires the RAHasher binary to be present
- Included for backward compatibility

---

## Configuration

Edit the following variables at the top of the script:

```powershell
$ROM_BASE_PATH = ''
$RAHASHER_PATH = ''
$HASH_OUTPUT_PATH = ''
$RA_USERNAME = ''
$RA_API_KEY = ''
```

Map RetroAchievements system names to your local folder names in:

```powershell
$SYSTEM_TO_FOLDER_MAP = @{
    'NES/Famicom' = 'nes'
    'SNES/Super Famicom' = 'snes'
    'Game Boy' = 'gb'
}

---

## Running the Script

### Linux (Arch, Ubuntu, etc.)

```bash
yay -S powershell       # or distro equivalent
pwsh ./Get-RomHashes.ps1
```

### macOS

```bash
brew install powershell
pwsh ./Get-RomHashes.ps1
```

### Windows

```powershell
pwsh .\script.ps1
```

---

## Output

The script generates a CSV file. Columns include:
- MatchFound
- System
- RomName
- Hash
- Path
- RATitle
- RAID
- CheevoCount

---

## Notes on Accuracy

- RetroAchievements primarily uses MD5 hashes
- Native hashing matches RA for most cartridge-based systems
- Headered ROMs or multi-track disc images may not match
- Unmatched files are safely reported (not errors)

---

## Attribution

This is a fork of the original RetroAchievements Library Validator.
All original credit goes to the original author, Siallus

This fork focuses on:

- Removing Windows-only dependencies
- Improving portability
- Maintaining backward compatibility

---

Pull requests and suggestions welcome!
