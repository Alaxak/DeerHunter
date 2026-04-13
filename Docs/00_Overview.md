# Overview

## Názov hry
**DeerHunter** – Survival Horror / First-Person Hunter


## Cieľová platforma
- **Windows** (Primary)


## Core loop
1. **Pohyb & Orientácia** – Hráč sa pohybuje v 3D prostredí, orientuje sa podľa time-of-day a objektov
2. **Lovenie** – Hráč streľa na jeleny (srnky) so zbranou
3. **Survival** – Nepriateľ (obluda) sa snaží hráča chytiť pocas noci; hráč sa musí skryť za dverami do konca dna
4. **Progresie** – Každa prekonana noc = nový deň s väčšou ťažkosťou

## FEATURES
- First-person pohyb a kamera (WASD + Mouse)
- Streľba na jeleny s hit detection
- Enemy AI (obluda) s chasing mechanikou
- Day/Night cycle a fade efekty
- Door teleportácia
- Audio feedback (shooting,chodenie, ambient, atd)
- UI menu (Play, Quit)

## Tech stack
- **Unity verzia**: 2022.3 LTS (odporúčané) alebo novšie
- **Render pipeline**: Built-in (štandardný) alebo URP (lightweight)
- **Input system**: Legacy Input Manager (aktuálne v kóde)
- **Persistencia/Save**: Zatiaľ nie; odporúčanie: JSON alebo Binary
- **Physika**: CharacterController (player), standard colliders (enemies)
