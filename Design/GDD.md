# Game Design Document (light)

## Žáner
- **Survival Horror / Action**
- **Perspektíva**: 1st Person (First-Person Shooter)
- **Herný mód**: Singleplayer
- **Téma**: Poľovnícky horór – Hráč je lovcom, ktorého v noci nasleduje tajomný neznanec (obluda)

---

## Pillars (5 hlavných pilierov)
1. **Survival Tension** – Noc je neustála hrozba; hráč musí prežiť do úsvitu
2. **Hunting Mechanics** – Streľba na jelene (srnky) s presnosťou a načasovaním
3. **Chase & Fear** – Nepriateľ (obluda) aktívne sleduje hráča s meniacou sa agresivitou
4. **Environmental Interaction** – Dvere, svietidlá, presun medzi oblasťami
5. **Day/Night Cycle** – Progresívnu hru prostredníctvom viacerých dní s zvyšujúcou sa ťažkosťou

---

## Mechaniky

### Pohyb & Kontrola
- **WASD** – Pohyb hráča (forward/backward, strafe left/right)
- **Mouse** – Rotácia pohľadu v 3D priestore

### Streľba & Combat
- **LMB (Ľavé tlačidlo myši)** – Výstrel z pušky
- **Reload Delay** – 3 sekundy medzi výstrelmi (cooldown)
- **Projektily** – Pohybujú sa 5 sekúnd predtým, ako zanikajú
- **Hit Detection**:
  - Zásah **jelena** (srnka) = odstránenie z mapy
  - Zásah **nepriateľa** (obluda) = 1 sekunda stun efekt (paralýza)

### Enemy AI
- **obluda (Monster)**:
  - Sleduje hráča v dvoch režimoch:
    - **Far Chase** (>5m) – Rýchly pohyb 4 m/s (vyzerá agresívne)
    - **Close Hunt** (≤5m) – Pomalý pohyb 1.5 m/s (taktický přístup)
  - Po zásahu projektilom: 1 sekundu paralýzy (stun)
  - Resetuje sa na počiatočnú pozíciu pri aktivácii nového dňa

- **srnka (Jelene)**:
  - Náhodne sa pohybujú v limitovanej oblasti
  - Aktivujú sa na základe herného scenára
  - Môžu byť löviť (odstránené pri zásahu)
  - Animácie rotácie a pohybov pre vierohodnosť

### Prostredie & Interakcia
- **Dvere (DoorTriggers)**:
  - Vstup do dverí = teleportácia hráča na novú pozíciu (room/area)
  - Spúšťa progresiu scenára
  - Môže resetovať spawn body
  
### Progresie & State Management
- **Hodinky (Time System)**:
  - Herný čas progresuje počas dňa
  - Noc = zvýšená hrozba (obluda je aktívne aj agresívní)
  - Fade-in/fade-out efekt medzi dňami (**Night Fade**)

- **Day Cycle**:
  - Deň 1, 2, 3... (napr. Day 1 = intro, väčšia hrazba v neskorom dni)
  - Počas každého dňa: lovenie jelení → prežiť noc → progresie na ďalší deň
  - Game Over: Ak hráč koliduje s nepriateľom (CollisionGameStopper)

### Audio & Atmosphere
- **Zvuky**:
  - Fire sound – Kedy hráč streľa
  - Reload sound – Po čakaní cooldownu
  - Chase music – Keď nepriateľ aktivne sleduje
  - Evening ambience – Večer v prírode
  - Door close – Pri teleportácii

### Camera & Feel
- **Camera Shake** – Krátka rotácia kamery pri výstrele (recoil efekt)
- **First-Person View** – Kamera z pohľadu hráča
- **Free Camera (Menu)** – V lobby/menu je kamera voľne otáčateľná (Mouse Look)

---

## UI Flow

```
┌─────────────┐
│  Main Menu  │ (lobby.cs – Free camera view)
└──────┬──────┘
       │
       ├──→ [Single Player Button] ──→ Game Start
       │
       └──→ [Quit Button] ──→ Exit App
       
       
┌──────────────────────────────┐
│    GAMEPLAY LOOP             │
├──────────────────────────────┤
│                              │
│  1. Spawn entities (obluda,  │
│     srnky) v scenári         │
│                              │
│  2. Hráč ovláda:             │
│     - Pohyb (WASD)           │
│     - Streľba (LMB)          │
│     - Svetlo (F)             │
│                              │
│  3. AI Update:               │
│     - obluda pozoruje hráča  │
│     - srnka sa pohybuje      │
│                              │
│  4. Interakcie:              │
│     - Projektil vs Entity    │
│     - Player vs Door         │
│     - Player vs Monster      │
│                              │
│  5. Evening:                 │
│     - Night Fade (fade out)  │
│                              │
│  6. Next Day / Game Over     │
│                              │
└──────────────────────────────┘
            
            
┌──────────────────────┐
│  Game Over           │
├──────────────────────┤
│ - Game exit          │
└──────────────────────┘
```


---

## Atmosféra & Storytelling

### Téma
Hráč je lovcom s puškou, ktorý sa pokúša prežiť v lesnom prostredí počas noci. Neznáma bytosť (obluda) ho prenasleduje – je to survival horror s elementom "

### Tón
- **Napätie** – Neustála hrozba
- **Izolinácia** – Samotný v prírode
- **Atmosféra** – Nočné zvuky, tieň, neznámo

---

## Cieľ Hry
1. **Primárny cieľ**: Prežiť noc (uniknúť monštru / dožiť úsvit)
2. **Sekundárny cieľ**: Lovať jelene pre skóre / zdroje
3. **Dlhodobý cieľ**: Postupovať cez viacero dní s zvyšujúcou sa ťažkosťou

---

## Technické Aspekty (z kódu)

| Systém | Komponenta | Stav |
|--------|-----------|------|
| **Physics** | CharacterController | ✓ Implementované |
| **Input** | Player controls | ✓ Implementované |
| **Combat** | Projectiles + Hit Detection | ✓ Implementované |
| **AI** | obluda + srnka | ✓ Implementované |
| **Environment** | DoorTriggers, Collisions | ✓ Implementované |
| **Time/Progression** | hodinky, day1, gameterminator | ✓ Implementované |
| **UI** | gui (fade), buttons, lobby | ✓ Implementované |
| **Audio** | AudioSource feedback | ✓ Sčasti |
| **Save/Load** | - | ❌ Nie je |

---

## Budúce Rozšírenia 
- Rôzne typy zbraní / upgrades
- Multiplayer režim (hint: singleplayerbutton vs multiplayer button)
- Dynamické prostredie (štyri sezóny, počasie)
