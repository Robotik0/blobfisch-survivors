# Blobfisch Survivors — Complete Reference

Every number below is pulled directly from the current game code, not from memory — and the weapon/passive tables below have also been checked against the running game level by level, so this reflects what's shipped right now (including area hazards, boss phases and recurring bosses, per-area pearl rates, the wearing Bubble Ring, the rebalanced Shop, claimable achievements, champions and the online mode with public rooms and team play). Percentages and damage values are shown *before* your character's damage multiplier, Shop bonuses and the Schlagkraft passive are applied, except where noted.

---

## 1. The Blobfische (Playable Characters)

| Character | Unlock | HP | Speed | Damage | Weapon Cooldown | Luck | Sprite behavior |
|---|---|---|---|---|---|---|---|
| **Standard-Blobi** | Available from the start | 100 | 150 | ×1.0 | ×1.0 | 0 | Top-down art — rotates freely to face any direction |
| **Turbo-Blobi** | Available from the start | 75 | 196 | ×0.9 | ×1.0 | 0 | Side-view art — mirrors left/right, tilts up to 90° |
| **Panzer-Blobi** | Available from the start | 145 | 122 | ×1.0 | ×1.05 (5% *slower*) | 0 | Side-view art — mirrors left/right, tilts up to 90° |
| **Glücks-Blobi** | Reach level 25 in one run | 90 | 155 | ×1.0 | ×0.95 (5% *faster*) | +3 | Side-view art — mirrors left/right, tilts up to 90° |

The character-select cards show the real, current numbers (including any Shop bonuses), and the stage cards show their difficulty multiplier and boss. These are *base* stats. Shop upgrades (Section 9) add flat/percentage bonuses on top of whichever character you pick, every run. Players who unlocked Glücks-Blobi under the earlier level-15 rule keep it.

Turbo, Panzer, and Glücks are drawn from the side, so instead of spinning all the way around (which would flip them upside-down), they mirror horizontally once you're heading more than 90° away from their natural facing, and only tilt within that ±90° window. Standard is the only one drawn from directly above, so it turns freely in a full circle.

---

## 2. Gebiete (Stages)

| Stage | Difficulty multiplier | Boss | Unlocked by | Pearls per kill | Area mechanic |
|---|---|---|---|---|---|
| Korallenriff (Coral Reef) | 1.0 | Hai-König | Available from the start | 11% chance × 1 pearl — **×1** | None — a harmless starter stage |
| Kelpwald (Kelp Forest) | 1.35 | Riesenkrake | Defeating the Hai-König | 22% × 1 — **×2** | Kelp patches slow you down |
| Tiefsee-Graben (Deep Trench) | 1.75 | Meeresungeheuer | Defeating the Riesenkrake | 16.5% × 2 — **×3** | Darkness — you only see near you |
| Vulkanschlucht (Volcanic Vent) | 2.2 | Lava-Titan | Defeating the Meeresungeheuer | 22% × 2 — **×4** | Periodic lava zones |

The difficulty multiplier affects how fast regular enemies gain HP/damage over time and how quickly the spawn rate ramps up (see Section 3) — a run in Vulkanschlucht gets harder much faster than the same elapsed time in Korallenriff.

**Pearls per kill:** the chance that a regular enemy drops a pearl, and how many pearls that pearl is worth, depend on the area. The bold factor is the expected pearls per kill compared with the Korallenriff (0.11 → 0.22 → 0.33 → 0.44 per kill), so harder areas pay clearly better. Boss treasure uses the pearl value too (Section 4).

**Unlocking:** every stage after the Korallenriff opens once you defeat the boss of the previous one (in any run, with any character). Locked stage cards show a 🔒 and what to beat. Saves that already had progress when this system arrived keep all four stages open.

**Area mechanics in detail:**
- **Korallenriff — nothing.** No hazards; it's meant for learning the game.
- **Kelpwald — kelp patches.** Fixed patches of swaying kelp (radius 70–130 units; about 4 in every 10 map cells of 380 × 380 units contain one, and none sit near your starting point). While you're inside one, your movement speed is ×0.6 (−40%). This multiplies with the Tintenfisch ink slow, so both together leave you at ×0.33. Enemies aren't slowed.
- **Tiefsee-Graben — darkness.** Everything outside a lit circle around you is dark. The circle's radius is half the shorter screen side, clamped to 230–420 units (and gently pulsing); it is fully clear in the inner 40% and fades to 90% dark at 130% of that radius. XP and pearl orbs, enemy shots, bosses and the Anglerfisch's lure stay visible in the dark.
- **Vulkanschlucht — lava zones.** From 0:12 on, lava erupts around you on a timer: every `max(3.2, 7 − seconds/90)` seconds, `min(3, 1 + ⌊seconds/200⌋)` zones (radius 78) appear. The first is placed where you're heading (0.7 s ahead of your movement), the others 110–340 units away in random directions. Each zone shows a glowing warning circle for 1.5 s, then burns for 3.5 s (the pool darkens as it cools down). Standing in active lava hurts about once every 0.5 s (your i-frames) for `9 × (1 + minutes × 0.10 × 2.2)` damage — Panzerung reduces it and a charged Schutzschild blocks one tick. Lava isn't a shot, so the Bubble Ring can't stop it, and it doesn't hurt enemies. The Lava-Titan adds a few lava zones of its own in its last phase (Section 4).

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

**While a boss is alive** the arena is calmer so you can focus on the duel: each wave brings only half as many regular enemies (rounded up, at least 1), the gap between waves is 1.4× longer, no Elites are created and the Piranha-Ring waits until the boss is dead. (The boss's own helpers are separate, see Section 4.)

**The 70-enemy cap:** at most 70 regular enemies are alive at once. At the cap, a new spawn never deletes anything you can see — it *replaces the farthest enemy that is outside the screen*, and if every enemy is on-screen the spawn is simply skipped. Bosses, elites and champions are never replaced, and a champion appears even when the cap is reached (Section 5).

**Piranha schools and rings:** whenever the spawner picks a Piranha it spawns a whole school of `4 + min(5, ⌊seconds/90⌋)` packed together (4 at the start, 9 from 7:30 on). On stages that have Piranhas (Riff, Kelp, Vulkan), a **Piranha-Ring** hits at 2:00 and then every 100 s (postponed while a boss is alive): 12 Piranhas appear evenly spaced on a circle just outside the screen and close in all at once, announced by a banner.

**Elites:** from 3:00 on, roughly every 55 s the next regular spawn (a Piranha school never counts) becomes an **Elite**: gold ring, ×3 HP, ×1.25 damage, ×1.3 size, ×4 XP, and +3 extra pearls when it dies (each worth the area's pearl value).

**Pearl drops:** a regular enemy drops a pearl with the area's drop chance — Riff 11%, Kelp 22%, Graben 16.5%, Vulkan 22% — and each pearl is worth the area's pearl value: 1 in Riff and Kelp, 2 in Graben and Vulkan (Section 2). Bosses drop a treasure (Section 4). Luck adds +10% per point to every pearl you collect (Section 7).

**Piles of orbs:** XP orbs and pearls that lie far away from you are merged so that huge piles don't slow the game down, and **nothing is ever lost**. Orbs outside the screen simply combine invisibly into one bigger orb (bigger orbs are drawn slightly larger, up to radius 12). If more than 200 orbs are lying around, the ones that are on-screen but more than 60 units beyond your pickup radius no longer vanish: they slowly drift into the nearest orb of their patch and add up when they arrive. As soon as you swim within pickup range, a drifting orb becomes individually collectible again. Hearts never merge.

---

## 4. Bosse

| Boss | Stage | Base HP | Base Speed | Base Damage | XP | Calls for help |
|---|---|---|---|---|---|---|
| Hai-König | Korallenriff | 2,200 | 75 | 20 | 120 | Kleine Haie |
| Riesenkrake | Kelpwald | 2,400 | 58 | 24 | 180 | Quallen |
| Meeresungeheuer | Tiefsee-Graben | 2,500 | 62 | 28 | 250 | Tintenfische |
| Lava-Titan | Vulkanschlucht | 3,200 | 52 | 34 | 340 | Krebse |

**Bosses recur.** The first one shows up 5 minutes into a run (with a 3-second warning banner). Defeat it, and the *next* one — same species, tied to your stage — arrives exactly 4 minutes later, and every subsequent appearance is stronger than the last. This can continue indefinitely as long as you keep surviving.

**How strong a boss is.** Bosses scale with *you*, so they stay a real fight no matter how fast you level:
- HP: `base HP × (1 + (stage difficulty − 1) × 0.5) × (1 + 0.15 × earlier appearances) × level factor`
- Level factor: `(your level ÷ 21)^1.3`, measured at the moment the boss appears and limited to 0.7 – 6. That is ×0.7 up to level 16, ×1.0 at level 21, ×1.6 at level 30, ×2.3 at level 40, ×3.9 at level 60 and the cap of ×6 from level 84 on.
- Damage: `base damage × (1 + 0.2 × earlier appearances)` — so ×1.0, ×1.2, ×1.4, … on the 1st, 2nd, 3rd appearance.

Boss HP on the first appearance (before your damage bonuses):

| Boss | Your level 15 | Level 21 | Level 30 | Level 40 |
|---|---|---|---|---|
| Hai-König | 1,540 | 2,200 | 3,498 | 5,084 |
| Riesenkrake | 1,974 | 2,820 | 4,484 | 6,517 |
| Meeresungeheuer | 2,406 | 3,438 | 5,465 | 7,944 |
| Lava-Titan | 3,584 | 5,120 | 8,140 | 11,832 |

At level 21 the 2nd appearance has 15% more HP than the table (3rd: +30%).

**HUD.** While a boss is alive, its name, a `×N` mark for repeat appearances and its current phase (`Phase 1–3`) appear above a red HP bar with notches at 66% and 33%. If the boss is off-screen, a red arrow at the screen edge points toward it.

**Phases.** A boss fights in three phases: **Phase 1** above 66% HP, **Phase 2** from 66% down to 33%, **Phase 3** below 33%. Each time it enters a new phase:
- A banner announces it ("⚠ … wird wütend!", in Phase 3 "… tobt vor Wut!").
- The boss **roars** for 1.1 s: it stands completely still and fires nothing extra, with expanding rings around it. Then it releases a ring of 12 shots (16 in Phase 3, 60% of its damage, ordinary shots).
- It **calls its helpers** (table above): 3 in Phase 2 and 5 in Phase 3, plus 1 more on the 2nd appearance and 2 more from the 3rd appearance on. Helpers are normal enemies with the usual time scaling and obey the 70-enemy cap.
- Its next signature move can't come sooner than 2.2 s after the roar began.

**Attack tier.** What a boss does depends on its *tier*: `tier = min(3, phase + appearance − 1)`. On its first appearance, tier = phase. A returning boss starts with the attacks of the next phase — the 2nd appearance already fights at tier 2 in Phase 1, and from the 3rd appearance on a boss always uses tier 3. The tier also sets how fast it is and how often it attacks:

| Tier | Boss walking speed | Wait between attacks |
|---|---|---|
| 1 | ×1.0 | ×1.0 |
| 2 | ×1.1 | ×0.85 |
| 3 | ×1.2 | ×0.7 |

On top of that, each earlier appearance shortens the waits by another 8% (this extra shortening stops at ×0.7 of the waiting time). The result for the signature move: 1st appearance ×1.00 / ×0.85 / ×0.70 in Phases 1/2/3, 2nd appearance ×0.78 in Phase 1 and ×0.64 later, 3rd ×0.59, 4th ×0.53, 5th and later ×0.49.

**Signature moves.** Every boss has its own move, and each one is telegraphed so it can always be dodged by moving. The first signature move comes at the earliest 3.5 s after the boss appears. None of them can be stopped by the Bubble Ring (only the *shots* mentioned further down can), a charged Schutzschild absorbs one hit, Panzerung reduces the damage, and the usual 0.5 s of i-frames apply. The table shows the first appearance; the paragraphs below name what returning bosses add.

| Boss | Signature move | Tier 1 | Tier 2 | Tier 3 |
|---|---|---|---|---|
| **Hai-König** | **Sturmangriff** (charge) | One charge | Two charges in a row | Two faster charges, each followed by a fan of 5 tooth shots |
| **Riesenkrake** | **Tentakelschläge** (slams) | 3 slam circles | 4 circles, then a **Tentakelpeitsche** (a line of 6 slams running from the boss to you) | 4 circles, the whip, then 3 more circles — plus a ring of 10 ink shots |
| **Meeresungeheuer** | **Sog** (suction) | Suction, then a ring of 8 shots | Suction, then a ring of 12 and a second ring 0.45 s later | Suction, then a ring of 12, two more rings (a rotating spiral) and a fan of 5 aimed shots |
| **Lava-Titan** | **Magma-Schockwelle** (shockwave) | One wave | A second wave 1.3 s later, gaps turned by 45° | A third wave (turned by 90°) and 2 lava zones |

**Hai-König — Sturmangriff.** When you're within 650 units it stops and shows a red lane for 0.9 s (it keeps aiming at you until the last 0.3 s, then locks — sidestep at the end), then charges down the lane at 600 units/s for 0.6 s (~360 units; 650 units/s, ~390 units in tier 3) with normal contact damage. Between two charges it re-aims for 0.8 s (0.6 s in tier 3). Tier 3 shoots 5 tooth shots in a 52° fan after every charge (50% damage, ordinary shots). Afterwards it is **tired** for 1.4 s (1.2 s in tier 2, 1.0 s in tier 3): it crawls at 25% speed and takes **+30% damage** — your window to hit back. The next charge comes 5.5 s × the wait factor after it recovers.

**Riesenkrake — Tentakelschläge.** When you're within 750 units, every 5.5 s × the wait factor, it marks purple circles (radius 52) — the first where you're heading, the others 110–280 units around you. After 1.1 s each one slams for 110% of the boss's damage if you're standing in it. Salvo size: 3 circles, +1 on the 2nd appearance, +2 from the 3rd on, and +1 more in tier 2 and 3. The follow-up whip and salvo (tier 2–3) start 0.9 s later and 0.85 s apart; the whip's circles (radius 44) warn longer the farther they are from the boss, so the line sweeps toward you. Tier 3 also fires its ink ring (shots at half damage that slow you by 45% for 2.2 s if they hit — Bubble Ring can block them).

**Meeresungeheuer — Sog.** When you're within 750 units: 1 s wind-up (blue ring), then 2.4 s of suction that drags you toward the boss at 105 units/s while it stands still — swim away. When the suction ends it fires its ring (70% damage per shot, ordinary shots) and the follow-up rings/fan; the extra rings come every 0.45 s, each turned a little further. The next Sog comes 9 s × the wait factor later.

**Lava-Titan — Magma-Schockwelle.** When you're within 800 units, every 7 s × the wait factor: 0.9 s wind-up in which three bright lanes show where the gaps will be, then an expanding ring (230 units/s, up to a radius of 900) with three evenly spaced gaps about 38° wide. Touching the wall deals the boss's damage once; stand in a gap and it passes through you. The follow-up waves come 1.3 s apart. In tier 3 two lava zones (radius 78, warning 1.6 s, burning 3.5 s, 30% of the boss's damage per tick) appear as well: one where you're heading, one 130–290 units away.

**Shared attacks:**
- **Radial burst** — from the boss's **2nd appearance on, or as soon as it is in tier 3**: every 4.5 s while you're within 700 units, fires 10 shots in a full circle (12 in tier 3), each dealing 70% of the boss's damage. These are ordinary shots — your Bubble Ring can destroy them on contact.
- **Heavy shot** — the first after 6 s, then every 7–8.5 s × the tier factor (tier 1 ≈ 7–8.5 s, tier 2 ≈ 6–7.2 s, tier 3 ≈ 4.9–6 s) while you're within 800 units: one large, slow, glowing red shot dealing 140% of the boss's damage, aimed directly at you. This **cannot** be deflected by the Bubble Ring — only a charged Schutzschild (or simply dodging it, since it travels slowly) will save you from it.
- While a boss roars it doesn't shoot anything extra.

**Loot.** Defeating a boss drops:
- its XP orb;
- a **heart** that heals 40% of your max HP (hearts are never merged and the Bubble Ring has nothing to do with them);
- a **treasure of 8–13 pearls**, each worth `area pearl value × (2 + appearance number)` — Luck applies on top:

| Appearance | Riff & Kelp (value 1) | Graben & Vulkan (value 2) |
|---|---|---|
| 1st | 3 each → 24–39 pearls | 6 each → 48–78 |
| 2nd | 4 each → 32–52 | 8 each → 64–104 |
| 3rd | 5 each → 40–65 | 10 each → 80–130 |
| 4th | 6 each → 48–78 | 12 each → 96–156 |

Beating a boss for the first time also opens the next area (Section 2) and counts toward the boss achievements (Section 10).

**Champion bosses:** from the 3rd boss of a run on, the boss comes as an angry champion boss with a special trait, more HP and double treasure (Section 5).

**Online:** with other players in the room, bosses come as **world bosses** on the room's schedule, near a random player, with +60 % HP per other player nearby and the average level of the players nearby; every third world boss is a champion boss (Section 13). Alone in a room, bosses work exactly as described here.

---

## 5. Champions

A **champion** is a rare, much tougher version of a normal enemy with one special trait (two late in a run). It is worth hunting: it drops a treasure chest. Champions sit one clear step above the gold-ringed Elites, which stay as they are. The TurboWarp Lite version has the same champions with the same numbers.

**When they come**
- The first champion appears at **4:00**, then one every **120–150 s** (random).
- Never during a boss fight (also not during the 3-second boss warning). After a boss dies, the next champion waits at least 20 s.
- At most **1** at a time before 15:00, up to **2** from **15:00** on.
- It is a random type from the area's current spawn rotation (Section 3), except **Piranha** (too small) and **Seeigel** (can't move). A champion appears even when the 70-enemy cap is full, and the cap never removes one.
- A message announces it ("👑 Champion erschienen: Gepanzerter Riesenkrebs") with a fanfare, and while it is off-screen a small arrow in its trait colour points to it.

**How strong**
- HP: `normal HP at that moment × 8 × level factor`. The level factor is the bosses' one (Section 4): `(your level ÷ 21)^1.3`, limited to 0.7 – 6. Online, the level is the average of the players near the champion, and like every new enemy it gets **+50 % HP for every other player nearby** (Section 13). Online with others in the room, champions come on the room's schedule (Section 13).
- Damage ×1.4, size ×1.5, XP ×10.
- Examples (single-player): a Krebs champion at 4:00 in the Riff at level 15 has 285 HP (a normal Krebs: 51); a Muräne champion at 10:00 in the Kelpwald at level 30 has 701 HP; a Riesenkrebs champion at 15:00 in the Tiefsee-Graben at level 45 has about 11,000 HP and hits for 76.
- One random trait before 15:00, two different ones from 15:00 on.

**Traits**

| Trait | Colour | What it does | How to beat it |
|---|---|---|---|
| **Flink** (fast) | cyan | 60 % faster. Every 4 s (the first after 2–4 s), when you're within 520 units, it **flashes for 0.6 s** — a cyan ring and a lane show where it will go; it keeps aiming at you until 0.2 s before — then **dashes** for 0.35 s at 480 units/s (about 170 units). | Sidestep when it flashes. |
| **Gepanzert** (armoured) | grey | A **shell** of six plates blocks **60 %** of all damage until the champion has lost 30 % of its HP; then the shell cracks (with a sound and a puff) and it takes full damage. | Strong single hits: Korallenspeer, Harpune. |
| **Vampir** | red | Heals **10 % of its max HP** every time its touch costs you HP (a blocked hit — Schutzschild — doesn't heal it). | Keep your distance. |
| **Teilend** (splitting) | green | When it dies it **splits into 3 normal enemies** of its type with 1.5× the normal HP (they obey the enemy cap). | Be ready for the split. |
| **Explosiv** | orange | When it dies, a **marked circle** (radius 110) appears where it died and **bursts after 1 s** for 2× its touch damage, once. | Swim out of the circle. |
| **Anführer** (leader) | gold | While it lives, other enemies within 220 units are **25 % faster** and hit **20 % harder** (touch and shots); thin gold lines link them to it. Bosses aren't affected. | Kill it first. |

**Look:** a soft aura in the trait colour, a small crown, and a name tag with its own HP bar, for example "Flinker Krebs", "Gepanzerte Qualle", "Anführer-Hai" or, with two traits, "Teilende, gepanzerte Qualle". The second trait shows as a dashed ring in its colour. In the Tiefsee-Graben champions glow, so they stay visible in the dark.

**Reward:** its XP orb (×10 XP) and a **treasure chest** with **12 × the area's pearl value**: 12 pearls in the Riff and the Kelpwald, 24 in the Tiefsee-Graben and the Vulkanschlucht. Luck applies (+10 % per point). Chests are never merged with other pickups.

**Champion bosses:** from the **3rd boss encounter** of a run on, the boss arrives as a **champion boss**:
- one trait: Flink (the boss walks 35 % faster), Gepanzert, Vampir or Anführer;
- **"wütend"**: it roars as soon as it arrives and fights in Phase 2 from the start (it can still reach Phase 3); the message reads "👑 Champion-Boss: … – wütend von Anfang an!", the HUD name gets a 👑, and a rotating dashed ring in its trait colour surrounds it;
- HP ×1.3 on top of the normal boss scaling (Section 4);
- reward: **double pearl treasure** (each of the 8–13 pearls is worth twice as much), the usual heart, and a chest with a **free upgrade card**: a normal level-up choice ("🎁 Schatztruhe!") that costs no XP. If a level-up and a free card are waiting at the same time, the level-up comes first.

**Achievements:** Champion-Jäger (defeat 25 champions, +60 pearls) and Kronenbrecher (defeat a champion boss, +120), see Section 10.

**How much they add (measured).** Bot runs of 20 minutes with and without champions, same seeds: in the Korallenriff the bot defeated about 5.4 champions and 0.8 champion bosses per run, which made up about 9–10 % of the run's pearls; in the Tiefsee-Graben about 2 champions, 7 %. No measurable extra levels (the differences stayed within the normal run-to-run spread). Human players who hunt champions get a bit more. The target was 10–15 % of the pearls and at most 1–2 extra levels by 20:00. If champions should feel more rewarding, raise `CHAMPION_CHEST` from 12 to 15.

**Tuning knobs** (all at the top of the game script, next to `BOSS_TYPES`): `CHAMPION_START`, `CHAMPION_GAP_MIN` / `MAX`, `CHAMPION_LATE`, `CHAMPION_HP`, `CHAMPION_DMG`, `CHAMPION_SIZE`, `CHAMPION_XP`, `CHAMPION_CHEST`, `CHAMPION_EXCLUDE`, `CHAMPION_BOSS_FROM`, `CHAMPION_BOSS_HP`, `CHAMPION_BOSS_TRAITS`, the trait table `CHAMPION_TRAITS` and the per-trait numbers `FLINK_*`, `SHELL_*`, `VAMPIR_HEAL`, `SPLIT_*`, `BURST_*`, `LEADER_*`; online `NET_GROUP_HP`.

---

## 6. Waffen (Weapons)

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

**Wear and popping (from ring level 4).** Blocking shots wears the bubbles down — but the ring is safe while you build it up, and you always get the chance to repair it:
- **Levels 1–3: bubbles never pop.** From **level 4** (the second-to-last upgrade) on, every ordinary enemy shot that a bubble blocks counts as one hit on *that* bubble. Heavy boss shots pass through and don't count, and neither does touching enemies.
- A worn bubble turns paler and reddish, shakes and shows cracks (cracks from about 40% wear, more after 70%). A small `⭕ 8/8` counter in the HUD shows your bubbles (it turns warning-colored when some are missing).
- After **12 blocked shots** a bubble pops. Three rules keep this fair: at most **one bubble pops every 50 seconds**; after a pop **no further bubble can pop until a level-up has been offered** (a bubble that is "due" simply waits, one hit short of popping); and when a bubble pops, all the others are relieved to at most half wear (6 hits).
- A banner tells you: the next level-up will let you refill the ring. That level-up **always contains the ring card**, so you never have to hunt for it — but you're free to pick something else; the next pop is then at least 50 s away, and the card is guaranteed again right after that pop (it can also turn up in any level-up as one of the normal random cards).
- **Ring level 4 → 5:** the normal upgrade card is the repair — a new level always comes with a full, undamaged ring.
- **Ring level 5 (maxed):** the card becomes **„Mehr Blasen“** (the "buy more" card). It is free, restores every missing bubble and repairs all cracks (`Blasen 8 → 10 · alle Risse repariert`). It only appears while at least one bubble is missing, so it never clutters the level-up screen at full health.
- Popping is part of the mid-run snapshot, so a resumed run keeps its bubble wear.

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

## 7. Passive Verbesserungen (Passives)

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
- **Lebenskraft is *not* a revive** (it used to be called Extra-Leben, which was misleading). It raises your max HP **for the current run only** — nothing carries over to the next run — and heals 20 HP each time you pick a level of it; it never brings you back from death. The only revive in the game is **Zweite Chance** in the Shop (Section 9).
- **Schutzschild** grants an immediate free charge the moment you first pick it, then recharges on the timer above after each block.
- **Luck** is a shared stat: it comes from your character (Glücks-Blobi starts at +3), the Shop's Glücksbringer (+1 per level), and this passive (+1 per level). Each point of Luck does two things: **+10% pearls from every pearl pickup** (tracked fractionally, so +10% really does mean one extra pearl per ten collected), and **+6% chance that a level-up offers a 4th upgrade card instead of 3** (capped at 60%). When the bonus card appears, the level-up screen says so.
- **Healing:** there are no healing pickups lying around the map (a pickup like that existed briefly and was removed for being too strong). The HP you regain mid-run comes from Regeneration (continuous), the one-off +20 heal when you pick Lebenskraft, and the **heart every boss drops** (+40% of your max HP, Section 4); the Schutzschild blocks a hit but doesn't heal.

---

## 8. Spezialmechaniken (How defense works, tied together)

1. **Ordinary enemy shots** (Anglerfisch, the Tintenfisch ink, and the boss's radial bursts, roar rings, Sog rings, fans, tooth shots and ink ring) — blockable by the Bubble Ring on contact. From ring level 4, every block wears the bubble that took it (Section 6).
2. **Heavy boss shots** (the big glowing red ones) — ignore the Ring entirely. Dodge them or have a charged Schutzschild.
3. **Contact damage** from touching an enemy — reduced by Panzerung, avoidable with i-frames (0.5s after any hit) or a charged shield.
4. **Hazards and boss moves** (lava zones, tentacle slams and the whip, the Magma-Schockwelle, the Hai-König's charge, the Sog pull) — not shots, so the Ring can't touch them. They are all telegraphed and avoided by moving; Panzerung reduces them, a charged Schutzschild absorbs one hit, and i-frames apply (which is why standing in lava hurts about every half second).
5. **Sustain** — Regeneration (slow, continuous), the one-off +20 heal from picking Lebenskraft and the heart from every boss restore HP; Schutzschild blocks a hit without healing; Zweite Chance (Shop) is the only revive.

**Leveling curve:** the XP needed to leave level *N* is `⌊6 + N × 4.6⌋` (rounded down), so it grows roughly linearly (a bit under 5 XP more needed per level) — for example 10 XP to go from level 1 to 2, 52 XP from 10 to 11 and 121 XP from 25 to 26. Once every weapon and passive is maxed (and no bubble is missing), a level-up gives pearls instead of a card: 3 × the area's pearl value (3 in Riff and Kelp, 6 in Graben and Vulkan).

**Level-up cards:** each card says exactly what changes, e.g. `Stufe 2 → 3: Schaden 13,8 → 17,2 · Blasen 1 → 2`. A new weapon or passive shows `Neu:` with its level-1 values. The ring's refill card is called „Mehr Blasen“ and shows `Blasen 8 → 10 · alle Risse repariert`. Numbers already include your damage multiplier and cooldown bonuses. If you reload the page on the level-up screen, the same cards are restored.

---

## 9. Shop (Permanent Upgrades, bought with banked Perlen)

The price of buying level *N+1* is `base cost × multiplier^N`, rounded. The last column lists the price of each level in order.

| Upgrade | Effect/level | Max level | Base cost × multiplier | Price to buy Lv1 / Lv2 / Lv3 / Lv4 / Lv5 |
|---|---|---|---|---|
| Grösserer Lebensvorrat | +10 starting max HP | 5 | 40 × 2.0 | 40 / 80 / 160 / 320 / 640 |
| Bessere Flossen | +3% starting speed | 5 | 35 × 1.9 | 35 / 67 / 126 / 240 / 456 |
| Schärfere Stacheln | +4% weapon damage | 5 | 55 × 2.1 | 55 / 116 / 243 / 509 / 1,070 |
| Perlen-Magnet | +22 pickup radius (base becomes 70 + 22×level) | 5 | 35 × 1.9 | 35 / 67 / 126 / 240 / 456 |
| Glücksbringer | +1 starting Luck (more pearls, more often a 4th upgrade card) | 3 | 70 × 2.4 | 70 / 168 / 403 |
| Zweite Chance | Revive once per run at 50% max HP | 1 (one-time) | 300 | 300 |

Buying everything costs 6,022 pearls in total (1,240 + 924 + 1,993 + 924 + 641 + 300); after that, pearls have no further use. (Before the rebalance the total was 3,366; the prices now go together with the per-area pearl rates from Section 2.)

**How Zweite Chance works:** it's a one-time, permanent purchase — once bought, every run starts with a revive "armed", shown as a green heart (💚) next to your HP numbers in the HUD. The first time you'd die, you're automatically brought back at 50% max HP with 2 seconds of invulnerability and a "Zweite Chance genutzt!" banner; the heart then disappears for the rest of that run. There's no button to press and it can't be found or picked up mid-run — it has to be bought in the Shop before you start. The revival also blasts enemies within 320 units back out to about 340 units (bosses are shoved 140 units) and wipes all enemy shots, lava zones, tentacle slams and shockwaves, so you don't land back in the same trouble.

These stack with your character's base stats and any in-run passives you pick — they're permanent, applied at the start of every run regardless of character.

---

## 10. Erfolge (Achievements)

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
| Champion-Jäger | Defeat 25 champions (lifetime) | 60 |
| Kronenbrecher | Defeat a champion boss | 120 |

**Achievements are unlocked automatically, but you collect the reward yourself.** All twelve together pay 990 pearls. Online, defeating an enemy together counts for every player who hit it (Section 13).
- When a condition is met, the achievement is **unlocked** and a banner points you to the menu. Nothing is paid yet.
- On the Achievements screen a waiting achievement shows a gold **NEU** tag, a 🎁 icon and a button **„Einlösen“ (+N 💧)**. Click it to collect the reward — the pearls count up into your balance. Two or more waiting? An **„Alle einlösen · +N 💧“** button at the top collects them all at once.
- The main menu's Erfolge button carries a red **„N NEU“** badge as long as rewards are waiting.
- The game-over screen lists the achievements you just unlocked (with the NEU tag and the pearls waiting) and offers a **„Erfolge einlösen“** shortcut. If you leave older rewards unclaimed, it reminds you how many are waiting.
- The list is sorted: waiting rewards first, then claimed ones (✓ eingelöst), then the locked ones.
- Every reward can be collected only once. Saves from the previous version, where rewards were paid automatically, keep all those achievements as already claimed — nothing is paid twice and nothing is lost. "Voll entwickelt" used to need level 20; anyone who already earned it keeps it.

---

## 11. Fortschritt & Speichern (Saving)

- **Between runs:** pearls, Shop levels, achievements (unlocked and claimed), unlocked stages, best stats, and character unlocks save automatically to the browser's local storage every time they change, and persist across sessions once this is live on your actual site. If the browser blocks local storage (private mode, some embeds), the main menu shows a warning, because progress then only lasts until the tab is closed.
- **Mid-run:** the game also snapshots your *current* run — level, weapons, passives, bubble-ring wear, HP, elapsed time, pearls so far, position — whenever the tab is backgrounded, right before the page is hidden, and every ~8 seconds while playing. If the browser discards or reloads the tab (common on mobile after being away a while), the main menu offers a **"Weiterspielen"** button that restores your **progress** instead of losing it: level, XP, weapons, passives, HP, elapsed time, pearls and position all come back. If you were on the level-up screen, you come back to exactly that screen with the same cards and no upgrade is lost. What does *not* come back is the live scene — enemies, projectiles and pickups on screen are cleared, so you resume into open water with 1.5 seconds of invulnerability. If a boss was alive when you left, that same boss encounter restarts at full HP a few seconds after you resume (it does not skip ahead to the next, tougher one). The champion timer and a waiting free upgrade card are saved too; champions alive at that moment are gone (the next one comes at least 20 s after you resume). **Online runs** are saved too, with their room, and come back with "Online weiterspielen" (Section 13); their pearls are banked when the run ends, you leave the room, or the saved run is no longer used.
- **Nothing is thrown away:** quitting via the pause menu, using **Neustart** in the pause menu, and starting a new dive while an old snapshot is waiting all bank the pearls and stats of the run they replace — including the Glücks-Blobi level check — exactly as dying does.
- **Tab switching:** the game pauses automatically when the tab or window loses focus, and it clears any held keys or touch so your fish doesn't keep drifting when you come back.

---

## 12. Steuerung (Controls)

- **Desktop:** WASD or arrow keys to move. ESC or the pause icon to pause (holding ESC no longer flickers the pause on and off).
- **Mobile:** drag anywhere on the screen to move. The first finger down owns the stick; extra fingers or a resting palm are ignored, and lifting a different finger doesn't stop you.
- Attacks on every weapon are fully automatic — the only inputs are movement and which upgrade to pick on level-up (a click/tap, or the keys **1–4**).
- **Online:** **Q** opens the quick-message wheel (keys 1–8 pick a message while it's open), **Tab** shows the player list; on touch screens the 💬 button and a tap on the room pill do the same.
- Typing in the name or code field of the "Online spielen" screen never moves the fish or pauses the game.

---

## 13. Online spielen (Beta)

Play together with others: in a **public room** with everyone who is online ("Schnellspiel") or in a **private room** with your friends. Everyone plays their own run — own level, XP, weapons, HP and pearls — but you see each other, fight side by side, rescue each other and each of you gets loot. The game needs the small online server from the folder `blobfisch-online` (its README explains the free Cloudflare setup); until its address is entered in `index.html` (`ONLINE_SERVER`), the online screens say the server isn't set up yet. Single-player is completely unaffected.

**Getting in** — three short screens:
1. Main menu → **🌐 Online spielen**: your **profile**. Type a name (3–12 characters: letters including umlauts, digits, space, `-` and `_`; 🎲 picks a random one like "Blobi482") and pick your Blobi. The top line shows how many players are online right now (refreshed every 10 s while the online screens are open). **Weiter**.
2. **Wie willst du spielen?** — three buttons (plus **🔄 Weiterspielen** when a saved online run is waiting, see below):
   - **⚡ Schnellspiel** — choose an area. The area where most players are right now is preselected (if you have unlocked it), and each area shows how many are playing there. You land in the **fullest public room of that area that still has space**, e.g. "Korallenriff #1", up to **24 players**; when all of them are full a new one opens ("#2"). A public room closes 60 s after its last player has left.
   - **➕ Raum erstellen** — choose an area for a **private room** (up to **8 players**). Your run starts at once; the room's **code** (4 letters, never I, L or O) is shown in a message, in the room pill under the XP bar (`👥 KRBX · 1/8`) and in the pause menu. Give it to your friends. The room stays open for 10 minutes after the last player has left, so you can rejoin with the same code.
   - **🔑 Raum beitreten** — type the code (upper or lower case).
3. You play in the room's area, even if you haven't unlocked it yourself yet (beating a boss there still counts normally).

Names are checked by the server; a name that isn't allowed is replaced by a random one and you're told so. Old random names "Blubbi…" become "Blobi…" automatically.

**The Hafen** — a safe harbour in the middle of every room (radius 250, a dashed circle with an ⚓ sign). Every online run starts inside it with **5 s of protection**. Inside the Hafen enemies can't reach you (they stop at its edge), enemy shots vanish, you take no damage and no lava zones appear — but **your weapons rest** (no shots, the Blasenring doesn't hurt, your Schwarm-Freunde don't shoot) and **no enemies spawn** around you. A hint at the bottom of the screen says so while you're inside. Swim out to fight.

**What is shared**
- **Seeing each other:** every Blobi shows its name, level and a small HP bar and has its own colour ring. You also see your friends' **Blasenring** bubbles, **Schwarm-Freunde** and **shield**; a friend's bubbles block small enemy shots on your screen exactly as in their game. Friends off-screen get a coloured arrow at the screen edge with name and distance (in "m" = 10 world units); the 5 nearest are shown. A **downed** friend always gets a red, pulsing arrow, and world bosses and champions always get one (red / in the trait's colour), even far away. In the Tiefsee-Graben your friends stay visible in the dark.
- **Enemies:** each player's enemies spawn around that player and scale with that player's run time and level, as in single-player. Every enemy chases the **nearest Blobi** — yours or a friend's, but a friend's only while they are within **1,600 units** (about 1.5 screens), so they can always see what chases them. Downed players are never chased; players in the Hafen only when nobody else is in reach (otherwise the enemies wait at the Hafen's edge).
- **Fighting together:** your weapons hit your friends' enemies too; their HP bars drop about a tenth of a second later. Ink-cloud slowing and the Vampir heal work across as well.
- **Loot is personal:** when an enemy dies, **everyone who hit it** gets their own full loot — the XP orb, the chance for a pearl, the Elite pearls, the boss treasure and heart, and a champion's chest (including a champion boss's free upgrade card). Pearls and orbs your friend picks up are still there for you — a one-time hint explains this. Each helper's kill counts for their achievements and statistics, and a boss kill opens the next area for every helper.
- **Taking damage:** your own game decides when you are hit, checking your Blobi against everything you see: your enemies and your friends', their shots, slam and lava zones, explosion circles and magma waves. A friend's Meeresungeheuer pulls you with its Sog when you are within 900 units (never inside the Hafen).

**Stronger in groups:** while other players are near (active, within 1,600 units), every new enemy that spawns around you gets **+50 % HP per other player** — harder through strength, not more enemies. This includes champions (whose level factor then uses the average level of the players nearby, Section 5). A **world boss** gets **+60 % HP per other player** near it when it appears, and its level factor also uses the average level.

**World bosses and room champions:** the player who has been in the room longest (the "anchor") runs the room's clocks; when they leave, the next one takes over with the same clocks. As long as you are **alone in a room**, everything works exactly like single-player (your boss at 5:00, champions from 4:00). As soon as **others are in the room**, your own boss and champion clocks rest and the room's schedule takes over (it starts from the anchor's own clocks):
- **World boss:** when the room's boss clock runs out (5 minutes of room activity, 4 minutes after the previous world boss is gone), a boss appears near a **random player** who is playing and not in the Hafen. The whole room gets a 3-second warning ("⚠ Ein Weltboss erscheint bei Lena!") and a red arrow. **Every third world boss is a champion boss.** Everyone who damaged it gets the treasure and the heart, and the kill counts for unlocking the next area. Near a world boss fewer normal enemies spawn, as in your own boss fight. The player it appeared at plays it; if they leave the room, it disappears and the next one comes 4 minutes later.
- **Room champions:** every 120–150 s (never during a world boss), one champion appears near a random player and is announced to the room ("👑 Champion bei Lena: Flinker Krebs"); at most 1 at a time (2 after 15:00 of the anchor's run). Every helper gets a chest.

**Downed and rescued:** at 0 HP the **Zweite Chance** helps first, if you bought it. Otherwise, if a friend who is playing is within **2,200 units** (about 2 screens), you are **downed for 20 s**: you can't move, attack or collect anything, you take no damage, and enemies ignore you. Your Blobi lies faded inside a red, pulsing ring; a banner shows the seconds left. A friend who stays within **60 units** of you (the dashed circle) for **3 s** rescues you — a green ring fills up on both screens — and you're back with **30 % HP**, 2 s of protection and nearby enemies pushed away, like the Zweite Chance. Both of you get a message. If no friend is within 2,200 units when you drop to 0 HP, or the 20 s run out, your run ends as in single-player.

**Pause and level-ups while friends are near:** if an active friend is within 2,400 units, **ESC** or the pause button opens the pause menu at the bottom of the screen, but **the game keeps running** (it says so); if no friend is near any more, it becomes a real pause. **Level-up cards** slide in as a bar at the bottom: pick with **1–4** or a tap; after **15 s** the first card is taken automatically. Alone, both stop the game as in single-player. Switching to another window counts as pressing pause. **Tab in the background** always pauses: your friends then see you as sleeping — your Blobi and your enemies disappear for them until you're back (💤 in the player list). If a friend's game is really paused, their enemies stand still on your screen in their normal colours; you can still hit and defeat them (their game applies it while paused), but they don't hurt you.

**Quick messages:** **Q** or the 💬 button opens a wheel with 8 messages — 👋 Hallo, 🆘 Hilfe!, 📍 Hierher!, 🙏 Danke!, ⚠️ Boss!, 🎉 GG, 👑 Champion!, 👍 OK — pick with a click/tap or the keys 1–8 while the wheel is open. The message shows as a speech bubble above your Blobi for 3 s; at most one every 2 s. Players who can't see you get it as a message at the top ("💬 Lena: Hilfe!"). There is no free text chat.

**Player list:** **Tab** or a tap on the room pill shows everyone in the room with colour, Blobi, name, level and what they're doing (distance, ⚓ Hafen, ⏸ Pause, 💔 Hilfe!, 💤 schläft, ☠ vorbei).

**Game over, leaving, being away:** your run ends as usual (summary, pearls banked) and your enemies vanish from the others' screens. **"Nochmal eintauchen"** starts a new run at level 1 in the Hafen of the same room. **"Zum Menü"** (also in the pause menu) leaves the room. After **5 minutes without any key, click or touch** you leave the room automatically and continue alone (your place in the room is free again).

**Reloading the page:** online runs are saved every ~8 seconds like single-player runs, together with their room. After a reload the main menu shows **"🌐 Online weiterspielen · Korallenriff #1 · Lv 12 · 8:30"** (the same button is on the "Wie willst du spielen?" screen). It takes you back into the same room with your level, XP, weapons, passives, HP, pearls and time; you start in the Hafen with 5 s protection (enemies and pickups of that moment are gone). Joining the same room with its code or through Schnellspiel restores the run too. If the private room no longer exists, you continue in Schnellspiel of the same area. A saved online run is kept for 30 minutes; starting a new online run elsewhere ends it — in both cases its pearls are banked. If you were downed when the page closed, the run counts as over (pearls banked).

**Connection problems:** if the connection drops, the game keeps running alone and reconnects by itself (up to 4 tries); if that fails, you continue alone (and the run can be resumed like a single-player run). Messages explain wrong codes ("gibt es nicht"), full rooms (Schnellspiel simply finds another room), an unreachable server, **"Der Online-Modus ist für heute voll"** (the server's free daily limit is used up; it resets at 00:00 UTC, which is 1:00 or 2:00 at night in Switzerland — the message shows the local time) and an outdated page ("Bitte lade die Seite neu").

**Technical numbers** (for tuning): the game sends its state **10 times per second** while another player is within 2,400 units (or one of your enemies is near them), **6.7 per second** when more than 6 players are on one screen and **5 per second** with more than 12; **once per second** when everyone is far away, every 2 s while paused or on the game-over screen, and **nothing at all while you're alone in the room** (the room then sleeps and costs nothing). Friends and their enemies are shown 130 ms in the past so they move smoothly (in a crowd, the time between their messages plus 30 ms, at most 300 ms). A friend who sends nothing for 3.5 s counts as asleep. Values from other players are capped (damage per hit 1,000, XP per kill 1,000). A message is about 0.5–1.5 KB. Measured: two players together send about 10 messages and 5–10 KB per second each; four players together about 14 KB/s up and 41 KB/s down each; 24 players on one screen about 82 KB/s down each (bot test against the real server software). Knobs in `index.html`: `ONLINE_SERVER`, `NET_NEAR`, `NET_LIVE`, `NET_TICK_NEAR` / `FAR` / `IDLE`, `NET_CROWD`, `NET_DELAY`, `NET_ASLEEP`, `NET_GROUP_HP`, `WORLD_BOSS_HP`, `WORLD_BOSS_GAP`, `HAFEN_R`, `HAFEN_PROTECT`, `DOWN_TIME`, `DOWN_NEAR`, `REVIVE_R`, `REVIVE_TIME`, `REVIVE_HP`, `LVLBAR_TIME`, `QUICK_MSGS`, `QUICK_SHOW`, `QUICK_GAP`, `Net.afk`, `ONLINE_SNAP_TTL`; in the server's `room-core.js`: `CAP_GLOBAL`, `CAP_PRIVATE`, `ROOM_TTL_MS`, `GLOBAL_TTL_MS`, `REPORT_EVERY_MS` and the name lists.
