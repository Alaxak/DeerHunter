# Code Overview

Tento priečinok slúži na **popis architektúry a kódu**

Hra bola připravena v engine **Unity** – First-person hunting survival game.

## Ako hra funguje
Hráč sa pohybuje v 3D prostredí z first-person pohľadu, hľadá a streľuje na jelene (srnky), zatiaľ čo ho prenasleduje silný nepriateľ (obluda). Cieľom je prežiť a zbierať resursy pred príchodom noci.

---

## Štruktúra kódu

### Player Controller系统
- **PlayerMovement.cs** – Riadenie pohybu hráča (WASD), rotácia kamery
  - CharacterController pre fyziku pohybu

- **PewPew.cs** – Systém streľby hráča
  - Spawn projektiled s animáciou (puška)
  - Reload delay (3 sekundy)
  - Audio feedback pri výstrele
  - Animácia zbrane s možnosťou nahradiť objekt po skončení animácie
  - Camera shake efekt pri výstrele


### Enemy & NPC Systémy
- **obluda.cs** – Hlavný nepriateľ (monster/creature)
  - Sleduje ciieľ (najčastejšie hráč)
  - Dva režimy rýchlosti: rýchla (4 m/s) mimo slow radiusu, pomalá (1.5 m/s) blízko cieľa
  - Hit stun mechanika (1 sekundu pri zásahu projektilom)
  - Pohyb obmedzený na X,Z osi (bez skákania)

- **srnka.cs** – Jelene (NPC/game objects)
  - Spawn jelena v určitom radiuse
  - Pohyb po náhodných bodoch v radiuse
  - Interakcia s hráčom (trigger na odstránenie)
  - Možnosť teleportovania medzi predvolenými bodmi
  - Rotácia a rôzne animácie pri spustení

### UI & Interactions
- **gui.cs** – GUI systém pre nočný fade efekt
  - Riadenie CanvasGroup alpha na začiatku/konci noci
  - Smooth coroutine-based fade in/out (1 sekunda + 2 sekundy hold + 1 sekunda fade out)

- **lobby.cs** – Lobby/menu loopovací pohľad
  - Rotácia View podľa myšky (sensitivity 15)
  - Pre menu obrazovku

- **singleplayerbutton.cs** – UI tlačidlo na spustenie single player režimu
- **quitgamebutton.cs** – UI tlačidlo na ukončenie hry

### Environment & Triggery
- **DoorTrigger.cs** – Systém dverí/teleportácie
  - Detekcia hráča cez collider trigger alebo proximity check
  - Teleportácia hráča na spawn point po vstupe
  - Debounce mechanikou (min. 0.5 sekundy medzi aktiváciami)
  - Voliteľna interakcia s GameManager pre zmenu spawn pointého

- **CollisionGameStopper.cs** – Zastavenie hry pri zásahu
  - Detekcia kolízie s nepriateleom
  - Game over logika

- **CameraShake.cs** – Kamera zmrazí efekt
  - Aplikuje sa pri výstrele (PewPew systém)

- **ProjectileMarker.cs** – Vizualizácia projektilu
  - Markér pre debug/visual feedback

### Audio & Effects
- **cassetess.cs** – Cassette/audio systém 
- **backpack.cs** – Batoh/inventory systém

### Scenáre & State Management
- **day.cs** – Scenár pre Dni
- **hodinky.cs** – Systém hodiniek/času (day cycle)
- **gameterminator1.cs** – Riadenie končenia hry/levelu

---

## Konvencie kódu
- 1 public class = 1 súbor (napr. `PlayerMovement.cs` obsahuje públic class PlayerMovement)
- **Naming**: PascalCase pre triedy a public metódy (PlayerMovement, PewPew)
- **Serialization**: `[SerializeField] private` pre nastaviteľné parametre v Unity inspektore
- **Tooltips**: `[Tooltip("...")]` pre dokumentáciu v inspektore
- **Headers**: `[Header("...")]` na organizáciu inspektora do sekcií

---

## Kľúčové toky

### Input → Gameplay → Feedback
```
Input (WASD, Mouse, F, Fire)
  ↓
PlayerMovement.Update() / PewPew.Update()
  ↓
Physics (CharacterController, Projectiles)
  ↓
Collisions (DoorTrigger, CollisionGameStopper, ProjectileHits)
  ↓
Game State & UI (gui, hodinky, gameterminator1)
```

### AI Loop
```
obluda.Update()
  ├→ Compute distance to target
  ├→ Decide speed (fast/slow based on slowRadius)
  ├→ Check for stun state
  └→ Move toward target
```

### Game Loop
```
Night Cycle (hodinky)
  ↓
Spawn entities (srnka, obluda)
  ↓
Player collects/hunts (ProjectileMarker hits)
  ↓
Door triggers progression (DoorTrigger)
  ↓
Night fade (gui.PlayNightFade)
  ↓
Next day / Game over
```

---

## Poznámky
- **Audio**: Používajú sa AudioSource komponenty na fire, ambient sounds (backpack, chase, vecer)
- **Camera**: Locked a hidden cursor v gameplay, free v lobby
- **Physics**: CharacterController pre player, gravity sa aplikuje cez moveDirection
- **Animation**: Animator-based (spúšťo triggery, prípadne legacy Animation)
