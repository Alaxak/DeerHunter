# Game Design Document (light)

## Žáner
- Survival
- Perspektíva: 1st person
- Herný mód: singleplayer

## Pillars
1. Core gameplay slučka (loop) - hráć musí zabezpečiť potravu pre lesníka nato aby mu umožnil prespať noc v chate čím si zabezpečí prežitie.
2. Konzistentný vizuálny a zvukový štýl podporujúci atmosféru hry v podobe hry z 90 rokov.
3. Intuitívne ovládanie s dôrazom na responzívnosť a „game feel“  
4. Progresia motivujúca hráča k opakovanému hraniu v podobe najdlhšie prežitia v počte dní. 

## Mechaniky
- Pohyb hráča (chôdza)  
- Combat systém (ranged)  
- Interakcia s prostredím (aktivácia objektov)   
- AI správanie zvery (patrol patterns)  
- Resource management (backpack - info o počte obetí)  
- Procedurálne levely

## UI flow
- Main Menu → (Play / Exit)   
- Game Start → Intro
- Core Gameplay Loop → (hráč hrá → získava zdroje → pokračuje)  
- Game Over → (Game exit)  
- HUD → (Resource indikátory, timer)  

### Vstupy
| Klávesa | Akcia |
|---------|-------|
| **W/A/S/D** | Pohyb |
| **Mouse** | Rotácia pohľadu |
| **TAB** | Backpack |
| **R** | Timer |
| **LMB** | Výstrel |

### Interakcie
- DoorTrigger → teleportácia hráča
- CollisionGameStopper → Game Over pri zásahu nepriateľom
- Projectiles → zasahujú srnky a nepriateľa (stun)

---

## Enemy AI
**Súbory:** `obluda.cs`, `srnka.cs`

### Zodpovednosť

#### obluda.cs (Monster - Hlavný nepriateľ)
- Sleduje cieľ (hráč)
- Dve-rýchlostný pohyb (agresívny vs pomalý)

#### srnka.cs (Jelene - Huntables)
- Spawn objektov v radiuse
- Náhodný pohyb
- Teleportácia medzi bodmi
- Animácie a rotácie

### Stavy

#### obluda
- **Idle**: target neaktívny
- **Hunting (Fast)**: daleký cieľ → 4 m/s
- **Hunting (Slow)**: blízko cieľa (< 5m) → 1.5 m/s

#### srnka
- **Wandering**: náhodný pohyb v radiuse
- **Triggered**: teleportácia + rotácia
- **Removed**: zničenie pri kolízii

### Senzory
- **Distance Check**: slowRadius = 5m (rozhoduje o rýchlosti)
- **Target State**: sleduje activeInHierarchy cieľa
- **Proximity**: spawn v rámci radiusu
- **Collision**: OnTriggerEnter na remove

---

## UI & Feedback

**Súbory:** `gui.cs`, `singleplayerbutton.cs`, `quitgamebutton.cs`, `CameraShake.cs`

- **Night Fade**: Fade in/out medzi dňami
- **Camera Shake**: Rotácia pri výstrele
- **Audio Feedback**: fire, reload, ambient sounds

---

## Save/Load
- **Formát**: Momentálne **NIE JE IMPLEMENTOVANÉ**