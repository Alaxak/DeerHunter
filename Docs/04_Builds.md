# Builds

Unity build je **platformovo špecifický** a **deterministický** – exportuj z **Windows** pre Windows, z **macOS** pre macOS.
Build je dostupný na nasledujúcej URL:
https://alaxak.itch.io/deer-hunter

## Kde držať buildy

### Odporúčané: GitHub Releases ⭐
- **Výhody**: Čistá Git história, menšie clone (~100MB), user-friendly download
- **Proces**: Push tag → GitHub Workflow → automaticky exportuj build → Deploy na Releases
- **Storage**: GitHub poskytuje ~5GB zadarmo na Releases

### Alternatíva: `Builds/` v repo (cez Git LFS)
- **Výhody**: Všetko v jednom repo
- **Nevýhody**: Väčší repo size, LFS poplatky
- **Kedy**: Ak vieš čo robíš a máš Git LFS credit

## Naming konvencia
```
<GameName>_<platform>_v<VERSION>_<YYYY-MM-DD>.zip
```

**Príklady:**
- `DeerHunter_Windows_v0.1.0_2026-02-22.zip`
- `DeerHunter_WebGL_v0.1.0_2026-02-22.zip`
- `DeerHunter_macOS_v0.1.0_2026-02-22.zip`

## Build Process (Manual)

### Krok 1: Príprava
1. Spusti **Play Mode** v Unity a otestuj hru
2. Uprav verziu v `ProjectSettings/ProjectSettings.asset` alebo v `File → Build Settings`:
   - **Player Settings** → **Version**: `0.1.0`

### Krok 2: Build export

**File → Build Settings:**
1. Vyber platform (Windows PC / WebGL / macOS)
2. Klikni **Add Open Scenes** (aby sa **ver1.unity** priidal)
3. Nastavenia:
   - **Build Type**: Development (debug) alebo Release (optimized)
   - **Compression**: Optimal
   - **Scripting Backend**: IL2CPP (Windows) alebo Mono (WebGL)
4. Klikni **Build** alebo **Build and Run**
5. Vyber folder: `Builds/DeerHunter_Windows_v0.1.0/`
6. Počkaj na kompiláceu (~2-10 minút)

### Krok 3: Package do ZIP

**Automaticky (odporúčané):**
```powershell
# Windows PowerShell:
.\Tools\package_build_zip.ps1 -version 0.1.0 -platform Windows
```

**Manuálne:**
```powershell
# Vytvor BuildInfo.txt
$buildInfo = @"
Game: DeerHunter
Version: 0.1.0
Platform: Windows
Build Date: $(Get-Date -Format 'yyyy-MM-dd HH:mm:ss')
Commit: $(git rev-parse --short HEAD)
Branch: $(git rev-parse --abbrev-ref HEAD)
"@

$buildInfo | Out-File -FilePath "Builds/DeerHunter_Windows_v0.1.0/BuildInfo.txt"

# ZIP-uj
Compress-Archive -Path "Builds/DeerHunter_Windows_v0.1.0" `
                 -DestinationPath "Builds/DeerHunter_Windows_v0.1.0_$(Get-Date -Format 'yyyy-MM-dd').zip"
```

**Linux/macOS (bash):**
```bash
./Tools/package_build_zip.sh -v 0.1.0 -p macOS
```

## ZIP Contents

```
DeerHunter_Windows_v0.1.0_2026-02-22.zip
├── DeerHunter.exe               # Main executable
├── DeerHunter_Data/
│   ├── Plugins/                 # DLL dependencies
│   ├── Resources/               # Bundled assets
│   ├── Scenes/                  # Scene data
│   ├── Managed/                 # .NET assemblies
│   └── StreamingAssets/         # Custom data
├── MonoBleedingEdge/            # C# runtime (ak Mono)
├── IL2CPP-Data/                 # Compiled scripts (ak IL2CPP)
├── BuildInfo.txt                # Metainformácie
├── README.txt                   # Quick start (optional)
└── INSTALL_NOTES.txt            # Systémové požiadavky (optional)
```

### BuildInfo.txt template
```
════════════════════════════════════════
            DeerHunter Build Info
════════════════════════════════════════

Version:      v0.1.0
Build Date:   2026-02-22 14:30:00 UTC
Platform:     Windows 64-bit
Engine:       Unity 2022.3 LTS
Commit:       abc1234
Branch:       main

System Requirements:
  - Windows 7 / 10 / 11 (64-bit)
  - 4 GB RAM minimum
  - GPU with DirectX 11 support
  - 500 MB free disk space

How to Play:
  1. Extract all files to a folder
  2. Run DeerHunter.exe
  3. Press Play in menu

Known Issues:
  - None reported for v0.1.0

════════════════════════════════════════
```

## Nasadenie na GitHub Releases (Manual)

### Krok 1: Tag verzia
```bash
git tag -a v0.1.0 -m "Release v0.1.0: Core gameplay"
git push origin v0.1.0
```

### Krok 2: Vytvor Release na GitHub
1. Choď na https://github.com/YourName/DeerHunter/releases
2. Klikni **Draft a new release**
3. Vyber tag: `v0.1.0`
4. **Title**: `v0.1.0 - Core Gameplay Release`
5. **Description**:
   ```markdown
   ## What's new
   - Full player controller (WASD + Mouse)
   - Enemy AI (basic chase)
   - Shooting and reloading
   - Day/Night cycle
   - Door teleportation
   
   ## Downloads
   - Windows x64
   - WebGL (experimental)
   
   ## Known Issues
   - Save/Load not implemented
   - Only 1 day cycle
   
   ## Credits
   Built with Unity 2022.3 LTS
   ```
6. **Attach files**: Drag & drop `DeerHunter_Windows_v0.1.0_2026-02-22.zip`
7. Klikni **Publish release**

## CI/CD (GitHub Workflow) – Future

**Príklad automatických builds na git push:**

`.github/workflows/build.yml`
```yaml
name: Build & Release

on:
  push:
    tags:
      - 'v*'

jobs:
  build-windows:
    runs-on: windows-latest
    steps:
      - uses: actions/checkout@v3
      - uses: unity-actions/activate@v2
      - uses: unity-actions/test@v4
      - uses: unity-actions/build-windows@v4
        with:
          unityVersion: 2022.3.0f1
      - uses: softprops/action-gh-release@v1
        with:
          files: build/*.zip
```

To automaticky exportuje build a uploaduje ZIP na Releases.

## Troubleshooting

### Build je príliš veľký (>1GB)
- Vrátaš sa na **Build Settings** a vyber **Compression**
- Alebo znížaš texture resolution či audio bitrate
- Alebo zapneš **Strip Engine Code** (iba release builds)

### Hra nefunguje po export-e
1. Skúšaj v **Development** build (lepšie error messages)
2. Klikni na .exe + check console logy (`DeerHunter_Data/output_log.txt`)
3. Overi, že sú všetci Dependencies (DLL) v zipe

### Git LFS tracking objem
```bash
git lfs ls-files | sort -k4 -rh | head -10  # Top 10 largest files
```
