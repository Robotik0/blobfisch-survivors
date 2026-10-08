# Blobfisch Survivors — Complete Reference

Every number below is pulled directly from the current game code, not from memory — and the weapon/passive tables below have also been checked against the running game level by level, so this reflects what's shipped right now (including area hazards, boss signature moves, elites, area unlocks and achievement rewards). Percentages and damage values are shown *before* your character's damage multiplier, Shop bonuses and the Schlagkraft passive are applied, except where noted.

---

## 1. The Blobfische (Playable Characters)

| Character | Unlock | HP | Speed | Damage | Weapon Cooldown | Luck | Sprite behavior |
|---|---|---|---|---|---|---|---|
| **Standard-Blobi** | Available from the start | 100 | 150 | ×1.0 | ×1.0 | 0 | Top-down art — rotates freely to face any direction |
| **Turbo-Blobi** | Available from the start | 75 | 196 | ×0.9 | ×1.0 | 0 | Side-view art — mirrors left/right, tilts up to 90° |
| **Panzer-Blobi** | Available from the start | 145 | 122 | ×1.0 | ×1.05 (5% *slower*) | 0 | Side-view art — mirrors left/right, tilts up to 90° |
| **Glücks-Blobi** | Reach level 25 in one run | 90 | 155 | ×1.0 | ×0.95 (5% *faster*) | +3 | Side-view art — mirrors left/right, tilts up to 90° |

The character-select cards now show the real, current numbers (including any Shop bonuses), and the stage cards show their difficulty multiplier and boss. These are *base* stats. Shop upgrades (Section 8) add flat/percentage bonuses on top of whichever character you pick, every run. Players who unlocked Glücks-Blobi under the earlier level-15 rule keep it.

Turbo, Panzer, and Glücks are drawn from the side, so instead of spinning all the way around (which would flip them upside-down), they mirror horizontally once you're heading more than 90° away from their natural facing, and only tilt within that ±90° window. Standard is the only one drawn from directly above, so it turns freely in a full circle.

---

## 2. Gebiete (Stages)

| Stage | Difficulty multiplier | Boss | Unlocked by | Area mechanic |
|---|---|---|---|---|
| Korallenriff (Coral Reef) | 1.0 | Hai-König | Available from the start | None — a harmless starter stage |
| Kelpwald (Kelp Forest) | 1.35 | Riesenkrake | Defeating the Hai-König | Kelp patches slow you down |
| Tiefsee-Graben (Deep Trench) | 1.75 | Meeresungeheuer | Defeating the Riesenkrake | Darkness — you only see near you |
| Vulkanschlucht (Volcanic Vent) | 2.2 | Lava-Titan | Defeating the Meeresungeheuer | Periodic lava zones |

The difficulty multiplier affects how fast regular enemies gain HP/damage over time and how quickly the spawn rate ramps up (see Section 3) — a run in Vulkanschlucht gets harder much faster than the same elapsed time in Korallenriff.

**Unlocking:** every stage after the Korallenriff opens once you defeat the boss of the previous one (in any run, with any character). Locked stage cards show a 🔒 and what to beat. Saves that already had progress when this system arrived keep all four stages open.

**Area mechanics in detail:**
- **Korallenriff — nothing.** No hazards; it's meant for learning the game.
- **Kelpwald — kelp patches.** Fixed patches of swaying kelp (radius 70–130 units; about 4 in every 10 map cells of 380 × 380 units contain one, and none sit near your starting point). While you're inside one, your movement speed is ×0.6 (−40%). This multiplies with the Tintenfisch ink slow, so both together leave you at ×0.33. Enemies aren't slowed.
- **Tiefsee-Graben — darkness.** Everything outside a lit circle around you is dark. The circle's radius is half the shorter screen side, clamped to 230–420 units (and gently pulsing); it is fully clear in the inner 40% and fades to 90% dark at 130% of that radius. XP and pearl orbs, enemy shots, bosses and the Anglerfisch's lure stay visible in the dark.
- **Vulkanschlucht — lava zones.** From 0:12 on, lava erupts around you on a timer: every `max(3.2, 7 − seconds/90)` seconds, `min(3, 1 + ⌊seconds/200⌋)` zones (radius 78) appear. The first is placed where you're heading (0.7 s ahead of your movement), the others 110–340 units away in random directions. Each zone shows an orange dashed warning circle for 1.5 s, then burns for 3.5 s. Standing in active lava hurts about once every 0.5 s (your i-frames) for `9 × (1 + minutes × 0.10 × 2.2)` damage — Panzerung reduces it and a charged Schutzschild blocks one tick. Lava isn't a shot, so the Bubble Ring can't stop it, and it doesn't hurt enemies.

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
| Tintenfisch (Octopus) | 19 | 58 | 6 | 3 | Chases you and periodically fires an ink shot that slows you by 45% (movement ×0.55) for 2.2 s |
| Piranha | 6 | 135 | 5 | 1 | Fast chaser, low HP — arrives in schools (see Spawning) |
| Riesenkrebs (Giant Crab) | 70 | 46 | 15 | 9 | Tanky elite-style chaser |

**Which enemies appear where** (listed in the order they're introduced: only the first type spawns at the start, and one more type joins every 25 seconds, so the full roster is out after 100 s in the Riff and after 150 s in the other stages; each unlocked type is then picked with equal probability):
- **Riff:** Qualle, Kleiner Hai, Krebs, Anglerfisch, Piranha
- **Kelp:** Qualle, Kleiner Hai, Krebs, Muräne, Tintenfisch, Piranha, Seeigel
- **Graben:** Kleiner Hai, Muräne, Tintenfisch, Krebs, Anglerfisch, Seeigel, Riesenkrebs
- **Vulkan:** Tintenfisch, Muräne, Krebs, Piranha, Anglerfisch, Seeigel, Riesenkrebs

**Time-based scaling** (applied at the moment each enemy spawns):
- HP multiplier: `1 + (minutes elapsed × 0.24 × stage difficulty)`
- Damage multiplier: `1 + (minutes elapsed × 0.10 × stage difficulty)`

**Spawning:** starts at 1 enemy per wave, gains +1 to the wave size every ~100 seconds (capped at 4 per wave), and the gap between waves shrinks from 1.2s down to a floor of 0.45s as the stage difficulty pushes it down over time (`max(0.45, 1.2 − minutes × 0.055 × stage difficulty)`).

**The 70-enemy cap:** at most 70 regular enemies are alive at once. At the cap, a new spawn never deletes anything you can see — it *replaces the farthest enemy that is outside the screen*, and if every enemy is on-screen the spawn is simply skipped. Bosses and elites are never replaced.

**Piranha schools and rings:** whenever the spawner picks a Piranha it spawns a whole school of `4 + min(5, ⌊seconds/90⌋)` packed together (4 at the start, 9 from 7:30 on). On stages that have Piranhas (Riff, Kelp, Vulkan), a **Piranha-Ring** hits at 2:00 and then every 100 s (postponed while a boss is alive): 12 Piranhas appear evenly spaced on a circle just outside the screen and close in all at once, announced by a banner.

**Elites:** from 3:00 on, roughly every 55 s the next regular spawn (a Piranha school never counts) becomes an **Elite**: gold ring, ×3 HP, ×1.25 damage, ×1.3 size, ×4 XP, and +3 extra pearls when it dies.

**Pearl drops:** a regular enemy drops a pearl only 32% of the time. Bosses always drop 8–13 (Section 4).

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

**Boss attacks.** Every boss has its own signature move, and all of them share the heavy shot (plus a radial burst from their second appearance on). Each signature move is telegraphed, so it can always be dodged by moving. None of them can be stopped by the Bubble Ring, a charged Schutzschild absorbs one hit, Panzerung reduces the damage, and the usual 0.5 s of i-frames apply.

| Boss | Signature move | How it plays |
|---|---|---|
| **Hai-König** | **Sturmangriff** (charge) | When you're within 650 units it stops and shows a red lane for 0.9 s (it keeps aiming at you for the first 0.6 s, then locks — sidestep at the end), then charges down the lane at 600 units/s for 0.6 s (~360 units) with normal contact damage. Afterwards it is **tired** for 1.4 s: it crawls at 25% speed and takes **+30% damage** — your window to hit back. The next charge comes 6.5 s after it recovers. |
| **Riesenkrake** | **Tentakelschläge** (slams) | When you're within 750 units, every 5.5 s: marks 3 purple circles (radius 52; +1 per repeat appearance, max 5) — one where you're heading, the others 110–280 units around you. After 1.1 s each one slams for 110% of the boss's damage if you're standing in it. |
| **Meeresungeheuer** | **Sog** (suction) | When you're within 750 units: 1 s wind-up (blue ring), then 2.4 s of suction that drags you toward the boss at 105 units/s while it stands still — swim away. When the suction ends it fires a ring of 8 ordinary shots (70% damage). The next Sog comes 9 s later. |
| **Lava-Titan** | **Magma-Schockwelle** (shockwave) | When you're within 800 units, every 7 s: 0.9 s wind-up, then an expanding ring (230 units/s, up to a radius of 900) with three evenly spaced gaps about 38° wide. Touching the wall deals the boss's damage once; stand in a gap and it passes through you. |

A signature move fires at the earliest 3.5 s after the boss appears. Below 50% HP its intervals are 25% shorter, and every repeat appearance shortens them by a further 12% of the original (floor: 60%).

**Shared attacks:**
- **Radial burst** — only from a boss's **2nd appearance on**: every 4.5s while you're within 700 units, fires 10 shots in a full circle, each dealing 70% of the boss's damage. These are ordinary shots — your Bubble Ring can destroy them on contact.
- **Heavy shot** — every ~7–8.5s while you're within 800 units, fires one large, slow, glowing red shot dealing 140% of the boss's damage, aimed directly at you. This **cannot** be deflected by the Bubble Ring — only a charged Schutzschild (or simply dodging it, since it travels slowly) will save you from it.

While a boss is alive but off-screen, a red arrow at the screen edge points toward it.

Defeating any boss always drops 8–13 pearls.

---

## 5. Waffen (Weapons)

Every weapon can be leveled 1–5 by picking it (or picking it again) on level-up. Damage figures already include the "+level" scaling but **not** your character's damage multiplier, the Shop damage bonus or the Schlagkraft passive — multiply by all of them to get your real numbers. The level-up cards do that for you and show the final values.

**Reach and targeting:** projectile weapons only fire at enemies within `560 × screen scale` units, where the screen scale is `min(2.4, max(1, longer screen side ÷ 850))` — 1.0 on phones, about 1.6 on a 1366-px laptop, about 2.3 on a 1920-px monitor (capped at 2.4). Projectile speed and lifetime are both stretched by √scale so the shots really reach that far. At scale 1 the reach is about 588 units (Blasenschuss), 616 (Harpune) and 585 (Korallenspeer).

### Blasenschuss (Bubble Shot) — starting weapon
Fires at the nearest enemy in targeting range. The bubble flies in a straight line to where the target was at the moment of firing — it does *not* home in, so fast movers can slip past it. Extra shots fan out about 10° apart. Base cooldown 0.85s.

| Level | Damage | Shots fired |
|---|---|---|
| 1 | 10.4 | 1 |
| 2 | 13.8 | 1 |
| 3 | 17.2 | 2 |
| 4 | 20.6 | 2 |
| 5 | 24.0 | 3 |

### Blasenring (Bubble Ring)
Orbiting bubbles that damage anything they touch (0.3s cooldown per individual enemy) **and destroy ordinary enemy shots on contact** (small deflect burst + sound; it does not heal you). Does not stop bosses' heavy red shots.

| Level | Bubbles | Damage/hit | Orbit radius |
|---|---|---|---|
| 1 | 2 | 9 | 59 |
| 2 | 4 | 12 | 66 |
| 3 | 6 | 15 | 73 |
| 4 | 8 | 18 | 80 |
| 5 | 10 | 21 | 87 |

### Tintenwolke (Ink Cloud)
Pulses from a point trailing 34 units *behind* your current facing direction (not centered on you), rendered as a soft, multi-tinted, drifting cloud. Base cooldown 1.2s. Deals **percentage of the target's max HP**, and slows anything it hits by 35% for 1.5s. Only a fraction of its damage applies to bosses so it can't trivialize them. It ignores your damage multiplier, the Shop damage bonus and Schlagkraft — the percentages below are exactly what it deals, which is why it keeps pace with enemy HP scaling.

| Level | Radius | Damage vs. regular enemies | Damage vs. bosses |
|---|---|---|---|
| 1 | 90 | 10.5% of max HP | 1.58% of max HP |
| 2 | 110 | 13.0% | 1.95% |
| 3 | 130 | 15.5% | 2.33% |
| 4 | 150 | 18.0% | 2.70% |
| 5 | 170 | 20.5% | 3.08% |

### Harpune (Harpoon)
Straight-line piercing shot, aimed down the **line with the most enemies**: the game checks the lane toward each of the 24 nearest enemies in range and fires down the one that would pierce the most (a boss in the lane counts triple; ties go to the nearer lane). Base cooldown 1.1s.

| Level | Damage | Enemies pierced |
|---|---|---|
| 1 | 14.2 | 3 |
| 2 | 18.4 | 4 |
| 3 | 22.6 | 5 |
| 4 | 26.8 | 6 |
| 5 | 31.0 | 7 |

### Elektroschlag (Electric Shock)
Chain lightning. It starts at the nearest enemy within 280 units of you and jumps to the nearest not-yet-hit enemy within 280 units of the previous one (both ranges are stretched by √screen scale on big screens). Base cooldown 1.2s.

| Level | Damage/jump | Max jumps |
|---|---|---|
| 1 | 9.9 | 3 |
| 2 | 12.8 | 4 |
| 3 | 15.7 | 5 |
| 4 | 18.6 | 6 |
| 5 | 21.5 | 7 |

### Korallenspeer (Coral Spear)
Single heavy hit on the **strongest** enemy in range (the one with the most current HP; a boss always takes priority) — the hardest-hitting shot in the game. Base cooldown 1.4s.

| Level | Damage |
|---|---|
| 1 | 31.0 |
| 2 | 40.0 |
| 3 | 49.0 |
| 4 | 58.0 |
| 5 | 67.0 |

### Schwarm-Freund (Swarm Friend)
One (later two) independent companion fish that actively hunt: each one seeks the nearest enemy within 300 units of you, swims in to engage it directly, and fires on it — returning to idle orbit near you when nothing's around, and never wandering more than 300 units away. Each companion claims its own target: the second one skips whatever the first is already hunting, and only when there's nothing else do both attack the same enemy — in which case they keep at least ~34 units apart instead of stacking.

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
| **Lebenskraft** *(formerly Extra-Leben)* | +20 max HP for this run only (and heals you 20 HP each time you pick it) | +20 | +40 | +60 | +80 | +100 |
| **Panzerung** | Flat damage reduction on every hit (min. 1 damage always gets through) | −1.2 | −2.4 | −3.6 | −4.8 | −6.0 |
| **Anziehungskraft** | +pickup radius | +20 | +40 | +60 | +80 | +100 |
| **Angriffstempo** | Reduces cooldowns on Blasenschuss/Tintenwolke/Harpune/Elektroschlag/Korallenspeer (not Ring or Friend, which don't use cooldowns) | −8% | −16% | −24% | −32% | −40% |
| **Glück** | +1 Luck per level (see Luck below) | +1 | +2 | +3 | +4 | +5 |
| **Schutzschild** | Recharge time for a shield charge that fully blocks your next hit — any hit, including a boss's heavy shot | 13.8s | 11.6s | 9.4s | 7.2s | 5.0s |
| **Regeneration** | Continuous healing per second | 0.15/s | 0.30/s | 0.45/s | 0.60/s | 0.75/s |
| **Schlagkraft** | +8% damage on every weapon except Tintenwolke (multiplies with character and Shop damage) | +8% | +16% | +24% | +32% | +40% |

Notes:
- **Lebenskraft is *not* a revive** (it used to be called Extra-Leben, which was misleading). It raises your max HP **for the current run only** — nothing carries over to the next run — and heals 20 HP each time you pick a level of it; it never brings you back from death. The only revive in the game is **Zweite Chance** in the Shop (Section 8).
- **Schutzschild** grants an immediate free charge the moment you first pick it, then recharges on the timer above after each block.
- **Luck** is a shared stat: it comes from your character (Glücks-Blobi starts at +3), the Shop's Glücksbringer (+1 per level), and this passive (+1 per level). Each point of Luck does two things: **+10% pearls from every pearl pickup** (tracked fractionally, so +10% really does mean one extra pearl per ten collected), and **+6% chance that a level-up offers a 4th upgrade card instead of 3** (capped at 60%). When the bonus card appears, the level-up screen says so.
- **There are no healing pickups** (a pickup like that existed briefly and was removed for being too strong). The only HP you regain mid-run comes from Regeneration (continuous) and the one-off +20 heal when you pick Lebenskraft; the Schutzschild blocks a hit but doesn't heal.

---

## 7. Spezialmechaniken (How defense works, tied together)

1. **Ordinary enemy shots** (Anglerfisch, the boss's radial burst, the Meeresungeheuer's closing ring) — blockable by the Bubble Ring on contact.
2. **Heavy boss shots** (the big glowing red ones) — ignore the Ring entirely. Dodge them or have a charged Schutzschild.
3. **Contact damage** from touching an enemy — reduced by Panzerung, avoidable with i-frames (0.5s after any hit) or a charged shield.
4. **Hazards and boss moves** (lava zones, tentacle slams, the Magma-Schockwelle, the Hai-König's charge) — not shots, so the Ring can't touch them. They are all telegraphed and avoided by moving; Panzerung reduces them, a charged Schutzschild absorbs one hit, and i-frames apply (which is why standing in lava hurts about every half second).
5. **Sustain** — there are no healing pickups. Only Regeneration (slow, continuous) and the one-off +20 heal from picking Lebenskraft restore HP; Schutzschild blocks a hit without healing; Zweite Chance (Shop) is the only revive.

**Leveling curve:** the XP needed to leave level *N* is `⌊6 + N × 4.6⌋` (rounded down), so it grows roughly linearly (a bit under 5 XP more needed per level) — for example 10 XP to go from level 1 to 2, 52 XP from 10 to 11 and 121 XP from 25 to 26. Once every weapon and passive is maxed, a level-up gives +5 pearls instead of a card.

**Level-up cards:** each card says exactly what changes, e.g. `Stufe 2 → 3: Schaden 13,8 → 17,2 · Blasen 1 → 2`. A new weapon or passive shows `Neu:` with its level-1 values. Numbers already include your damage multiplier and cooldown bonuses. If you reload the page on the level-up screen, the same cards are restored.

---

## 8. Shop (Permanent Upgrades, bought with banked Perlen)

The price of buying level *N+1* is `base cost × multiplier^N`, rounded — so Lv1 costs the base price (40 for the HP upgrade), Lv2 costs 64, and so on. The last column lists the price of each level in order.

| Upgrade | Effect/level | Max level | Price to buy Lv1 / Lv2 / Lv3 / Lv4 / Lv5 |
|---|---|---|---|
| Grösserer Lebensvorrat | +10 starting max HP | 5 | 40 / 64 / 102 / 164 / 262 |
| Bessere Flossen | +3% starting speed | 5 | 40 / 64 / 102 / 164 / 262 |
| Schärfere Stacheln | +4% weapon damage | 5 | 55 / 94 / 159 / 270 / 459 |
| Perlen-Magnet | +22 pickup radius (base becomes 70 + 22×level) | 5 | 35 / 53 / 79 / 118 / 177 |
| Glücksbringer | +1 starting Luck (more pearls, more often a 4th upgrade card) | 3 | 70 / 126 / 227 |
| Zweite Chance | Revive once per run at 50% max HP | 1 (one-time) | 180 |

Buying everything costs 3,366 pearls in total; after that, pearls have no further use.

**How Zweite Chance works:** it's a one-time, permanent purchase — once bought, every run starts with a revive "armed", shown as a green heart (💚) next to your HP numbers in the HUD. The first time you'd die, you're automatically brought back at 50% max HP with 2 seconds of invulnerability and a "Zweite Chance genutzt!" banner; the heart then disappears for the rest of that run. There's no button to press and it can't be found or picked up mid-run — it has to be bought in the Shop before you start. The revival also blasts enemies within 320 units back out to about 340 units (bosses are shoved 140 units) and wipes all enemy shots, lava zones, tentacle slams and shockwaves, so you don't land back in the same trouble.

These stack with your character's base stats and any in-run passives you pick — they're permanent, applied at the start of every run regardless of character.

---

## 9. Erfolge (Achievements)

| Achievement | Condition | Reward |
|---|---|---|
| Erster Blubb | Defeat your first enemy ever | 10 pearls |
| Blasen-Profi | Defeat 100 enemies total (lifetime) | 25 |
| Ozean-Legende | Defeat 1000 enemies total (lifetime) | 100 |
| Kurzer Tauchgang | Survive 5 minutes in a single run | 40 |
| Tiefseeforscher | Survive 15 minutes in a single run | 150 |
| Königsschlächter | Defeat any boss once | 60 |
| Boss-Bezwinger | Defeat all 4 boss *species* (lifetime) — since each stage has its own boss, this means winning in every stage at least once | 200 |
| Perlensammler | Earn 1000 pearls in total (lifetime) — having 1000 banked at once also counts | 100 |
| Voll entwickelt | Reach level 30 in a single run | 75 |
| Ganze Blobi-Familie | Unlock all 4 characters | 50 |

Each achievement pays its reward **once**, in banked pearls, the moment it unlocks (a banner shows `🏆 Erfolg! +N 💧`, and the Achievements screen lists each reward). All ten together pay 810 pearls. Saves from before rewards existed were paid retroactively, once. "Voll entwickelt" used to need level 20; anyone who already earned it keeps it.

---

## 10. Fortschritt & Speichern (Saving)

- **Between runs:** pearls, Shop levels, achievements, unlocked stages, best stats, and character unlocks save automatically to the browser's local storage every time they change, and persist across sessions once this is live on your actual site. If the browser blocks local storage (private mode, some embeds), the main menu shows a warning, because progress then only lasts until the tab is closed.
- **Mid-run:** the game also snapshots your *current* run — level, weapons, passives, HP, elapsed time, pearls so far, position — whenever the tab is backgrounded, right before the page is hidden, and every ~8 seconds while playing. If the browser discards or reloads the tab (common on mobile after being away a while), the main menu offers a **"Weiterspielen"** button that restores your **progress** instead of losing it: level, XP, weapons, passives, HP, elapsed time, pearls and position all come back. If you were on the level-up screen, you come back to exactly that screen with the same cards and no upgrade is lost. What does *not* come back is the live scene — enemies, projectiles and pickups on screen are cleared, so you resume into open water with 1.5 seconds of invulnerability. If a boss was alive when you left, that same boss encounter restarts at full HP a few seconds after you resume (it does not skip ahead to the next, tougher one).
- **Nothing is thrown away:** quitting via the pause menu, using **Neustart** in the pause menu, and starting a new dive while an old snapshot is waiting all bank the pearls and stats of the run they replace — including the Glücks-Blobi level check — exactly as dying does.
- **Tab switching:** the game pauses automatically when the tab or window loses focus, and it clears any held keys or touch so your fish doesn't keep drifting when you come back.

---

## 11. Steuerung (Controls)

- **Desktop:** WASD or arrow keys to move. ESC or the pause icon to pause (holding ESC no longer flickers the pause on and off).
- **Mobile:** drag anywhere on the screen to move. The first finger down owns the stick; extra fingers or a resting palm are ignored, and lifting a different finger doesn't stop you.
- Attacks on every weapon are fully automatic — the only inputs are movement and which upgrade to pick on level-up.
