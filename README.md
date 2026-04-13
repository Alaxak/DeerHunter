# DeerHunter 🌲🔫

**Survival Horror First-Person Hunter** – Prežij noc v lese. Streľaj jeleny. Unikaj monštru.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Unity Version](https://img.shields.io/badge/Unity-2022.3_LTS-blue.svg)](https://unity.com)
[![Platform](https://img.shields.io/badge/Platform-Windows_%7C_macOS-brightgreen.svg)](#)

---

## 📖 Popis hry

**DeerHunter** je survival horror hra z prvej osoby, kde si lovcom v lesnom prostredí. Počas dňa zbieraš zdroje a lovíš jeleny, ale keď príde noc, tajomná bytosť ťa začne prenasledovať. Tvoj cieľ: **prežiť do úsvitu**.

### Gameplay Loop
1. **Pohyb & Orientácia** – Naviguj v 3D lesnom prostredí (WASD + Mouse)
2. **Lovenie** – Streľaj na jeleny presnosťou a taktickým načasovaním
3. **Survival** – Unikaj nepriateľovi alebo sa chráň za dverami
4. **Progresie** – Každá nasledujúca noc je ťažšia

---

## 🚀 Rýchly štart

### Predpoklady
- **Git LFS** (pre binárne assets)
- **Unity 2022.3 LTS** alebo novšie
- **Min. 10 GB** disk priestoru

### Inštalácia
```bash
# 1. Inštaluj Git LFS
git lfs install

# 2. Klonuj repo
git clone <repo-url>
cd DeerHunter

# 3. Otvor v Unity Hub
# Add → vyber priečinok DeerHunter
# Engine: Unity 2022.3 LTS
```

### Povinné nastavenia
V Unity editore (File → Project Settings):
- **Editor** → Version Control: **Visible Meta Files**
- **Editor** → Asset Serialization: **Force Text**

Viac detailov: [Setup Guide](Docs/01_Setup.md)

---

## 📁 Dokumentácia

| Dokument | Obsah |
|----------|-------|
| [Overview](Docs/00_Overview.md) | Názov, ciele, tech stack |
| [Setup](Docs/01_Setup.md) | Krok-za-krokom inštalácia |
| [Project Structure](Docs/02_Project_Structure.md) | Štruktúra priečinkov |
| [Git Workflow](Docs/03_Workflow_Git.md) | Branching, commits, PR pravidlá |
| [Builds](Docs/04_Builds.md) | Export a packaging |
| [Code Overview](CodeDocs/00_Code_Overview.md) | Popis všetkých skriptov |
| [Key Systems](CodeDocs/01_Key_Systems.md) | Detailný popis systémov |
| [Design Doc](Design/GDD.md) | Game Design Document |

---

## 🎮 Ovládanie

| Klávesa | Akcia |
|---------|-------|
| **W/A/S/D** | Pohyb |
| **Mouse** | Rotácia pohľadu |
| **LMB** | Výstrel |
| **R** | Krčenie sa |
| **F** | Flašľa (zoom) |

---

## 📦 Build & Release

Buildy sú k dispozícii na:
- **Itch.io**: [alaxak.itch.io/deer-hunter](https://alaxak.itch.io/deer-hunter)


---

## 🛠️ Tech Stack

- **Engine**: Unity 2022.3 LTS
- **Render Pipeline**: Built-in / URP (lightweight)
- **Physics**: CharacterController + Colliders
- **Input**: Legacy Input Manager
- **Version Control**: Git + Git LFS
- **IDE**: Visual Studio Code / Rider

---

## 📋 Stav projektu

| Systém | Stav |
|--------|------|
| Player Controller | ✅ Hotovo |
| Shooting System | ✅ Hotovo |
| Enemy AI | ✅ Hotovo |
| Day/Night Cycle | ✅ Hotovo |
| Door Teleportation | ✅ Hotovo |
| UI & Audio | ✅ Hotovo |
| Multiplayer | ❌ MOŽNO to pridám |

---

## 🤝 Prispievanie

Keď prispievaš:
1. Vezmi **dev** branch ako base
2. Vytvor **feat/xyz** branch
3. Commity podľa konvencie: `feat:`, `fix:`, `docs:`
4. Otvori **PR** s popisom
5. Aspoň 1 review + smoke test pred merge-om

Detaily: [Git Workflow](Docs/03_Workflow_Git.md)

---

---

## 👨‍💻 Tvorcovia

- **Alan Pažitnaj** – Lead Dev / Game Design
---

## 🔗 Odkazy

- 🎮 **Play**: [itch.io/deer-hunter](https://alaxak.itch.io/deer-hunter)
- 📖 **Docs**: [Docs/](Docs/)
- 🎨 **Design**: [Design/GDD.md](Design/GDD.md)
- 💻 **Code**: [CodeDocs/](CodeDocs/)

---

## ❓ FAQ

**Q: Aká je recommended Unity verzia?**  
A: 2022.3 LTS. Nové verzie (2023, 2024) by mali tiež fungovať.

**Q: Kde sú assets (textúry, zvuky)?**  
A: Sledované cez Git LFS. Po `git clone` budeš mať všetko.

**Q: Ako sa exportuje játek?**  
A: Pozri [Builds Guide](Docs/04_Builds.md).

**Q: Môžem vytvoriť mod?**  
A: Áno! Code je open & MIT licensed. Fork a push pull request.

---

**Created with ❤️ using Unity**
