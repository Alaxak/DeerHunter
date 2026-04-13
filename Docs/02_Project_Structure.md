# Project Structure

## Root priečinok
```
DeerHunter/
├── .editorconfig            # Editor nastavenia
├── .github/                 # GitHub workflows (CI/CD)
├── .gitignore               # Git ignore (cache, build, library)
├── Builds/                  # Exportované buildy (.zip)
├── CodeDocs/                # Technická dokumentácia a zdrojové dáta
├── Design/                  # Game Design Document
├── Docs/                    # Projektová dokumentácia
├── LICENSE                  # Licencia projektu
├── Presentation/            # Prezentácia (PowerPoint, slides)
├── README.md                # Readme súbor
└── DeerHunter.sln           # Visual Studio solution
```

## CodeDocs/ (Projektový obsah)
```
CodeDocs/
├── code/                    # Unity projekt
│   ├── Assembly-CSharp.csproj
│   ├── My project (1).sln
│   ├── Assets/              # Herný obsah
│   ├── Library/             # Cache Unity (IGNORUJ)
│   ├── Logs/                # Log súbory (IGNORUJ)
│   ├── Packages/            # Manifest balíkov
│   ├── ProjectSettings/     # Nastavenia projektu
│   ├── Temp/                # Dočasné súbory (IGNORUJ)
│   └── UserSettings/        # Lokálne nastavenia (IGNORUJ)
│
├── data/                    # Zdrojové dáta a surové materiály
│   ├── models/              # 3D modely (Blender, zdroje)
│   ├── source/              # Zdrojové súbory (PSD, Krita atď.)
│   ├── textures/            # Textúry a obrázky (zdrojové)
│   ├── static/              # Statické assets
│   ├── oz1/ až oz10/        # Game zones (scény?)
│   ├── no signal/           # Assets pre "no signal" scénu
│   ├── Audio súbory         # Zvuky (.MP3, .mp3)
│   ├── Obrázky (PNG, JPG)   # Sprity, UI obrázky
│   ├── *.kra                # Krita súbory (design sources)
│   ├── Deer.zip             # 3D model archiívy
│   ├── old-bed.zip          # Assets archiívy
│   └── logoanim.zip         # Logo animácia
│
├── 00_Code_Overview.md      # Popis všetkých skriptov
└── 01_Key_Systems.md        # Detailný popis systémov
```

## CodeDocs/code/Assets/ (Podrobná štruktúra)
```
Assets/
├── animation/               # Animation clips, controllers
├── cutscene/                # Cutscene assets
├── Materials/               # Materiály a shadery
├── mapa/                    # Mapy
├── models/                  # 3D modely (.obj, .fbx)
├── Realistic Tree/          # Tree assets
├── Scenes/                  # Unity scény (.unity)
│   └── ver1.unity           # Main gameplay scéna
├── Scripts/                 # C# skripts
│   ├── PlayerMovement.cs
│   ├── PewPew.cs            # Shooting system
│   ├── obluda.cs            # Enemy AI
│   ├── srnka.cs             # Deers/NPCs
│   ├── gui.cs               # UI fades
│   ├── DoorTrigger.cs       # Door teleportation
│   ├── flashlight.cs        # Flashlight toggle
│   ├── hodinky.cs           # Time system
│   ├── gameterminator1.cs   # Game over logic
│   └── ... ostatné
├── SkySeries Freebie/       # Sky materials
├── TextMesh Pro/            # TMP assets
├── Tree_Textures/           # Textúry stromov
├── Zvuky                    # Audio súbory
│   ├── backpack.MP3
│   ├── chase.MP3
│   ├── vecer.MP3
│   ├── close-door-382723.mp3
│   └── ... ostatné
├── Textúry a sprity (PNG)   # UI a textúry
│   ├── Tex_Deer.png
│   ├── day1.PNG až day10.PNG
│   ├── Multiplayer.png
│   ├── settings.png
│   ├── dvere.png
│   └── ... ostatné
├── Prefabs/                 # Prefabs
│   ├── Player.prefab
│   └── Tree.prefab
├── New Terrain.asset        # Unity terrain
└── better.renderTexture     # Render texture
```

## Docs/ (Dokumentácia projektu)
```
Docs/
├── 00_Overview.md           # Popis hry, ciele, tech stack
├── 01_Setup.md              # Setup inštrukcie
├── 02_Project_Structure.md  # TÁTO STRÁNKA
└── 04_Builds.md             # Build export proces
```

## Design/ (Game Design)
```
Design/
└── GDD.md                   # Game Design Document
```

## Presentation/ (Prezentácia)
```
Presentation/
├── Slideshow či prezentačné súbory
└── (detaily podľa obsahu)
```

## Builds/ (Exportované buildy)
```
Builds/
├── DeerHunter_Windows_v*.zip
└── (ostatné verzie)
```
**Odporúčenie:** Drž aktuálne buildy v GitHub Releases pre menšie clone.

---

## Important Files v Git-e

### .editorconfig
Jednotné nastavenia editora (indentácia, line endings).

### .gitignore
Ignoruj tieto Unity archiválie:
- `CodeDocs/code/Library/`
- `CodeDocs/code/Temp/`
- `CodeDocs/code/UserSettings/`
- `CodeDocs/code/Logs/`
- `.vs/`, `.vscode/`
- `.DS_Store` (macOS)

### .gitattributes
Stopuje Git LFS pre binárne súbory:
```
*.png filter=lfs
*.mp3 filter=lfs
*.wav filter=lfs
*.obj filter=lfs
*.zip filter=lfs
*.FBX filter=lfs
```

### .github/
Workflows pre CI/CD (GitHub Actions).

---

## CodeDocs/data/ - Zdrojové dáta
Obsahuje všetky surové materiály, ktoré sa importujú do Unity:

- **models/** - Originálne 3D modely (Blender sources)
- **source/** - Zdrojové súbory (Krita .kra, Photoshop .psd)
- **textures/** - Textúrové zdroje
- **static/** - Statické assets
- **Audio** - Surové zvukové dáta
- **oz1-oz10/** - Surové assets pre jednotlivé zóny/scény
- **no signal/** - Surové assets pre "no signal" scénu

---

## Klúčové Pozornosti

1. **Unity Cache** - Library/, Temp/, UserSettings/, Logs/ sa automaticky vygenerujú, **NECOMMITUJ** ich
2. **Assets v Unity** - CodeDocs/code/Assets/ obsahuje všetky importované assets pre hru
3. **Source Materials** - CodeDocs/data/ obsahuje originálne zdroje kôli editáciám
4. **Git LFS** - Veľké binárne súbory používajú Git LFS aby repo zostal malý
