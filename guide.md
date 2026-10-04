# Blobfisch Survivors — Complete Reference

Every number below is pulled directly from the current game code, not from memory — and the weapon/passive tables below have also been checked against the running game level by level, so this reflects what's shipped right now. Percentages and damage values are shown *before* your character's damage multiplier and any Shop bonuses are applied, except where noted.

---

## 1. The Blobfische (Playable Characters)

| Character | Unlock | HP | Speed | Damage | Weapon Cooldown | Luck | Sprite behavior |
|---|---|---|---|---|---|---|---|
| **Standard-Blobi** | Available from the start | 100 | 150 | ×1.0 | ×1.0 | 0 | Top-down art — rotates freely to face any direction |
| **Turbo-Blobi** | Available from the start | 75 | 196 | ×0.9 | ×1.0 | 0 | Side-view art — mirrors left/right, tilts up to 90° |
| **Panzer-Blobi** | Available from the start | 145 | 122 | ×1.0 | ×1.05 (5% *slower*) | 0 | Side-view art — mirrors left/right, tilts up to 90° |
| **Glücks-Blobi** | Reach level 15 in one run | 90 | 155 | ×1.0 | ×0.95 (5% *faster*) | +3 | Side-view art — mirrors left/right, tilts up to 90° |

The character-select cards now show the real, current numbers (including any Shop bonuses), and the stage cards show their difficulty multiplier and boss. These are *base* stats. Shop upgrades (Section 8) add flat/percentage bonuses on top of whichever character you pick, every run.

Turbo, Panzer, and Glücks are drawn from the side, so instead of spinning all the way around (which would flip them upside-down), they mirror horizontally once you're heading more than 90° away from their natural facing, and only tilt within that ±90° window. Standard is the only one drawn from directly above, so it turns freely in a full circle.

---

## 2. Gebiete (Stages)

| Stage | Difficulty multiplier | Boss |
|---|---|---|
| Korallenriff (Coral Reef) | 1.0 | Hai-König |
| Kelpwald (Kelp Forest) | 1.35 | Riesenkrake |
| Tiefsee-Graben (Deep Trench) | 1.75 | Meeresungeheuer |
| Vulkanschlucht (Volcanic Vent) | 2.2 | Lava-Titan |

The difficulty multiplier affects how fast regular enemies gain HP/damage over time and how quickly the spawn rate ramps up (see Section 3) — a run in Vulkanschlucht gets harder much faster than the same elapsed time in Korallenriff.

---

## 3. Gegner (Regular Enemies)

Base stats below; actual in-run stats scale with time elapsed and stage difficulty (formula at the bottom).

| Enemy | HP | Speed | Damage | XP | Behavior |
|---|---|---|---|---|---|
| Qualle (Jellyfish) | 11 | 52 | 8 | 2 | Chases you directly |
| Kleiner Hai (Small Shark) | 8 | 112 | 6 | 2 | Chases you directly |
| Krebs (Crab) | 26 | 42 | 10 | 3 | Chases you directly |
| Anglerfisch (Anglerfish) | 15 | 38 | 7 | 3 | Keeps mid-range and fires projectiles at you |
| Seeigel (Sea Urchin) | 22 | 0 | 12 | 2 | Stationary; damages on contact only |
| Muräne (Moray Eel) | 13 | 128 | 9 | 3 | Chases with erratic, jittery movement |
| Tintenfisch (Octopus) | 19 | 58 | 6 | 3 | Chases you and periodically fires a slow-inducing ink shot |
| Piranha | 6 | 135 | 5 | 1 | Fast swarm chaser, low HP |
| Riesenkrebs (Giant Crab) | 70 | 46 | 15 | 9 | Tanky elite-style chaser |

**Which enemies appear where:**
- **Riff:** Qualle, Kleiner Hai, Krebs, Anglerfisch, Piranha
- **Kelp:** Qualle, Kleiner Hai, Krebs, Muräne, Tintenfisch, Piranha, Seeigel
- **Graben:** Muräne, Tintenfisch, Anglerfisch, Seeigel, Riesenkrebs, Kleiner Hai, Krebs
- **Vulkan:** Riesenkrebs, Tintenfisch, Muräne, Anglerfisch, Seeigel, Krebs, Piranha

**Time-based scaling** (applied at the moment each enemy spawns):
- HP multiplier: `1 + (minutes elapsed × 0.24 × stage difficulty)`
- Damage multiplier: `1 + (minutes elapsed × 0.10 × stage difficulty)`

**Spawning:** starts at 1 enemy per wave, gains +1 to the wave size every ~100 seconds (capped at 4 per wave), and the gap between waves shrinks from 1.2s down to a floor of 0.45s as the stage difficulty pushes it down over time. There's a soft cap of 70 living enemies on screen at once — if it's ever exceeded, the *oldest* regular enemies are quietly retired to keep things smooth (the boss is always exempt from this).

---

## 4. Bosse

| Boss | Stage | Base HP | Base Speed | Base Damage | XP |
|---|---|---|---|---|---|
| Hai-König | Korallenriff | 750 | 75 | 20 | 120 |
| Riesenkrake | Kelpwald | 1350 | 58 | 24 | 180 |
| Meeresungeheuer | Tiefsee-Graben | 2100 | 62 | 28 | 250 |
| Lava-Titan | Vulkanschlucht | 3000 | 52 | 34 | 340 |

**Bosses now recur.** The first one shows up 5 minutes into a run (with a 3-second warning banner). Defeat it, and the *next* one — same species, tied to your stage — arrives exactly 4 minutes later, and every subsequent encounter is stronger than the last:

- HP multiplier per encounter: `(1 + (stage difficulty − 1) × 0.5) × (1 + encounter number × 0.4)`
- Damage multiplier per encounter: `1 + encounter number × 0.2`

So your 3rd Hai-König (encounter index 2) spawns with roughly 1.8× the HP and 1.4× the damage of the first. The HUD shows a `×N` suffix next to a repeat boss's name so you can tell it's a tougher return bout. This can continue indefinitely as long as you keep surviving and defeating them.

**Boss attacks:**
- **Radial burst** — every 4.5s while you're within 700 units, fires 10 shots in a full circle, each dealing 70% of the boss's damage. These are ordinary shots — your Bubble Ring can destroy them on contact.
- **Heavy shot** — every ~7–8.5s while you're within 800 units, fires one large, slow, glowing red shot dealing 140% of the boss's damage, aimed directly at you. This **cannot** be deflected by the Bubble Ring — only a charged Schutzschild (or simply dodging it, since it travels slowly) will save you from it.

Defeating any boss always drops 8–13 pearls.

---

## 5. Waffen (Weapons)

Every weapon can be leveled 1–5 by picking it (or picking it again) on level-up. Damage figures already include the "+level" scaling but **not** your character's damage multiplier or Shop damage bonus — multiply by both to get your real numbers.

### Blasenschuss (Bubble Shot) — starting weapon
Homing shot at the nearest enemy within 900 range. Base cooldown 0.85s.

| Level | Damage | Shots fired |
|---|---|---|
| 1 | 10.4 | 1 |
| 2 | 13.8 | 1 |
| 3 | 17.2 | 2 |
| 4 | 20.6 | 2 |
| 5 | 24.0 | 3 |

### Blasenring (Bubble Ring)
Orbiting bubbles that damage anything they touch (0.3s cooldown per individual enemy) **and destroy ordinary enemy shots on contact** (small deflect burst + sound + 1 HP back to you). Does not stop bosses' heavy red shots.

| Level | Bubbles | Damage/hit | Orbit radius |
|---|---|---|---|
| 1 | 2 | 9 | 59 |
| 2 | 4 | 12 | 66 |
| 3 | 6 | 15 | 73 |
| 4 | 8 | 18 | 80 |
| 5 | 10 | 21 | 87 |

### Tintenwolke (Ink Cloud)
Pulses from a point trailing 34 units *behind* your current facing direction (not centered on you), rendered as a soft, multi-tinted, drifting cloud. Base cooldown 1.2s. Deals **percentage of the target's max HP**, and slows anything it hits by 35% for 1.5s. Only a fraction of its damage applies to bosses so it can't trivialize them.

| Level | Radius | Damage vs. regular enemies | Damage vs. bosses |
|---|---|---|---|
| 1 | 90 | 10.5% of max HP | 1.58% of max HP |
| 2 | 110 | 13.0% | 1.95% |
| 3 | 130 | 15.5% | 2.33% |
| 4 | 150 | 18.0% | 2.70% |
| 5 | 170 | 20.5% | 3.08% |

### Harpune (Harpoon)
Straight-line piercing shot. Base cooldown 1.1s.

| Level | Damage | Enemies pierced |
|---|---|---|
| 1 | 14.2 | 3 |
| 2 | 18.4 | 4 |
| 3 | 22.6 | 5 |
| 4 | 26.8 | 6 |
| 5 | 31.0 | 7 |

### Elektroschlag (Electric Shock)
Chain lightning that jumps between enemies within 260 units of each other. Base cooldown 1.3s.

| Level | Damage/jump | Max jumps |
|---|---|---|
| 1 | 8.6 | 3 |
| 2 | 11.2 | 4 |
| 3 | 13.8 | 5 |
| 4 | 16.4 | 6 |
| 5 | 19.0 | 7 |

### Korallenspeer (Coral Spear)
Single heavy hit at the nearest enemy — the hardest-hitting shot in the game. Base cooldown 1.4s.

| Level | Damage |
|---|---|
| 1 | 31.0 |
| 2 | 40.0 |
| 3 | 49.0 |
| 4 | 58.0 |
| 5 | 67.0 |

### Schwarm-Freund (Swarm Friend)
One (later two) independent companion fish that actively hunt: each one seeks the nearest enemy within 300 units of you, swims in to engage it directly, and fires on it — returning to idle orbit near you when nothing's around, and never wandering more than 300 units away.

| Level | Damage/shot | Fire interval | Companions |
|---|---|---|---|
| 1 | 9 | 1.15s | 1 |
| 2 | 12 | 1.00s | 1 |
| 3 | 15 | 0.85s | 2 |
| 4 | 18 | 0.70s | 2 |
| 5 | 21 | 0.55s | 2 |

The 2nd companion unlocks at level 3, orbiting on the opposite side from the first.

---

## 6. Passive Verbesserungen (Passives)

| Passive | Effect per level | L1 | L2 | L3 | L4 | L5 |
|---|---|---|---|---|---|---|
| **Flossen-Tempo** | +4% movement speed | +4% | +8% | +12% | +16% | +20% |
| **Extra-Leben** | +20 max HP (and heals you that much immediately when picked) | +20 | +40 | +60 | +80 | +100 |
| **Panzerung** | Flat damage reduction on every hit (min. 1 damage always gets through) | −1.2 | −2.4 | −3.6 | −4.8 | −6.0 |
| **Anziehungskraft** | +pickup radius | +20 | +40 | +60 | +80 | +100 |
| **Angriffstempo** | Reduces cooldowns on Blasenschuss/Tintenwolke/Harpune/Elektroschlag/Korallenspeer (not Ring or Friend, which don't use cooldowns) | −8% | −16% | −24% | −32% | −40% |
| **Glück** | +1 Luck per level (see Luck below) | +1 | +2 | +3 | +4 | +5 |
| **Schutzschild** | Recharge time for a shield charge that fully blocks your next hit — any hit, including a boss's heavy shot | 13.8s | 11.6s | 9.4s | 7.2s | 5.0s |
| **Regeneration** | Continuous healing per second | 0.15/s | 0.30/s | 0.45/s | 0.60/s | 0.75/s |

Notes:
- **Extra-Leben is *not* a revive.** Despite the name, it permanently raises your max HP for the run and heals you by the same amount when picked — it never brings you back from death. The only revive in the game is **Zweite Chance** in the Shop (Section 8).
- **Schutzschild** grants an immediate free charge the moment you first pick it, then recharges on the timer above after each block.
- **Luck** is a shared stat: it comes from your character (Glücks-Blobi starts at +3), the Shop's Glücksbringer (+1 per level), and this passive (+1 per level). Each point of Luck does two things: **+10% pearls from every pearl pickup** (tracked fractionally, so +10% really does mean one extra pearl per ten collected), and **+6% chance that a level-up offers a 4th upgrade card instead of 3** (capped at 60%). When the bonus card appears, the level-up screen says so.
- Regeneration and the shield are the only two ways to recover HP mid-run (a healing-pickup mechanic existed briefly and was removed a few turns back for being too strong stacked with these).

---

## 7. Spezialmechaniken (How defense works, tied together)

1. **Ordinary enemy shots** (angler fish, the boss's radial burst) — blockable by the Bubble Ring on contact.
2. **Heavy boss shots** (the big glowing red ones) — ignore the Ring entirely. Dodge them or have a charged Schutzschild.
3. **Contact damage** from touching an enemy — reduced by Panzerung, avoidable with i-frames (0.5s after any hit) or a charged shield.
4. **Sustain** — only Regeneration (slow, continuous) and Schutzschild (occasional full block) protect or recover your HP mid-run; Zweite Chance (Shop) is the only revive. There's no other healing in the game right now.

**Leveling curve:** XP needed for level *N* is `6 + N × 4.6`, so it grows roughly linearly (a bit under 5 XP more needed per level).

---

## 8. Shop (Permanent Upgrades, bought with banked Perlen)

Cost to go from level *N* to *N+1* is `base cost × multiplier^N`, rounded.

| Upgrade | Effect/level | Max level | Cost: Lv1 → Lv2 → Lv3 → Lv4 → Lv5 |
|---|---|---|---|---|
| Grösserer Lebensvorrat | +10 starting max HP | 5 | 40 → 64 → 102 → 164 → 262 |
| Bessere Flossen | +3% starting speed | 5 | 40 → 64 → 102 → 164 → 262 |
| Schärfere Stacheln | +4% weapon damage | 5 | 55 → 94 → 159 → 270 → 459 |
| Perlen-Magnet | +22 pickup radius (base becomes 70 + 22×level) | 5 | 35 → 53 → 79 → 118 → 177 |
| Glücksbringer | +1 starting Luck (more pearls, more often a 4th upgrade card) | 3 | 70 → 126 → 227 |
| Zweite Chance | Revive once per run at 50% max HP | 1 (one-time) | 180 |

**How Zweite Chance works:** it's a one-time, permanent purchase — once bought, every run starts with a revive "armed", shown as a green heart (💚) next to your HP numbers in the HUD. The first time you'd die, you're automatically brought back at 50% max HP with 2 seconds of invulnerability and a "Zweite Chance genutzt!" banner; the heart then disappears for the rest of that run. There's no button to press and it can't be found or picked up mid-run — it has to be bought in the Shop before you start.

These stack with your character's base stats and any in-run passives you pick — they're permanent, applied at the start of every run regardless of character.

---

## 9. Erfolge (Achievements)

| Achievement | Condition |
|---|---|
| Erster Blubb | Defeat your first enemy ever |
| Blasen-Profi | Defeat 100 enemies total (lifetime) |
| Ozean-Legende | Defeat 1000 enemies total (lifetime) |
| Kurzer Tauchgang | Survive 5 minutes in a single run |
| Tiefseeforscher | Survive 15 minutes in a single run |
| Königsschlächter | Defeat any boss once |
| Boss-Bezwinger | Defeat all 4 boss *species* (lifetime) — since each stage has its own boss, this means winning in every stage at least once |
| Perlensammler | Collect 1000 pearls total (lifetime) |
| Voll entwickelt | Reach level 20 in a single run |
| Ganze Blobi-Familie | Unlock all 4 characters |

---

## 10. Fortschritt & Speichern (Saving)

- **Between runs:** pearls, Shop levels, achievements, best stats, and character unlocks save automatically to the browser's local storage every time they change, and persist across sessions once this is live on your actual site.
- **Mid-run:** the game also snapshots your *current* run — level, weapons, passives, HP, elapsed time, pearls so far, position — whenever the tab is backgrounded, right before the page is hidden, and every ~8 seconds while playing. If the browser discards or reloads the tab (common on mobile after being away a while), the main menu offers a **"Weiterspielen"** button that restores your **progress** instead of losing it: level, XP, weapons, passives, HP, elapsed time, pearls and position all come back. What does *not* come back is the live scene — enemies, projectiles and pickups on screen are cleared, so you resume into open water with 1.5 seconds of invulnerability. If a boss was alive when you left, that same boss encounter restarts at full HP a few seconds after you resume (it does not skip ahead to the next, tougher one). Starting a genuinely new run discards the pending snapshot.
- **Quitting via pause** banks your pearls and stats just like dying does — it doesn't throw away progress.

---

## 11. Steuerung (Controls)

- **Desktop:** WASD or arrow keys to move. ESC or the pause icon to pause.
- **Mobile:** drag anywhere on the screen to move.
- Attacks on every weapon are fully automatic — the only inputs are movement and which upgrade to pick on level-up.
