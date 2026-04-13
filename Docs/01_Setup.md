# Setup

## Predpoklady
- **Git** s LFS podporou nainstalovaný
- **Unity Hub** (free verzia OK)
- **Visual Studio Code** alebo **Rider** (IDE)
- **Min. 10 GB** disk priestoru (Unity + assets)

## Krok 1: Git LFS
```bash
# Nainštaluj Git LFS (jednorazovo)
git lfs install

# Klonuj repo
git clone <repo-url>
cd DeerHunter
```

Git LFS sleduje: `*.png`, `*.wav`, `*.mp3`, `*.obj`, `*.asset`, `*.zip` (binárne väčšinou).

## Krok 2: Otvor projekt v Unity
1. Otvor **Unity Hub**
2. **Add Project** → vyber priečinok `DeerHunter` (kde je `Assets/` a `Packages/`)
3. Ak nie je Unity 2022.3 LTS nainstalovaná, Hub ťa upozorní
4. Projekt sa otvorí a importuje assets (~2-5 minút)

## Krok 3: Povinné nastavenia
V Unity editore:

**Project Settings → Editor:**
- ✓ **Version Control Mode**: Visible Meta Files
- ✓ **Asset Serialization**: Force Text

Toto zabezpečuje:
- `.meta` súbory sú viditeľné v Git-e (potrebné pre Git tracking)
- Assets sa ukladajú ako YAML text (čitateľne v Git-e)

**Project Settings → Physics:**
- Skontroluj Gravity (-9.81 m/s²)
- Default Layer Collision Matrix (výber physics layers)

## Krok 4: Over setup
```bash
# V terminále (v projekt folderí):
git status
# Mal by si vidieť:.gitattributes, .gitignore, a žiadne veľké binárne súbory
```

## Krok 5: Code exploration
- Otvoriť `Assets/Scripts/` v code editore (VS Code + C# extension)
- Skontroluj `PlayerMovement.cs` a `PewPew.cs` aby si pochopil základnu logiku

## Troubleshooting

### Git LFS neinterpreuje
```bash
git lfs pull  # Stiahne LFS objekty
```

### Unity nedokáže importovať assets
- Skúš: Assets → Reimport All
- Alebo: File → Cache Server → Clear Cache

### Skripty majú chyby
- Skúš: Assets → Open C# Project
- Alebo reloadni Unity (File → Reload Domain)
