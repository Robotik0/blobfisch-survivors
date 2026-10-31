# Blobfish Survivors — Complete Reference

Every number below is pulled directly from the current game code, not from memory — and the weapon/passive tables below have also been checked against the running game level by level, so this reflects what's shipped right now. **Version 5 (2026-10-25)** changed a lot: progress now runs through the areas (Shop tiers open with the bosses of the deeper areas, Blobis are unlocked and then bought), every boss drops a treasure chest, Zweite Chance is a button you press, a late-game flood ends long runs, lava burns enemies, champions and bosses have new detailed, animated art (champion bosses even more, and they are bigger) while normal enemies and the backgrounds keep their simple look, and online play has shared loot and a PvP mode. Percentages and damage values are shown *before* your character's damage multiplier, Shop bonuses and the Schlagkraft passive are applied, except where noted. **Version 6 (2026-10-30)** is about online play and polish: the game is now called **Blobfish Survivors** (English spelling, to match "Survivors"), it speaks **German, English and Ukrainian** (toggle on the start menu, Section 16), online rooms have a **Leitfisch** who can call the swarm to him, PvP is **team Blau against team Rot** with far fewer enemies, champions are harder (and shoot), "Zum Menü" saves the run, and there are new sounds, smoother frame pacing on fast phone screens, better multi-touch and several online fixes. **Version 7 (2026-10-31)** adds the PvP mode **Jeder gegen jeden** (free-for-all) next to team PvP, rebuilds the online menus as short steps with two choices each, replaces the crowded points line in online play with a small labelled **score card**, keeps arrows, labels, toasts and the player list from overlapping, shows **progress bars** for every achievement, gives the game-over screen one clear next step, and reworks the **sounds** (Section 14). The TurboWarp Lite version still has the version 3 rules; Section 15 lists the differences.

---

## 1. The Blobfische (Playable Characters)

| Character | Unlock | Price | HP | Speed | Damage | Weapon Cooldown | Luck | Sprite behavior |
|---|---|---|---|---|---|---|---|---|
| **Standard-Blobi** | Available from the start | — | 100 | 150 | ×1.0 | ×1.0 | 0 | Top-down art — rotates freely to face any direction |
| **Turbo-Blobi** | Defeat the Riesenkrake (Kelpwald) once | 700 | 75 | 196 | ×0.9 | ×1.0 | 0 | Side-view art — mirrors left/right, tilts up to 90° |
| **Panzer-Blobi** | Defeat the Meeresungeheuer (Tiefsee-Graben) once | 1,500 | 145 | 122 | ×1.0 | ×1.05 (5% *slower*) | 0 | Side-view art — mirrors left/right, tilts up to 90° |
| **Glücks-Blobi** | Reach level 25 in one run | 2,500 | 90 | 155 | ×1.0 | ×0.95 (5% *faster*) | +3 | Side-view art — mirrors left/right, tilts up to 90° |

**Unlock, then buy.** At the start only the Standard-Blobi is playable. When you meet a Blobi's condition it becomes *unlocked*: a message tells you, and the menu shows a **NEUER BLOBI** badge until you have looked at it. Then you buy it in the Blobi selection with banked pearls (the card shows the price; the first tap asks, the second tap buys). The prices add up to 4,700 pearls. Saves from before version 5 keep every Blobi they already had, and players who unlocked Glücks-Blobi under the earlier level-15 rule keep it.

The character-select cards show the real, current numbers (including any Shop bonuses), and the stage cards show their difficulty multiplier and boss. These are *base* stats. Shop upgrades (Section 9) add flat/percentage bonuses on top of whichever character you pick, every run.

Turbo, Panzer, and Glücks are drawn from the side, so instead of spinning all the way around (which would flip them upside-down), they mirror horizontally once you're heading more than 90° away from their natural facing, and only tilt within that ±90° window. Standard is the only one drawn from directly above, so it turns freely in a full circle.

---

## 2. Gebiete (Stages)

| Stage | Difficulty multiplier | Boss | Unlocked by | Pearls per kill | Boss treasure (1st) | Area mechanic |
|---|---|---|---|---|---|---|
| Korallenriff (Coral Reef) | 1.0 | Hai-König | Available from the start | 10% chance × 1 pearl — **×1** | 25 | None — a harmless starter stage |
| Kelpwald (Kelp Forest) | 1.35 | Riesenkrake | Defeating the Hai-König | 25% × 1 — **×2.5** | 60 | Kelp patches slow you down |
| Tiefsee-Graben (Deep Trench) | 1.75 | Meeresungeheuer | Defeating the Riesenkrake | 20% × 2 — **×4** | 110 | Darkness — you only see near you |
| Vulkanschlucht (Volcanic Vent) | 2.2 | Lava-Titan | Defeating the Meeresungeheuer | 20% × 3 — **×6** | 180 | Lava pools |

The difficulty multiplier affects how fast regular enemies gain HP/damage over time and how quickly the spawn rate ramps up (see Section 3) — a run in Vulkanschlucht gets harder much faster than the same elapsed time in Korallenriff.

**Pearls per kill:** the chance that a regular enemy drops a pearl, and how many pearls that pearl is worth, depend on the area. The bold factor is the expected pearls per kill compared with the Korallenriff (0.1 → 0.25 → 0.4 → 0.6 per kill). The boss treasure (Section 4), champion chests (Section 5), Elite pearls and the pearls for a maxed level-up all scale with the area too, so a deeper area pays several times more for the same time played.

**Why the deeper areas matter (version 5):** the Shop's higher tiers only open once you have beaten the boss of a deeper area (Section 9), Turbo- and Panzer-Blobi are unlocked by those bosses (Section 1), and the deeper areas pay far more pearls. Measured with a bot (`webtest/economy_measure.js`, 22-minute runs): an immortal bot brings home about 500–600 pearls in the Korallenriff without Shop upgrades and 1,000–2,500 in the Vulkanschlucht with tier 2; everything in the Shop and all Blobis cost 23,935 pearls together.

**Unlocking:** every stage after the Korallenriff opens once you defeat the boss of the previous one (in any run, with any character). Locked stage cards show a 🔒 and what to beat. Saves that already had progress when this system arrived keep all four stages open.

**Area mechanics in detail:**
- **Korallenriff — nothing.** No hazards; it's meant for learning the game.
- **Kelpwald — kelp patches.** Fixed patches of swaying kelp (radius 70–130 units; about 4 in every 10 map cells of 380 × 380 units contain one, and none sit near your starting point). While you're inside one, your movement speed is ×0.6 (−40%). This multiplies with the Tintenfisch ink slow, so both together leave you at ×0.33. Enemies aren't slowed.
- **Tiefsee-Graben — darkness.** Everything outside a lit circle around you is dark. The circle's radius is half the shorter screen side, clamped to 230–420 units (and gently pulsing); it is fully clear in the inner 40% and fades to 90% dark at 130% of that radius. XP and pearl orbs, enemy shots, bosses and the Anglerfisch's lure stay visible in the dark.
- **Vulkanschlucht — lava pools.** From 0:12 on, lava erupts around you on a timer: every `max(3.2, 7 − seconds/90)` seconds, `min(3, 1 + ⌊seconds/200⌋)` pools (radius 78) appear. The first is placed where you're heading (0.7 s ahead of your movement), the others 110–340 units away in random directions. Each pool shows a glowing warning circle with cracks for 1.5 s, then burns for 3.5 s as molten lava with a soft glowing edge (it darkens as it cools down). Standing in active lava hurts about once every 0.5 s (your i-frames) for `9 × (1 + minutes × 0.10 × 2.2)` damage (× the late-game flood factor after 15:00, Section 3) — Panzerung reduces it and a charged Schutzschild blocks one tick. Lava isn't a shot, so the Bubble Ring can't stop it. **Lava also burns enemies** standing in it: 30 % of their max HP per second (Elites 15 %, champions 5 %, bosses 1.2 %; the Lava-Titan is immune), so luring enemies through a pool is a real tactic; enemies killed by lava drop their loot as usual. The Lava-Titan adds a few lava pools of its own in its last phase (Section 4).

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

**Pearl drops:** a regular enemy drops a pearl with the area's drop chance — Riff 10%, Kelp 25%, Graben 20%, Vulkan 20% — and each pearl is worth the area's pearl value: 1 in Riff and Kelp, 2 in Graben, 3 in Vulkan (Section 2). Bosses drop a treasure chest (Section 4). Luck adds +10% per point to every pearl you collect (Section 7).

**The late-game flood (from 15:00):** a banner says "🌊 Die Flut steigt!", and from then on every minute makes new enemies tougher: HP × 1.22 and damage × 1.12 per minute past 15:00 (compounding, on top of the normal time scaling: × 2.7 HP and × 1.8 damage at 20:00, × 7.3 and × 3.1 at 25:00). Bosses get × 1.105 HP (the square root) and × 1.12 damage per minute, lava × 1.12 damage. The wave size cap grows by one every 2 minutes (5 at 17:00, 6 at 19:00, …) and an Elite comes every 30 s instead of every 55 s. Sooner or later the flood ends every run — the longer you last, the more pearls you take home.

**Look:** normal enemies keep the simple, round blob look: a coloured blob with a face and one feature per type (tentacles, a fin, claws, spikes, a lure). They gently squash as they move, and a hit makes them flash white. The Anglerfisch's lure gives a small, soft light in the dark of the Tiefsee-Graben (much dimmer since version 5). The detailed, animated drawings are reserved for **champions** (Section 5) and **bosses** (Section 4), so a special enemy stands out at a glance. The collision circle is the enemy's radius from the table.

**Piles of orbs:** XP orbs and pearls that lie far away from you are merged so that huge piles don't slow the game down, and **nothing is ever lost**. Orbs outside the screen simply combine invisibly into one bigger orb (bigger orbs are drawn slightly larger, up to radius 12). If more than 200 orbs are lying around, the ones that are on-screen but more than 60 units beyond your pickup radius no longer vanish: they slowly drift into the nearest orb of their patch and add up when they arrive. As soon as you swim within pickup range, a drifting orb becomes individually collectible again. Hearts never merge.

---

## 4. Bosse

### Version 7.2: six bosses per area, every boss with its own attacks

**Which boss comes.** Timing is unchanged (first at 5:00, then 4 minutes after each kill); only the species changes. The 1st boss of a run is one of the area's three *Einstieg* bosses (E); from the 2nd on they come from a shuffled bag of all six (the first is already out of it), no repeat until the bag is empty, then it is shuffled again. Scaling keeps counting *encounters*, not species. Online, the room anchor keeps the room's bag and sends the species with the world-boss call. (Kelpwald, Tiefsee-Graben and Vulkanschlucht still have only their one boss until their new bosses are built.)

**Gates.** Beating **any** boss of an area opens the next area, the Shop tiers and Turbo-/Panzer-Blobi ("Besiege einen Boss im Kelpwald."). "Boss-Bezwinger" now means one boss in each of the four areas.

**Korallenriff: easier, with fewer extras.** Riff bosses have **20 % less HP and damage** than the tables, every boss warning lasts **0.3 s longer**, repeats add **+10 % HP** (not 15 %), waits between attacks shrink to at most **×0.85** (not ×0.7). Tier 1 uses only the signature move and the heavy shot; the burst joins at tier 2, the second move at tier 3, and **tier 3 only from the 3rd boss** of a run. One helper less per phase, none in phase 2 on the first boss. Riff champions and champion bosses only get **Flink, Gepanzert, Teilend** (bosses: Flink, Gepanzert), and a Riff champion boss starts angry (phase 2) only **from the 4th boss**. Elites start at **4:00** (others 3:00), the Piranha-Ring at **3:00** (others 2:00). Rewards are unchanged.

| Boss (Riff) | Group | Base HP | Speed | Damage | Radius | Helpers |
|---|---|---|---|---|---|---|
| Hai-König | E | 2,200 | 75 | 20 | 44 | Kleine Haie |
| Kugelfisch-Kapitän | E | 1,900 | 55 | 18 | 46 | Piranhas |
| Korallenwächter | E | 2,500 | 40 | 22 | 50 | Krebse |
| Mantarochen | | 2,000 | 90 | 20 | 48 | Kleine Haie |
| Anemonen-Zwillinge | | 2 × 1,200 | 85 | 16 | 34 each | Quallen |
| Schatzkrabbe | | 2,100 | 60 | 19 | 42 | Krebse |

All new bosses give 120–130 XP. Every move warns for at least 0.9 s (online at least 1.1 s; Riff +0.3 s). Every boss has a **weak window** (the dazed / tired state with stars) in which it takes **+30 % damage**.

**Own attacks (replace the shared red heavy ball and the plain ring).** The heavy shot comes every 7–8.5 s × phase factor and can't be blocked by the Blasenring; the burst every 4.5 s; the second move every 9–12 s × the boss's wait factor.

| Boss | Heavy shot | Burst | Second move |
|---|---|---|---|
| Hai-König | Kronzahn: a tooth (×1.4 damage) that sticks in the sand for 3 s as an obstacle | Zahnregen: 7 small circles (r 30, ×0.6) in a fan in front of it | – |
| Riesenkrake | Tintenbombe (×1.4, slows) that leaves a black puddle (r 110) hiding everything in it for 3 s | Saugnapf-Salve: one shot from each of 8 tentacle tips, curving | – |
| Meeresungeheuer | Laternenstrahl: slow glowing orb (85/s, ×1.4) | Strömungsring: 14 bubbles in a spiral that curves | – |
| Lava-Titan | Lavabrocken: rock in a high arc, landing circle r 70 (×1.3), then 3 embers | Glutfaust: 9 embers in a cone | – |
| Kugelfisch-Kapitän | Bordkanone: big ball (×1.4) that bounces once (×1.2) | Hutwurf: the hat flies out and back like a boomerang, trailing spikes | Kapitänspfiff: a marked line (1 s), then a tight school of 7 piranhas (×0.6) races along it |
| Korallenwächter | Korallenfels: a boulder rolls 2.1 s and breaks into 6 shards | Splitterkreuz: shards as +, 0.45 s later as × | Riffspur: 7 spike circles (r 40) in a line toward you, each 0.12 s later |
| Mantarochen | Schwanzstachel: fast barb (270/s, ×1.3) | Flügelschlag: sand wave r 300 pushes you up to 150 away (×0.4) and clouds the view | Schattenfalle: its shadow (r 95) around you, it drops onto it 1.2 s later (×1.3) |
| Anemonen-Zwillinge | Anemonenball: thrown from one twin to the other and back (×1.3), hits everything on the line | Halbe-halbe: each fires half of a 16-shot ring, together a ring with one gap | Nesselband: for 4 s a stinging thread between the twins (×0.8): never be between them |
| Schatzkrabbe | Goldmünze: a giant coin rolls at you (×1.4) | Falsche Perlen: 10 fake pearls drift out and pop when touched (real pearls sparkle, fakes don't) | Scherenklau: grabs loot within 300 and heals 1 % per piece; it all comes back when she is beaten |

**Signature moves of the new bosses**
- **Kugelfisch-Kapitän – Aufblähen:** swells for 1 s, then 3 s puffed: double radius, rolls slowly at you, takes only **30 %** damage; then a ring of 12 spikes and 1.5 s out of breath (weak). Tier 2: two rings 0.4 s apart, offset. Tier 3: 4 Seeigel stay behind and it rolls faster while puffed (contact ×2).
- **Korallenwächter – Korallenmauer:** a ring of coral pillars (r 260) around you with **one** lit gap (50°); you can only leave through the gap. After 2.2 s it falls inward (×1.2 to whoever is inside). Then it stands still 1.5 s (weak). Tier 2: gap 35° plus an inner ring (r 150) with its gap opposite. Tier 3: two walls in a row and a coral spear through the gap.
- **Mantarochen – Gleitflug:** rises to the surface (only its shadow, can't be hit), then dives along a marked lane 1,200 long (r 50, ×1.2); its tail leaves a stinging stripe for 1.5 s (×0.25). Tier 2: two lanes crossing; tier 3: three, the last aimed where you're heading, each dropping 2 Kleine Haie. Afterwards it rests 1.2 s (weak).
- **Anemonen-Zwillinge:** two bodies on **one HP bar** (each half). They circle you on opposite sides, then dash crossing through the middle (two lanes, ×1.1), then 1 s dizzy (weak). Tier 2: first they plant their anemone (r 110, slows you, 5 s). Tier 3: two crossings, then a ring from each. If one twin falls, the other goes **wild 8 s later** (+50 % speed, heals 2 % of its half per second) — kill them close together.
- **Schatzkrabbe – Muschelversteck:** she buries herself (can't be hit) and 3 chests rise around you (r 220). One is her (a tiny eye blinks); the others are traps that burst (r 100, ×1.2, 1 s warning) when hit or touched. Hitting the real one knocks her out for 2 s (weak). Tier 2: 4 chests, shuffled once; tier 3: 5 chests, shuffled twice, pearl bombs from the hideout. After 8 s she comes out by herself. Her Boss-Schatz is **+25 %**.

**Kelpwald (7.2)** — the bosses use the kelp; **Tiefsee-Graben (7.2)** — the bosses play with the darkness and with where you stand.

| Boss | Area | Group | Base HP | Speed | Damage | Radius | Helpers |
|---|---|---|---|---|---|---|---|
| Riesenkrake | Kelpwald | E | 2,400 | 58 | 24 | 51 | Quallen |
| Giftkugelfisch | Kelpwald | E | 2,200 | 55 | 22 | 48 | Piranhas |
| Tang-Schrat | Kelpwald | E | 2,600 | 45 | 23 | 52 | Seeigel |
| Seeschlangen-Königin | Kelpwald | | 2,500 | 95 | 24 | 30 (head) | Muränen |
| Hummer-General | Kelpwald | | 2,700 | 50 | 27 | 54 | Krebse |
| Seepferdchen-Ritter | Kelpwald | | 2,300 | 80 | 25 | 44 | Kleine Haie |
| Meeresungeheuer | Graben | E | 2,500 | 62 | 28 | 57 | Tintenfische |
| Panzerassel | Graben | E | 2,800 | 55 | 27 | 54 | Riesenkrebse |
| Tiefseelaterne | Graben | E | 2,300 | 50 | 26 | 50 | Anglerfische |
| Abgrund-Seeschlange | Graben | | 2,700 | 100 | 28 | 30 (head) | Muränen |
| Vampirkalmar | Graben | | 2,400 | 70 | 26 | 50 | Tintenfische |
| Schlinger | Graben | | 2,600 | 65 | 30 | 58 | Muränen |

XP: Kelpwald bosses 180–190, Graben bosses 250–260.

- **Giftkugelfisch:** Aufblähen as in the Riff; when it pops, 6 **poison clouds** (r 60, 4 s) appear around it: they slow like kelp and sting once per second (15 % of its damage). Own attacks: Giftblase (bursts into a poison cloud), Stachelspirale (a turning spiral of 12 spines), Giftatem (4 poison clouds in a cone over 2 s).
- **Tang-Schrat — Wurzelgriff:** sinks (can't be hit), bubbles mark the kelp patch where it comes up 1 s later (near you), then roots burst under you (r 70, warning): if they hit you, you're held for **0.8 s**. Every 12 s it grows a new kelp patch (r 90, 20 s) where you're heading. Tier 2: two jumps, the roots as a line of 3 circles. Tier 3: two copies of Seeigel appear in other patches (1 HP each, dim eyes). Weak 1.5 s after surfacing. Own attacks: Samenkapsel (a Seeigel grows where it lands), Blätterwirbel (10 curving leaves), Rankenpeitsche (7 circles in an arc around it).
- **Seeschlangen-Königin — Würgegriff:** 12 body segments follow her head; the head takes full damage, **the body 25 %** (contact with the body hurts too, ×0.6). She closes a ring of her body around you (r 300 → 80 in 3 s, tier 2: 2.3 s) with a 60° lit gap between head and tail; you can't cross the body elsewhere; whoever is inside at the end is squeezed (×1.2). Tier 2: 3 venom shots into the gap; tier 3: two rings, the second turned 180°. Weak 1.2 s after. Own attacks: Giftspucke (sticky slowing puddle), Schuppenregen (every segment sheds a scale outward), Schwanzhieb (the tail slams a marked spot, r 70).
- **Hummer-General — Scherenzange:** two claw lanes left and right (0.9 s), then they snap (×1.1) and he is stuck for 1 s (weak). Tier 2: then a grab lane: if it hits you, you are pulled up to 150 toward him. Tier 3: two snaps. Every 15 s a **formation** of 6 (tier 2: 8) Krebse with shields marches across the screen (shield in front blocks 60 %); tier 3 from two sides. Own attacks: Feuer frei! (a shell lands on a circle r 64, ×1.4), Knackwelle (7 shots in a cone), Schildwall (soldiers march in and he takes only 50 % until one of them falls).
- **Seepferdchen-Ritter — Lanzenritt:** a curved charge: the bending path shows for 1 s (×1.1), then he rides it at 520/s and plants the lance: a ring of 8 shots. Tier 2: two charges, curving the other way; tier 3: then a line of 5 Kleine Haie sweeps across in a straight lane. Weak 1.3 s (pulling out the lance). Own attacks: Lanzenwurf (boomerang lance), Fanfare (11 bubbles in a forward wave), **Ehrenduell** (a circle r 300 around both of you for 6 s: inside he takes +30 %, leaving it costs you 20 % HP once).
- **Panzerassel:** front and sides armoured: hits from the front half deal **40 %**, hits into the glowing back **150 %** (on its back during the weak window: 150 % from everywhere). **Kugelroll:** rolls into a ball (1 s), rolls at you and turns toward you after each bounce (3 bounces, tier 2: 5 and faster), then 1.5 s on its back. Tier 3: the shell splits into 3 rolling balls and the soft body spits a ring. Own attacks: Plattenwurf (a curving discus), Sandtritt (9 shots kicked out *backward*), Igel-Konter (curls up for 1.5 s and throws your shots back).
- **Tiefseelaterne — Lichtfalle:** your light shrinks to **55 % for 6 s**; 3 lanterns (tier 2: 4, tier 3: 5) hang around you: one is the real lure and pulls you slowly toward it, the others burst after 2 s (r 90, ×1.1). Afterwards it re-lights its lantern (weak 2.5 s). Every 15 s **Blendung**: its eyes glow white for 1 s; if you are *facing* it when it flashes, your light is 40 % for 3 s. Tier 3: it is invisible except for its lure until hit. Own attacks: Hexenlicht (a slow lantern flame that lights the dark around it), Leuchtsporen (9 wobbling spores), Schattenhände (6 hands rise around you, only visible in your light).
- **Abgrund-Seeschlange:** the same Würgegriff, black with blue spots; 0.6 s before the ring starts, its head flashes; in phase 3 the gap moves around the ring. Own attacks: Lichtfresser (a puddle of total darkness), Funkenkette (every segment fires a shot, head to tail), Tiefenruf (vanishes and surfaces under you after a 1.2 s glowing circle, ×1.3).
- **Vampirkalmar — Lebensband:** after a 1 s thin line, a red tether holds you for 6 s and drains **4 % of your max HP per second** while it heals 1.2 %/s; swim **more than 420** away to break it — then it is stunned 1.3 s (weak). Every 10 s it turns its cloak inside out (1 s warning): spikes (contact ×1.6) and it can't be hit from the front for 2 s. Tier 2: a slowing glowing mucus cloud; tier 3: it also eats an enemy near it to heal 5 %. Own attacks: Bluttinte (heals it 3 % if it hits), Netzmantel (12 slowing shots), Kalmarbrut (3 baby squids: each one that hits clings and drains 1 %/s until you swim fast for 1.5 s).
- **Schlinger — Verschlucken:** a lane in front of its mouth (1.1 s), then it lunges. If you're in it, you are **swallowed**: up to 3 s inside, 8 % of your max HP per second, nothing else can hurt you, and **your hits count triple**; after 3 s or when you've dealt 6 % of its HP it spits you out (2 s invulnerable) and coughs for 1.5 s (weak). A charged Schutzschild blocks the swallow. Tier 2: a second lunge if the first misses; tier 3: a suction pull during the warning. Own attacks: Ausspucken (spits an enemy at you), Rülpser (a shockwave that pushes you back), Fressrausch (eats up to 3 nearby enemies: +2 % HP and 10 % bigger each).

**Vulkanschlucht (7.2)** — the bosses fill the screen with hazards; two of them burn in lava (1.2 %/s like other bosses), the others are immune.

| Boss | Group | Base HP | Speed | Damage | Radius | Helpers | Lava |
|---|---|---|---|---|---|---|---|
| Lava-Titan | E | 3,200 | 52 | 34 | 64 | Krebse | immune |
| Vulkanschildkröte | E | 3,500 | 35 | 33 | 66 | Krebse | immune |
| Schwefel-Rochen | E | 2,900 | 95 | 32 | 52 | Piranhas | burns |
| Glutqualle | | 2,800 | 60 | 30 | 52 | Quallen | immune, heals 1 %/s in it |
| Schlotwurm-Kolonie | | 5 × 750 | 0 | 32 | 40 per worm | Tintenfische | immune |
| Feuerfisch-Fürst | | 3,100 | 75 | 35 | 50 | Muränen | burns |

XP 340–350.

- **Vulkanschildkröte — Ausbruch:** the shell rumbles (1 s), then lava bombs fly in high arcs: each landing circle (r 70, ×1.1) becomes a lava pool for 3 s. Tier 1: 4 bombs; tier 2: 7, two aimed where you're heading; tier 3: a ring of 10 around itself, then 4 at you and a heavy shot. **Umkippen:** deal 8 % of its HP within 4 s while it erupts and it tips onto its back for 2.5 s, taking **+50 %**. Contact pushes you 120 away. Own attacks: Aschebrocken (leaves an ash cloud), Dampfdüsen (6 turning steam jets, 3 waves), Panzerrutsch (slides down a lane, ×1.2, leaving a lava stripe for 3 s).
- **Schwefel-Rochen:** Gleitflug like the Mantarochen, but the lane keeps burning for 3 s as a lava stripe (×0.35). Own attacks: Schwefelbombe (a yellow cloud that dims the view), Glutflügel (embers in two arcs), Schwefelregen (7 drops across a marked band).
- **Glutqualle — Glutnetz:** trails burning threads behind it; every 8 s it links up to 3 lava pools (tier 2: 5) with burning lines (0.9 s warning, 3 s, ×0.4). Standing in lava heals it 1 %/s — pull it away. Tier 2: an electric pulse (r 180, 1 s warning), then 1.5 s dim (weak). Tier 3: two small Glutquallen (6 % of its HP each). Own attacks: Feuertropfen (a landing circle r 60, ×1.3), Kettenblitz (lightning lanes to the nearest pools and then to you), Hitzewelle (every lava pool grows 30 % for 4 s).
- **Schlotwurm-Kolonie:** five worms in vents around you (r 350), each with its own HP (750 base), one shared bar; the colony itself can't be hit. Only 2 worms are up at a time (tier 2: 3); a worm that pops up is dazed 1 s (weak). **Geysirfeld:** a vent glows (1 s) and blows a steam column (r 80) that pushes you away and hides the spot for 2 s (tier 2: two at once). A beaten worm leaves a lava pool. Tier 2: the worms spit fire; tier 3: the last two worms move to new vents every 6 s. Own attacks: Magmaspucke (a magma glob in a high arc), Schlotblasen (lava bubbles from every vent), Tunnelbiss (a worm bursts out under you after a 1.1 s circle).
- **Feuerfisch-Fürst — Giftfächer:** spreads its fins (0.9 s), then two fans of 9 spines over 100°, the second offset by half a gap; then 1.2 s folded (weak). Tier 2: then a spiral of 16; tier 3: fans in three directions. **Wiedergeburt (once):** at 0 HP it becomes a glowing egg for 6 s with 15 % of its HP: break it and it's dead, otherwise it hatches with 30 % HP and tier 3 attacks (tier 3: the egg also calls 3 Muränen). Own attacks: Königsstachel (a fast flaming javelin), Umhangschwung (13 embers over the half circle in front), Hofstaat (two small guards with 5 % of its HP each copy its fans at half strength).

### Legenden-Bosse (version 7.2, online COOP only)

- **When:** in a COOP room (public or private) with at least **6 active players**, a Legende takes the place of a world boss when the room's world-boss clock runs out — first after **12:00** of room activity, then at most once every **25 minutes**. With fewer players a normal world boss comes.
- **Warning:** 60 s for the whole room ("🌟 Eine Legende erwacht!"), a golden marker with a countdown and a gold edge arrow at the middle of the active players (moved out of the Hafen).
- **Arena:** a glowing current ring (r **1,000**) around that point. You can swim in and out; inside, no normal enemies spawn (the Legende brings its own adds every 15 s), and champions and world bosses wait. Downed / rescue and the Zweite Chance work as usual.
- **Strength:** HP = area base × (1 + 0.85 × (participants − 1)) × level factor of the participants' average level; more HP is added at each phase change if more players joined. Area base: Riff 18,000 · Kelpwald 24,000 · Graben 30,000 · Vulkan 40,000. Four phases at 75 / 50 / 25 % HP. **Enrage at 10:00:** the arena floods with the area's hazard and the Legende dives away 20 s later.
- **Rewards** (for whoever was in the arena at least half the fight or dealt 2 % of its HP): **Legenden-Schatz** = 10 × the area's boss treasure (250 / 600 / 1,100 / 1,800 pearls) with a free upgrade card, a second free card and a heart; the first kill per area gives a **badge** shown next to your name on the name tag and in the player list (🪸 Riff, 🍃 Kelp, 👁️ Graben, 🔥 Vulkan). A failed attempt gives everyone in the arena a small chest (2 × the boss treasure). Achievements: **Legendenjäger** (any Legende, 200) and **Legendär** (all four, 800).

| Legende | Damage | Phase 1 | Phase 2 | Phase 3 | Phase 4 |
|---|---|---|---|---|---|
| **Atollon, der Riffkoloss** (Riff) | 28 | **Korallentürme:** 1 tower per 3 participants (2–6) at the arena edge, each with 8 % of its HP and shooting at the nearest player; while any stands, Atollon takes only **25 %** | **Ebbe und Flut:** every 20 s a current crosses the arena for 4 s (2 s warning, 80 units/s); hide behind one of 5 coral rocks; the towers regrow once | **Perlenschild:** a giant pearl lands in a circle (r 130, 3 s): 250 % of a max HP shared between everyone inside | **Riffbruch:** the reef breaks off, the arena shrinks to r 650 in 30 s, the shell takes +40 %, tide and pearl come faster |
| **Die Tangmutter** (Kelpwald) | 32 | **Köpfe:** 2 + 1 per 4 participants (max 7), each 6 % of its HP; the body can only be hit with no heads left; a cut head regrows as two after 4 s **unless a neighbouring head is cut within 4 s** | **Rankenband:** every 25 s players are paired by a vine (2 s warning): more than 350 apart costs 30 % max HP and roots you 1 s | **Sporenregen:** 1 player per 4 marked for 4 s; when it bursts everyone within 200 of them is slowed for 4 s and stung | **Wilder Wald:** kelp slows everywhere in the arena except on 3 slowly turning glowing paths; heads regrow only once |
| **Abyssos, das Auge der Tiefe** (Graben) | 36 | **Der Blick:** the eye glows (2 s); whoever *faces* it when it opens loses **60 % max HP** and is blinded 3 s | **Greifarme:** 1 player per 4 grabbed and dragged to the mouth (100/s); the arm has 4 % of its HP — friends must break it; reaching the mouth downs you | **Erlöschen:** your light shrinks to 35 % unless friends are near (+15 % per friend within 250) | **Abgrundsog:** a 5 s pull toward the eye while it opens; the open mouth takes +50 % |
| **Magmaros, der Herz-Vulkan** (Vulkan) | 40 | **Basaltplatten:** the floor turns to lava except 1 plate per 3 participants (min 2); a plate with fewer than 2 players for 5 s sinks for 20 s; the stone hands slam 2 players every 7 s | **Meteorregen:** marked players (red ring, 3 s): stay away from others (60 % to those near, 30 % to the marked); one gold ring: stack on it to share 250 % | **Krustenbruch:** 4 cracks, each must take 5 % of its HP within 12 s, or it seals and Magmaros heals 5 % | **Herzschlag:** the heart is exposed (+50 %) and pulses every 4 s: a magma wave whose gaps turn |

Online: the room anchor calls the Legende (its state rides in the anchor's room clocks `an`), a randomly picked active player hosts it like a world boss (handed over if they leave). Group checks (stack circles 15 % larger, links, marks) are decided by each player's own game from the positions it sees.

**Boss-Album** (main menu): one page per area with six cards — a shadow until you have met the boss, its picture once met, a gold frame once beaten, a crown once beaten as a champion boss. New achievements: Riff-Album komplett 80, Kelp-Album komplett 150, Graben-Album komplett 250, Vulkan-Album komplett 400 (beat all six of the area), Bestiarium 600 (all 24).

### The four original bosses

| Boss | Stage | Base HP | Base Speed | Base Damage | XP | Radius | Calls for help |
|---|---|---|---|---|---|---|---|
| Hai-König | Korallenriff | 2,200 | 75 | 20 | 120 | 44 | Kleine Haie |
| Riesenkrake | Kelpwald | 2,400 | 58 | 24 | 180 | 51 | Quallen |
| Meeresungeheuer | Tiefsee-Graben | 2,500 | 62 | 28 | 250 | 57 | Tintenfische |
| Lava-Titan | Vulkanschlucht | 3,200 | 52 | 34 | 340 | 64 | Krebse |

The radius is the boss's collision circle (10 % larger since version 5); the boss is drawn another 12 % larger than that, so it towers over every normal enemy. A champion boss is another 15 % larger (Section 5).

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
| **Hai-König** | **Sturmangriff** (charge) | One charge | Two charges in a row | Three faster charges, each followed by a fan of 5 tooth shots |
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
- the **Boss-Schatz**, a big treasure chest: `area treasure × (1 + 0.5 × earlier appearances)` pearls, rounded (× 2 for a champion boss, whose chest also holds a free upgrade card). Luck applies (+10 % per point). A light beam rises from the chest, a gold arrow with "💰 Schatz" points to it while it is off-screen, and a message tells you the amount when the boss dies and again when you open it (with a fountain of pearls).

| Appearance | Korallenriff | Kelpwald | Tiefsee-Graben | Vulkanschlucht |
|---|---|---|---|---|
| 1st | 25 | 60 | 110 | 180 |
| 2nd | 38 | 90 | 165 | 270 |
| 3rd (usually a champion boss: × 2) | 50 | 120 | 220 | 360 |
| 4th | 63 | 150 | 275 | 450 |

Chests and hearts never merge with other pickups and are kept when you reload the page mid-run (Section 11). Online, every player near the boss gets their own heart and chest (Section 13).

Beating a boss for the first time also opens the next area (Section 2), unlocks a Blobi or a Shop tier where that boss is the condition (Sections 1 and 9), and counts toward the boss achievements (Section 10).

**Look and animations.** Every boss has a glowing outline in its own colour (pale blue for the Hai-König, magenta for the Riesenkrake, ice-blue for the Meeresungeheuer, orange for the Lava-Titan), a soft aura that grows with each phase and a shadow beneath it — no normal enemy has these, so you can always tell the boss at a glance. Bosses breathe and blink, swim harder when they move, flash and recoil a little when hit, and rise out of the depths when they appear (they grow in with a ring of bubbles). Each one shows its moves before they happen:
- **Hai-König:** pulls back and cocks its tail during the wind-up, stretches into the charge with streaks behind it, sags with half-closed eyes and a slipping crown while tired; its crown jumps when it roars and the big gem glints now and then. Tiger stripes, speckles, a lateral line and a second row of teeth set it apart.
- **Riesenkrake:** eight tentacles spread around it and curl at the tips; for a slam salvo or the whip it raises its outer tentacles and lashes them down; its mantle breathes, ribs and a row of glowing dots line it, and its suckers are drawn as rings.
- **Meeresungeheuer:** puffs up and opens its jaws during the wind-up; during the Sog it trembles, its lantern flickers and streaks of current flow into its mouth. Its comb has rays, its belly folds, and its barbels end in glowing tips.
- **Lava-Titan:** raises both fists high above its head during the wind-up and smashes them down when the magma wave goes off (a ring of dust); burning rocks circle it and smoke rises from its flame crown.

**Defeated** bosses flash white and shake, then the side-view bosses (Hai-König, Meeresungeheuer) roll belly-up while the others tilt and sink; their eyes become crosses, and they fade out in a stream of bubbles over 1.7 s while the treasure lands.

**Champion bosses:** from the 3rd boss of a run on, the boss comes as an angry champion boss with a special trait, more HP, a double treasure chest and a free upgrade card (Section 5).

**Online:** with other players in the room, bosses come as **world bosses** on the room's schedule, near a random player, with +60 % HP per other player nearby and the average level of the players nearby; every third world boss is a champion boss (Section 13). If the player it belongs to leaves, the nearest other player takes it over with all its values. Alone in a room, bosses work exactly as described here.

---

## 5. Champions

A **champion** is a rare, much tougher version of a normal enemy with one special trait (two late in a run). It is worth hunting: it drops a treasure chest. Champions sit one clear step above the gold-ringed Elites, which stay as they are. Version 6 made them clearly harder (more HP, harder hits, a little faster, and they shoot); the TurboWarp Lite version still has the older champions (HP ×8, damage ×1.4, normal speed, no shots, chest 12 ×).

**When they come**
- The first champion appears at **4:00**, then one every **120–150 s** (random).
- Never during a boss fight (also not during the 3-second boss warning). After a boss dies, the next champion waits at least 20 s.
- At most **1** at a time before 15:00, up to **2** from **15:00** on.
- It is a random type from the area's current spawn rotation (Section 3), except **Piranha** (too small) and **Seeigel** (can't move). A champion appears even when the 70-enemy cap is full, and the cap never removes one.
- A message announces it ("👑 Champion erschienen: Gepanzerter Riesenkrebs") with a fanfare, and while it is off-screen a small arrow in its trait colour points to it.

**How strong**
- HP: `normal HP at that moment × 12 × level factor` (×8 until version 5). The level factor is the bosses' one (Section 4): `(your level ÷ 21)^1.3`, limited to 0.7 – 6. Online, the level is the average of the players near the champion, and like every new enemy it gets **+50 % HP for every other player nearby** (Section 13). Online with others in the room, champions come on the room's schedule (Section 13).
- Damage ×1.7, size ×1.5, speed ×1.1, XP ×10 (until version 5: damage ×1.4, normal speed).
- **Fan shot (version 6):** every **3.5 s** (the first after 1.75–3.5 s), when you're within 620 units and it isn't dashing, it fires a fan of **3 shots** at its target, 0.26 rad (about 15°) apart, at 175 units/s, each dealing **55 % of its touch damage**; the shots have its trait colour and live 3.2 s. A Schutzschild blocks them like any enemy shot. Champion bosses don't use it (they have their own attacks).
- Examples (single-player): a Krebs champion at 4:00 in the Riff at level 15 has about 428 HP (a normal Krebs: 51); a Muräne champion at 10:00 in the Kelpwald at level 30 has about 1,050 HP; a Riesenkrebs champion at 15:00 in the Tiefsee-Graben at level 45 has about 16,500 HP and hits for about 92.
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

**Look:** unlike normal enemies, a champion is drawn in full detail and animated (since version 5, 8 frames per loop): the Qualle's bell pulses and its threads drift, the Hai, Anglerfisch, Muräne and Piranha are drawn from the side and face the way they swim (tilting a little up or down), the Krebs and Riesenkrebs walk and snap their claws, the Anglerfisch's lure pulses, the Seeigel's spines sway, the Muräne's spotted body snakes behind it, the Tintenfisch waves its arms and the Piranha snaps; a hit flashes it white. Around it: a soft aura in the trait colour, a small crown, and a name tag with its own HP bar, for example "Flinker Krebs", "Gepanzerte Qualle", "Anführer-Hai" or, with two traits, "Teilende, gepanzerte Qualle". The second trait shows as a dashed ring in its colour. In the Tiefsee-Graben champions glow, so they stay visible in the dark.

**Reward:** its XP orb (×10 XP) and a **treasure chest** with **15 × the area's pearl value** (12 × until version 5): 15 pearls in the Riff and the Kelpwald, 30 in the Tiefsee-Graben and 45 in the Vulkanschlucht. Luck applies (+10 % per point). Chests are never merged with other pickups; online every player near the champion gets one.

**Champion bosses:** from the **3rd boss encounter** of a run on, the boss arrives as a **champion boss**:
- one trait: Flink (the boss walks 35 % faster), Gepanzert, Vampir or Anführer;
- **"wütend"**: it roars as soon as it arrives and fights in Phase 2 from the start (it can still reach Phase 3); the message reads "👑 Champion-Boss: … – wütend von Anfang an!" and the HUD name gets a 👑;
- **15 % bigger** than the normal boss (collision circle and picture, since version 5; online the other players see the same size);
- HP ×1.3 on top of the normal boss scaling (Section 4);
- **look (version 5):** a double outline (gold outside, its trait colour inside) and an aura in its trait colour; under it a glowing seal with two rings, one dashed and one with twelve runes, turning in opposite directions; seven sparks circle it (passing in front of and behind it, with short tails), embers in its colour rise around it, and a shockwave ring pulses out every 3.2 s. Each boss wears champion jewellery: the **Hai-König** a five-pointed state crown with pearls and a big stone in its trait colour, a gold-trimmed dorsal fin with gold studs, glowing war paint and scars and a gold tooth; the **Riesenkrake** a gold diadem with a big stone, gold bands on its tentacles and a glow that runs along its suckers; the **Meeresungeheuer** glowing comb tips, glowing chevrons on its flank, gold rings on its lantern rod and three sparks circling the lantern; the **Lava-Titan** a crown of three crystals and a forehead jewel in its trait colour and six burning rocks instead of four. The three without a crown of their own get a floating state crown above them. In the Tiefsee-Graben the seal, sparks and crown stay visible in the dark, and the corpse keeps the jewellery;
- reward: the usual heart and a **double Boss-Schatz** (twice the pearls of Section 4) that also holds a **free upgrade card**: a normal level-up choice ("🎁 Schatztruhe!") that costs no XP. If a level-up and a free card are waiting at the same time, the level-up comes first.

**Achievements:** Champion-Jäger (defeat 25 champions, +60 pearls) and Kronenbrecher (defeat a champion boss, +120), see Section 10.

**How much they add (measured in version 3, before the version 5 economy).** Bot runs of 20 minutes with and without champions, same seeds: in the Korallenriff the bot defeated about 5.4 champions and 0.8 champion bosses per run, which made up about 9–10 % of the run's pearls; in the Tiefsee-Graben about 2 champions, 7 %. No measurable extra levels (the differences stayed within the normal run-to-run spread). Human players who hunt champions get a bit more. The target was 10–15 % of the pearls and at most 1–2 extra levels by 20:00. Version 6 raised `CHAMPION_CHEST` from 12 to 15 together with making champions harder, so hunting them stays worth it.

**Tuning knobs** (all at the top of the game script, next to `BOSS_TYPES`): `CHAMPION_START`, `CHAMPION_GAP_MIN` / `MAX`, `CHAMPION_LATE`, `CHAMPION_HP`, `CHAMPION_DMG`, `CHAMPION_SIZE`, `CHAMPION_SPEED`, `CHAMPION_XP`, `CHAMP_SHOT_EVERY` / `_N` / `_SPREAD` / `_SPEED` / `_DMG`, `CHAMPION_CHEST`, `CHAMPION_EXCLUDE`, `CHAMPION_BOSS_FROM`, `CHAMPION_BOSS_HP`, `CHAMPION_BOSS_TRAITS`, the trait table `CHAMPION_TRAITS` and the per-trait numbers `FLINK_*`, `SHELL_*`, `VAMPIR_HEAL`, `SPLIT_*`, `BURST_*`, `LEADER_*`; online `NET_GROUP_HP`.

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
Pulses from a point trailing 34 units *behind* your current facing direction (not centered on you), rendered as a soft, multi-tinted, drifting cloud. Base cooldown 1.2s. Deals **percentage of the target's max HP**, and slows anything it hits by 35% for 1.5s. Only a fraction of its damage applies to bosses (15 %) and champions (40 %, since version 5) so it can't trivialize them. It ignores your damage multiplier, the Shop damage bonus and Schlagkraft — the percentages below are exactly what it deals, which is why it keeps pace with enemy HP scaling. In PvP it hits other players for a flat `(6 + 3 × level) × your damage` instead (then the PvP rules of Section 13 apply).

| Level | Radius | Damage vs. regular enemies | vs. champions | vs. bosses |
|---|---|---|---|---|
| 1 | 90 | 10.5% of max HP | 4.2% | 1.58% |
| 2 | 110 | 13.0% | 5.2% | 1.95% |
| 3 | 130 | 15.5% | 6.2% | 2.33% |
| 4 | 150 | 18.0% | 7.2% | 2.70% |
| 5 | 170 | 20.5% | 8.2% | 3.08% |

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
Single heavy hit on the **strongest** enemy in range (the one with the most current HP; a boss always takes priority) — the hardest-hitting shot in the game. Base cooldown 1.4s. Since version 5 the spear **steers toward its target** (up to 5 radians per second) and **passes through every other enemy**, so it can no longer be wasted on a small fish in the way; it is drawn as a spear with a jagged coral tip.

| Level | Damage |
|---|---|
| 1 | 31.0 |
| 2 | 40.0 |
| 3 | 49.0 |
| 4 | 58.0 |
| 5 | 67.0 |

### Schwarm-Freund (Swarm Friend)
One (later two) independent companion fish that actively hunt: each one seeks the nearest enemy within 300 units of you, swims in to engage it directly, and fires on it — returning to idle orbit near you when nothing's around, and never wandering more than 300 units away. Each companion claims its own target: the second one skips whatever the first is already hunting, and only when there's nothing else do both attack the same enemy — in which case they keep at least ~34 units apart instead of stacking. They never park closer than 32 units to your Blobi's centre (they would be hidden under it). Online, when you swim into or out of the Hafen they drop their targets and come along (one that is more than 450 units away reappears next to you with a few bubbles); in the Hafen they orbit you without shooting. A companion that ever ends up more than 660 units away or with a broken position reappears next to you at once, and after a rescue or the Zweite Chance they are back at your side.

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
- **Healing:** every Blobi always heals **1 HP per minute** on its own (since version 5; not while downed). There are no healing pickups lying around the map (a pickup like that existed briefly and was removed for being too strong). The rest of the HP you regain mid-run comes from Regeneration (continuous, on top of the base 1 HP/min), the one-off +20 heal when you pick Lebenskraft, and the **heart every boss drops** (+40% of your max HP, Section 4); the Schutzschild blocks a hit but doesn't heal.

---

## 8. Spezialmechaniken (How defense works, tied together)

1. **Ordinary enemy shots** (Anglerfisch, the Tintenfisch ink, and the boss's radial bursts, roar rings, Sog rings, fans, tooth shots and ink ring) — blockable by the Bubble Ring on contact. From ring level 4, every block wears the bubble that took it (Section 6).
2. **Heavy boss shots** (the big glowing red ones) — ignore the Ring entirely. Dodge them or have a charged Schutzschild.
3. **Contact damage** from touching an enemy — reduced by Panzerung, avoidable with i-frames (0.5s after any hit) or a charged shield.
4. **Hazards and boss moves** (lava zones, tentacle slams and the whip, the Magma-Schockwelle, the Hai-König's charge, the Sog pull) — not shots, so the Ring can't touch them. They are all telegraphed and avoided by moving; Panzerung reduces them, a charged Schutzschild absorbs one hit, and i-frames apply (which is why standing in lava hurts about every half second).
5. **Sustain** — the base 1 HP per minute, Regeneration (continuous), the one-off +20 heal from picking Lebenskraft and the heart from every boss restore HP; Schutzschild blocks a hit without healing; Zweite Chance (Shop) is the only revive.

**Leveling curve:** the XP needed to leave level *N* is `⌊6 + N × 4.6⌋` (rounded down), so it grows roughly linearly (a bit under 5 XP more needed per level) — for example 10 XP to go from level 1 to 2, 52 XP from 10 to 11 and 121 XP from 25 to 26. Once every weapon and passive is maxed (and no bubble is missing), a level-up gives pearls instead of a card: 3 × the area's pearl value (3 in Riff and Kelp, 6 in Graben, 9 in Vulkan).

**Level-up cards:** each card says exactly what changes, e.g. `Stufe 2 → 3: Schaden 13,8 → 17,2 · Blasen 1 → 2`. A new weapon or passive shows `Neu:` with its level-1 values. The ring's refill card is called „Mehr Blasen“ and shows `Blasen 8 → 10 · alle Risse repariert`. Numbers already include your damage multiplier and cooldown bonuses. If you reload the page on the level-up screen, the same cards are restored.

---

## 9. Shop (Permanent Upgrades, bought with banked Perlen)

Every upgrade has its own price per level, and the higher levels are **gated by the bosses of the deeper areas**: tier 0 is open from the start, tier 1 needs the Riesenkrake (Kelpwald) beaten, tier 2 the Meeresungeheuer (Tiefsee-Graben), tier 3 the Lava-Titan (Vulkanschlucht) — once, in any run. So the Korallenriff alone can never max you out.

| Upgrade | Effect/level | Lv1 | Lv2 | Lv3 | Lv4 | Lv5 | Total |
|---|---|---|---|---|---|---|---|
| Grösserer Lebensvorrat | +10 starting max HP | 40 | 110 | 380 *(tier 1)* | 900 *(tier 2)* | 2,000 *(tier 3)* | 3,430 |
| Bessere Flossen | +3% starting speed | 35 | 95 | 330 *(1)* | 800 *(2)* | 1,800 *(3)* | 3,060 |
| Schärfere Stacheln | +4% weapon damage | 55 | 150 | 500 *(1)* | 1,200 *(2)* | 2,600 *(3)* | 4,505 |
| Perlen-Magnet | +22 pickup radius (base becomes 70 + 22×level) | 30 | 80 | 280 *(1)* | 700 *(2)* | 1,500 *(3)* | 2,590 |
| Glücksbringer | +1 starting Luck (more pearls, more often a 4th upgrade card) | 250 | 1,200 *(2)* | 3,000 *(3)* | — | — | 4,450 |
| Zweite Chance | Once per run, a button that revives you at 50 % HP | 1,200 *(1)* | — | — | — | — | 1,200 |

Everything costs **19,235 pearls**, plus **4,700** for the three Blobis (Section 1). The Shop shows the three gate bosses as chips at the top (✔ once beaten, 🔒 until then), each upgrade's levels as pips (locked ones dimmed), the price of the next level, and for a gated level "🔒 Nächste Stufe: besiege …". When you beat the boss that opens a tier, a message tells you. Saves from before version 5 keep every level they already bought.

**How Zweite Chance works (version 5):** a one-time, permanent purchase (1,200 pearls, after you have beaten the Riesenkrake). Every run then starts with the revive armed, shown as a green heart (💚) next to your HP numbers. The first time you'd die, **the game stops and a bar appears with 10 seconds to decide**: press **„💚 Zweite Chance“** (or Space / Enter) and you're back at 50 % max HP with 2 s of invulnerability and a revive flash, while enemies within 320 units are blasted back out to about 340 units (bosses are shoved 140 units) and every enemy shot, lava pool, tentacle slam and shockwave is wiped. The bar also says what is at stake (version 7: "Sonst ist dein Lauf vorbei: Level 12 · 8:40 · 306 Gegner"). Press **„Lauf beenden“** (called „Aufgeben“ until version 6) or let the time run out and the run ends. Online with a friend nearby you are downed instead of the game stopping (Section 13), and the same bar lets you use the Zweite Chance while you wait for a rescue; if a friend rescues you first, the Zweite Chance stays armed for later.

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
| Boss-Bezwinger | Defeat a boss in each of the four areas (lifetime; since 7.2 any of the area's six bosses counts) | 200 |
| Perlensammler | Earn 1000 pearls in total (lifetime) — having 1000 banked at once also counts | 100 |
| Voll entwickelt | Reach level 30 in a single run | 75 |
| Ganze Blobi-Familie | Own all 4 Blobis (since version 5 that means buying them) | 50 |
| Champion-Jäger | Defeat 25 champions (lifetime) | 60 |
| Kronenbrecher | Defeat a champion boss | 120 |
| Riff-Album komplett | Defeat all six Korallenriff bosses (7.2) | 80 |
| Kelp-Album komplett | Defeat all six Kelpwald bosses (7.2) | 150 |
| Graben-Album komplett | Defeat all six Tiefsee-Graben bosses (7.2) | 250 |
| Vulkan-Album komplett | Defeat all six Vulkanschlucht bosses (7.2) | 400 |
| Bestiarium | Defeat all 24 bosses (7.2) | 600 |

**Achievements are unlocked automatically, but you collect the reward yourself.** All twelve together pay 990 pearls. Online, defeating an enemy together counts for every player who hit it (Section 13).
- When a condition is met, the achievement is **unlocked** and a banner points you to the menu. Nothing is paid yet.
- On the Achievements screen a waiting achievement shows a gold **NEU** tag, a 🎁 icon and a button **„Einlösen“ (+N 💧)**. Click it to collect the reward — the pearls count up into your balance. Two or more waiting? An **„Alle einlösen · +N 💧“** button at the top collects them all at once.
- The main menu's Erfolge button carries a red **„N NEU“** badge as long as rewards are waiting.
- The game-over screen lists the achievements you just unlocked (with the NEU tag and the pearls waiting) and offers a **„Erfolge einlösen“** shortcut. If you leave older rewards unclaimed, it reminds you how many are waiting.
- **Progress (version 7):** every locked achievement shows a bar with how far you are ("37 / 100", "3:20 / 5:00"), and the top of the screen shows "🏆 3 von 12 Erfolgen" with a bar. The list is sorted: waiting rewards first, then the locked ones — **the one you are closest to first** — then the claimed ones (✓ eingelöst).
- **Game over (version 7) shows one next step at a time:** new or waiting rewards first (with "Erfolge einlösen"); otherwise, if your banked pearls now pay for an open Shop upgrade, "💧 Du hast jetzt 154 Perlen – genug für Grösserer Lebensvorrat (40 💧)" with a "💧 Verbesserungen kaufen" button (the cheapest one you can afford); otherwise the **next goal** — the locked achievement you are closest to, with its bar.
- **Shop (version 7):** an upgrade you can't afford yet shows how much is missing under its price ("noch 25").
- Every reward can be collected only once. Saves from the previous version, where rewards were paid automatically, keep all those achievements as already claimed — nothing is paid twice and nothing is lost. "Voll entwickelt" used to need level 20; anyone who already earned it keeps it.

---

## 11. Fortschritt & Speichern (Saving)

- **Between runs:** pearls, Shop levels, achievements (unlocked and claimed), unlocked stages, best stats, and character unlocks save automatically to the browser's local storage every time they change, and persist across sessions once this is live on your actual site. If the browser blocks local storage (private mode, some embeds), the main menu shows a warning, because progress then only lasts until the tab is closed.
- **Mid-run:** the game also snapshots your *current* run — level, weapons, passives, bubble-ring wear, HP, elapsed time, pearls so far, position — whenever the tab is backgrounded, right before the page is hidden, and every ~8 seconds while playing. Since version 5 the snapshot also holds **the scene**: every enemy with its HP and state (including a boss in the middle of its fight and champions), every pickup on the ground (orbs, pearls, hearts, chests), the spawn, lava, Elite and Piranha-Ring timers and your invulnerability. If the browser discards or reloads the tab (common on mobile after being away a while), the main menu offers a **"Weiterspielen"** button and you continue exactly where you were: the game shows a **3-second countdown** in which everything stands still, then it goes on. Only the short-lived things — shots in flight, lava pools, slam circles and shockwaves — are not restored. If you were on the level-up screen, you come back to exactly that screen with the same cards and no upgrade is lost. Reloading is therefore no escape from a bad situation any more: the enemies, the boss's HP and your HP are all as before. (Snapshots from before version 5 still work the old way: no scene, 1.5 s of protection.) **Online runs** are saved too, with their room, and come back with "Online weiterspielen" (Section 13); their pearls are banked when the run ends, you leave the room, or the saved run is no longer used.
- **"Zum Menü" keeps the run (version 6):** the pause menu's **Zum Menü** no longer ends your run. It saves it (with the scene, as above) and goes to the main menu **without asking**; **Weiterspielen** continues it, online runs with **Online weiterspielen** (Section 13). Only when you are downed or the Zweite Chance bar is open does Zum Menü end the run (pearls banked), as before.
- **Nothing is thrown away:** using **Neustart** in the pause menu and starting a new dive while an old snapshot is waiting bank the pearls and stats of the run they replace — including the Glücks-Blobi level check — exactly as dying does. **Neustart always asks once more** ("Wirklich neu starten?", a second tap within 4 s confirms), except in the first 3 seconds of a run. (Until version 5 both Neustart and Zum Menü asked only after the first minute, so sometimes they asked and sometimes not; now the rule is simple: Neustart asks, Zum Menü never needs to because nothing is lost.)
- **Tab switching:** the game pauses automatically when the tab or window loses focus, and it clears any held keys or touch so your fish doesn't keep drifting when you come back.

---

### Konto (version 7.2, optional)

Main menu **👤 Konto**. Guests play as before (save in the browser); an account keeps the save on the server.
- **Konto erstellen:** a private login name (3–24 letters, digits, `. _ -`), a public display name (same rules as online names, unique, changeable **once per day**) and a password of at least **8** characters (any characters, emoji count as one; common passwords, game words, the names themselves and passwords known from data leaks are refused; the screen suggests three random words). The browser's save moves into the account. A **recovery code** (16 characters, `XXXX-XXXX-XXXX-XXXX`) is shown **once**; "Weiter" only after ticking "Ich habe ihn aufgeschrieben".
- **Anmelden** on another device: "Angemeldet bleiben" (on by default) keeps the device logged in (90 days without use, one year at most). If that browser has guest progress, both saves are shown side by side and you pick one (asked twice); the other stays **30 days** ("Alten Spielstand wiederherstellen").
- **Two devices:** the one that plays last is active; the other stops with "Dein Konto ist gerade auf einem anderen Gerät aktiv" and **Hier weiterspielen** (no password; the save reloads from the server first). Changes upload 2 s after they happen, each with the next save number; offline they wait and retry every 30 s.
- **Wrong passwords:** after 5 wrong tries a wait of 1 minute, doubling up to 15 minutes. About 30 login tries per minute and 20 sign-ups per hour per network address. Every failed login says the same: "Login-Name oder Passwort stimmt nicht."
- **Passwort vergessen?:** login name + recovery code + new password; you get a new code and every other device is logged out. **Neuen Code erstellen** (with the password) replaces the code; **Passwort ändern** logs out the other devices; **Geräte** lists them (remove one, or all); **Abmelden** leaves this browser as a guest with an empty save; **Konto löschen** (with the password) removes everything.
- **Online rooms** use the account's display name (sent through a one-time ticket valid 30 s, never the login token).
- **The server checks every save**: shop levels, Blobis and achievements must exist, at most 40,000 pearls more than the last save, and everything bought must fit the pearls ever earned plus achievement rewards (+2,000 slack). A refused save is kept for the admin to look at.

## 12. Steuerung (Controls)

- **Desktop:** WASD or arrow keys to move. ESC or the pause icon to pause (holding ESC no longer flickers the pause on and off). **Space** or **Enter** uses the Zweite Chance while its bar is shown.
- **Mobile:** drag anywhere on the screen to move. The first finger down owns the stick; extra fingers or a resting palm are ignored, and lifting a different finger doesn't stop you. If you lift the steering finger while another finger is still down, that finger takes over the stick (version 6). The stick grows with the screen (radius 11 % of the shorter side, between 46 and 76 px), so it suits phones and tablets alike. **Multi-touch:** buttons that matter during play — the level-up cards of the bottom bar, the Zweite Chance buttons, the Schwarmruf buttons, the 💬 and 📯 buttons, the quick-message wheel and the room pill — react to a second finger while the first keeps steering. Since version 6 they react as soon as the finger touches them (touch / pointer down, not only on the browser's click, which some phones drop while another finger is on the screen), and the bars at the bottom let touches through everywhere except on their buttons, so you can steer under them.
- Attacks on every weapon are fully automatic — the only inputs are movement and which upgrade to pick on level-up (a click/tap, or the keys **1–4**).
- **Online:** **Q** opens the quick-message wheel (keys 1–8 pick a message while it's open), **Tab** shows the player list; on touch screens the 💬 button and a tap on the room pill do the same. As Leitfisch, **R** (or the 📯 button) sends the Schwarmruf; when a call comes, **F** follows and **N** declines (Section 13).
- Typing in the name or code field of the "Online spielen" screen never moves the fish or pauses the game.

---

## 13. Online spielen (Beta)

Play together with others: in a **public room** with everyone who is online ("Schnellspiel") or in a **private room** with your friends, either in **COOP** (together against the sea) or in **PvP** — **team PvP** (team Blau against team Rot: your weapons also hit the other team) or, since version 7, **Jeder gegen jeden** (free-for-all: no teams, everyone is your enemy). PvP has far fewer enemies. Everyone plays their own run — own level, XP, weapons, HP and pearls — but you share one map: you see each other, fight the same enemies, race for the same loot and rescue each other. The game needs the small online server from the folder `blobfisch-online` (its README explains the free Cloudflare setup); until its address is entered in `index.html` (`ONLINE_SERVER`), the online screens say the server isn't set up yet. Single-player is completely unaffected.

**Getting in (version 7)** — short steps, never more than two choices at once. A bar at the top shows the step ("Schritt 2 von 4"); the line "Du spielst als …" repeats what you have already chosen; your last choice is preselected with a green "Zuletzt" tag (first time: COOP is marked "Für den Anfang").
1. Main menu → **🌐 Online spielen**: your **profile**. A name is already filled in (3–13 characters: letters including umlauts, digits, space, `-` and `_`; 🎲 picks a random one like "Blobi482"); pick your Blobi (one you own). The top line shows how many players are online right now (refreshed every 10 s while the online screens are open). **Weiter**.
2. **Wie willst du spielen?** — **🤝 Zusammen (COOP)** or **⚔️ Gegeneinander (PvP)**. Above them **🔄 Weiterspielen** appears when a saved online run is waiting (it says how many minutes it still waits before it's gone). Below them: **"🔑 Du hast einen Code von einem Freund? Hier beitreten"** — type the code (upper or lower case); you get that room's mode.
3. Only for PvP: **Welches PvP?** — **🆚 Team gegen Team** (Blau against Rot) or **🗡️ Jeder gegen jeden**.
4. **Mit wem?** — **⚡ Schnellspiel** ("Empfohlen", with the number of players in this mode right now) or **👥 Mit Freunden** (a private room).
5. **Wo willst du spielen?** — the area. For Schnellspiel the area where most players of your mode are right now is preselected (if you have unlocked it) and each area shows how many are there; the button says how many are waiting ("Los geht’s! · 3 warten"). You land in the **fullest public room of that area and mode that still has space**, e.g. "Korallenriff #1" (COOP), "Korallenriff PvP #1" (team PvP) or "Korallenriff FFA #1" (Jeder gegen jeden), up to **24 players**; when all of them are full a new one opens ("#2"). A public room closes 60 s after its last player has left. For **Mit Freunden** you get a **private room** (up to **8 players**) in your mode; your run starts at once, and the room's **code** (4 letters, never I, L or O) is shown in a message, in the room pill under the XP bar (`🤝 KRBX · 👥 1/8`; ⚔️ team PvP, 🗡️ Jeder gegen jeden) and in the pause menu. Give it to your friends. The room stays open for 10 minutes after the last player has left, so you can rejoin with the same code.

You play in the room's area, even if you haven't unlocked it yourself yet (beating a boss there still counts normally).

**Jeder gegen jeden (version 7, mode `ffa`):** like team PvP (30 % damage, at most a quarter of the target's max HP per hit, far fewer enemies, more XP, knockouts give XP and 30 points), but without teams: every other player is a target, nobody can rescue anyone (0 HP ends your run unless you use the Zweite Chance), and there is **no Schwarmruf**. The best player still wears the crown — every player hunts him, and knocking him out is worth 60 points. Every player keeps their own colour ring.

Names are checked by the server; a name that isn't allowed is replaced by a random one and you're told so. Old random names "Blubbi…" become "Blobi…" automatically. **Versions:** a room only mixes players with the same game version (protocol 5 since version 7; protocol 4 was version 6); an older page gets "Bitte lade die Seite neu", and Schnellspiel keeps versions apart. The server must be updated before the new page goes online.

**The Hafen** — a safe harbour in the middle of every room (radius 250, a dashed circle with an ⚓ sign). Every online run starts inside it with **5 s of protection**. Inside the Hafen enemies can't reach you (they stop at its edge), enemy shots vanish, you take no damage and no lava zones appear — but **your weapons rest** (no shots, the Blasenring doesn't hurt, your Schwarm-Freunde don't shoot) and **no enemies spawn** around you. A hint at the bottom of the screen says so while you're inside. Swim out to fight. Outside the Hafen an arrow at the screen edge points back to it with the distance to its edge ("⚓ Hafen · 275 m", version 6), like the arrows to friends.

**What is shared**
- **Seeing each other:** every Blobi shows its name, level and a small HP bar and has its own colour ring. You also see your friends' **Blasenring** bubbles, **Schwarm-Freunde** and **shield**; a friend's bubbles block small enemy shots on your screen exactly as in their game. Friends off-screen get a coloured arrow at the screen edge with name and distance (in "m" = 10 world units); the **3 nearest** are shown (5 until version 7). A **downed** friend (in PvP: teammate) always gets a red, pulsing arrow, the **Leitfisch** always gets one (👑), a Leitfisch who is calling a pulsing gold one (📯), and world bosses and champions always get one (red / in the trait's colour), even far away. **Nothing overlaps (version 7):** arrows stay below everything at the top of the screen; when several point the same way the arrows slide apart along the edge and their labels go to the free side; arrows and labels also keep clear of a friend who is just visible at the screen edge. In the Tiefsee-Graben your friends stay visible in the dark.
- **Enemies:** each player's enemies spawn around that player and scale with that player's run time and level, as in single-player. Every enemy chases the **nearest Blobi** — yours or a friend's, but a friend's only while they are within **1,600 units** (about 1.5 screens), so they can always see what chases them. Downed players are never chased; players in the Hafen only when nobody else is in reach (otherwise the enemies wait at the Hafen's edge).
- **Fighting together:** your weapons hit your friends' enemies too; your game predicts the hit at once (the HP bar drops and a predicted kill disappears straight away) and the owner's game confirms it a moment later. Ink-cloud slowing and the Vampir heal work across as well.
- **Loot is shared — first come, first served (version 5):** an enemy drops its loot **once**, where it died, and everyone sees the same orbs, pearls, hearts and chests. Whoever touches a pickup first gets it; it disappears for everyone else. (The owner of the enemy decides who was first; an unconfirmed grab is released after 2.5 s.) Boss hearts and Boss-Schätze are the exception: every player near the boss gets **their own** heart and chest ("einer für jeden"), and a champion drops one chest per player nearby. Loot of a player who leaves, dies or keeps the tab in the background for 15 s is taken over by the others, so nothing vanishes. **Version 6 fixed chests that sometimes gave nothing:** when the owner can't give you a pickup (someone was faster, or you already have your own boss heart or chest), their game answers at once and you get a message ("🎁 Zu spät – jemand anderes hatte die Truhe schon."); a grab that gets no answer leaves the pickup on the ground instead of removing it; a pickup you had grabbed from a player who then left is given to you; and the pickup sound plays only when you really get the item. Each helper's kill counts for their achievements and statistics, and a boss kill opens the next area for every helper. **Version 7.2 fixed pearls that some players never saw:** loot that drops while a friend is 2,400–2,700 units away now reaches them too, and every game resends its whole loot list every **10 s** while a friend is near.
- **More players, more loot:** enemies that spawn near several players are tougher (see below) and drop correspondingly more: XP × the same group factor and a higher pearl chance.
- **Taking damage:** your own game decides when you are hit, checking your Blobi against everything you see: your enemies and your friends', their shots, slam and lava zones, explosion circles and magma waves. A friend's Meeresungeheuer pulls you with its Sog when you are within 900 units (never inside the Hafen). To keep a modified game from knocking you out unfairly, anything that comes from another player's game can take at most **60 % of your max HP in one hit**, its slam and lava circles warn for at least 0.6 s (and stay visible on your screen for at least 0.35 s despite the delay), and a magma wave always starts close to its boss.

**PvP rooms — teams (version 6):** a PvP room has two teams, **🔵 Blau** and **🔴 Rot**. The server puts every new player into the smaller team (and remembers it when you come back); a message tells you your team, and your colour ring, arrow, name and player-list entry use the team colour. In a **private** PvP room you can switch teams in the player list while you are in the Hafen (at most every 5 s). Everything above applies, and in addition every weapon hits the players of the **other team**: **30 % of the damage it would deal to an enemy**, at most **25 % of the victim's max HP per hit** (the Tintenwolke hits players for a flat `(6 + 3 × level) × damage`). Teammates can't hurt each other. Players in the Hafen can't be hit and can't hit others, downed players can't be hit, and the usual i-frames apply. When a player drops to 0 HP, the last player of the other team who hit them within 4 s gets the knockout (both get a message) and **6 XP per level of the knocked-out player**. Being knocked out works like any defeat: Zweite Chance first, then downed if a **teammate** is near, otherwise the run ends. **Only teammates can rescue you**: you can't revive a player of the other team (their downed ring isn't shown to you).

**PvP has far fewer enemies (version 6):** PvP is about the other team, so each enemy wave is **half as big**, waves come **2.2 × less often** and there are **no Piranha-Rings**. So that you still level up at a similar pace, enemies give **2.5 × XP**. Bosses, world bosses and champions come as usual.
Since version 7.2 the **size and rate of the waves follow the longest run in the room** (each player still spawns around themselves, and the enemies' strength and kinds still follow your own run time), so a newcomer gets as many enemies as a player who has been there for 10 minutes.

**PvP hits (version 7.2):** players of the other team (FFA: everyone) are shown where they are *now* — their newest position, moved forward by the measured round trip to the server (ping every 5 s in PvP) and smoothed over about 40 ms, at most 2.5 × their speed per frame — not 130 ms in the past like friends. Your weapons hit them there. A hit travels with its place and time; the victim's game only counts it if the victim was within **34 units** of that place at that time (the last 0.15 s). Bubbles of the other team stop when they touch you on your own screen.

**Stronger in groups:** while other players are near (active, within 1,600 units), every new enemy that spawns around you gets **+50 % HP per other player** — harder through strength, not more enemies. This includes champions (whose level factor then uses the average level of the players nearby, Section 5). A **world boss** gets **+60 % HP per other player** near it when it appears, and its level factor also uses the average level. Since version 6 bosses and champions also **grow when more players come near later**: their max HP rises to the bigger group's value and they keep their HP fraction (no growth when players leave).

**World bosses and room champions:** the player who has been in the room longest (the "anchor") runs the room's clocks; when they leave, the next one takes over with the same clocks. As long as you are **alone in a room**, everything works exactly like single-player (your boss at 5:00, champions from 4:00). As soon as **others are in the room**, your own boss and champion clocks rest and the room's schedule takes over (it starts from the anchor's own clocks):
- **World boss:** when the room's boss clock runs out (5 minutes of room activity, 4 minutes after the previous world boss is gone), a boss appears near a **random player** who is playing and not in the Hafen. The whole room gets a 3-second warning ("⚠ Ein Weltboss erscheint bei Lena!") and a red arrow. **Every third world boss is a champion boss.** Every player near it when it dies gets their own heart and Boss-Schatz, and the kill counts for unlocking the next area for everyone who hit it. Near a world boss fewer normal enemies spawn, as in your own boss fight. The player it appeared at plays it; if they leave the room or their run ends, the nearest other player (within about 3,600 units) **takes it over** with all its HP and state, so a world boss no longer vanishes with its host. Room champions are handed over the same way. Since version 6 the heir may also be a **paused** friend (their game takes the boss and keeps it frozen until they continue), and the up to **40 nearest normal enemies** go along too, so a player dying or pausing no longer makes the boss and every mob vanish. The boss bar shows the boss's name, its encounter number in the room (×2, ×3 …) and its phase; it no longer shows whose boss it is. **When everyone in the room has died** (all on the game-over screen), the room's schedule starts over for the next runs: the first world boss comes after 5 minutes again and counts as ×1 (version 5 kept counting, so after a wipe the next boss was announced as ×4).
- **Room champions:** every 120–150 s (never during a world boss), one champion appears near a random player and is announced to the room ("👑 Champion bei Lena: Flinker Krebs"); at most 1 at a time (2 after 15:00 of the anchor's run). Every player nearby gets a chest.

**Downed and rescued:** at 0 HP, if you bought the **Zweite Chance**, its bar appears (Section 9) — with a friend (PvP: teammate) near you are downed at the same time and can use it or wait for the rescue. Otherwise, if a friend who is playing is within **2,200 units** (about 2 screens), you are **downed for 20 s**: you can't move, attack or collect anything, you take no damage, and enemies ignore you. Your Blobi lies faded inside a red, pulsing ring; a banner shows the seconds left. A friend who stays within **60 units** of you (the dashed circle) for **3 s** rescues you — a green ring fills up on both screens — and you're back with **30 % HP**, 2 s of protection and nearby enemies pushed away, like the Zweite Chance. Both of you get a message. If no friend is within 2,200 units when you drop to 0 HP, or the 20 s run out, your run ends as in single-player.

**Pause and level-ups while friends are near:** if an active friend is within 2,400 units, **ESC** or the pause button opens the pause menu at the bottom of the screen, but **the game keeps running** (it says so); if no friend is near any more, it becomes a real pause. **Level-up cards** slide in as a bar at the bottom: pick with **1–4** or a tap; after **15 s** the first card is taken automatically. Alone, both stop the game as in single-player. Switching to another window counts as pressing pause. **Tab in the background** always pauses: your friends then see you as sleeping — your Blobi and your enemies disappear for them until you're back (💤 in the player list). If a friend's game is really paused, their enemies stand still on your screen in their normal colours; you can still hit and defeat them (their game applies it while paused), but they don't hurt you.

**Leitfisch & Schwarmruf (version 6).** Every room keeps a board of **Schwarmpunkte** (swarm points). The best active player wears the crown — the **Leitfisch** (lead fish) — and can call the whole swarm to him.

- **Points:** every enemy you defeat 1, an Elite 3, a champion 20, a boss 50 (a champion boss 70), rescuing a friend 15; in PvP a knockout 30 (60 if you knock out the other team's Leitfisch). The Leitfisch also gets 3 points for every player who follows his call. The room keeps your points while you're away and gives them back when you return (your browser has a private key; the name doesn't matter), and they are saved when the room empties. The server limits how fast points can rise (60 per second, plus 300 at once), so a modified game can't buy the crown.
- **The crown:** the player with the most points becomes Leitfisch once they have at least **100 points** and at least **2 active players** are in the room (PvP: in their team — each team has its own Leitfisch). A challenger needs 10 % more points (at least 25 more) to take the crown, so it doesn't flicker. "Active" means playing and not 60 s without any key or touch; if the Leitfisch is no longer active (or reloads), the crown waits 10 s before moving on. The Leitfisch wears a golden crown above the name on every screen, and a message tells the room when the crown changes.
- **HUD — the score card (version 7):** under the room pill a small card with at most three labelled rows: in team PvP first the score **🔵 1.200 ▬▬▬ 950 🔴** with a bar (your team underlined); then **"🏅 Platz 3 von 5 · 480 Punkte"** (in team PvP "🏅 🔴 Im Team: Platz 2 von 3 · …"); then the crown: "👑 Krone: Lena · 1.250", "👑 Du hast die Krone!" (Jeder gegen jeden: "… Alle jagen dich."), "👑 Krone ab 100 Punkten" or, while there are too few players, "👑 Krone ab 2 Spielern (im Team)". Tapping the card opens the player list; while the list is open the card hides so nothing lies on top of each other. The room pill shows only mode, room and players ("⚔️ KRBX · 👥 3/8"); your team is on the card. **Toasts** in a run always appear just below the card (and the boss bar), never on top of them.
- **Schwarmruf (swarm call)** (not in Jeder gegen jeden): the Leitfisch gets a 📯 button next to 💬 (key **R**). The first call is possible 60 s after the first crown, then once every **3 minutes** per room (PvP: per team); a new Leitfisch inherits the timer, and the button shows the time left. A call goes to everyone (PvP: only the own team): a horn sounds, a gold bar at the bottom says who calls and how far away ("📯 Lena ruft! · 840 m"), and you have **10 s** to answer with **🐟 Folgen** (F) or **Nein** (N). A gold arrow points to the caller meanwhile.
- **Strömungsritt (current ride):** after Folgen there is a 0.6 s wind-up (Nein still cancels), then a current carries you to the Leitfisch at 3,000 units per second (1.2–3 s). While riding you can't be hit, but you also don't attack, collect anything or spawn enemies; a trail shows the ride on every screen. Your own enemies that are left more than 2,400 units behind move to the spawn ring around your new spot, so they don't sit somewhere far away. You can't follow while you're downed, the Zweite Chance bar is open or your own boss fight is on (the bar says why). If you're already within 1,200 units of the Leitfisch you skip the ride and get the bonus at once.
- **Arrival:** you land on a ring 160 units around the Leitfisch. A wave pushes your normal enemies within 220 units out of the circle and **stuns them for 1 s** (no damage; bosses and champions only flash), and you have 1.5 s of protection.
- **Schwarmgeist:** the Leitfisch, everyone who followed and everyone who was already near gets **+15 % damage for 30 s**, the followers while within 900 units of the Leitfisch (a pill in the HUD shows the time; it doesn't stack). Players of the other team get a message that a call went out.
- **Safety:** the server decides who wears the crown and when a call is allowed; a player can only fly the ride flag for at most 4 s after a real call, so nobody can fake rides to dodge hits.

**Quick messages:** **Q** or the 💬 button opens a wheel with 8 messages — 👋 Hallo, 🆘 Hilfe!, 📍 Hierher!, 🙏 Danke!, ⚠️ Boss!, 🎉 GG, 👑 Champion!, 👍 OK — pick with a click/tap or the keys 1–8 while the wheel is open. The message shows as a speech bubble above your Blobi for 3 s; at most one every 2 s. Players who can't see you get it as a message at the top ("💬 Lena: Hilfe!"). There is no free text chat.

**Player list:** **Tab** or a tap on the room pill shows everyone in the room with colour, Blobi, name, level, **Schwarmpunkte** (👑 for the Leitfisch) and what they're doing (distance, ⚓ Hafen, ⏸ Pause, 💔 Hilfe!, 💤 schläft, ☠ vorbei). In team-PvP rooms it is split into the two teams with their point totals, and in private team-PvP rooms it has the team-switch button. A line at the bottom explains the points for the room's mode. It opens just below the room pill.

**Game over, leaving, being away:** your run ends as usual (summary, pearls banked) and your enemies vanish from the others' screens. **"Nochmal eintauchen"** starts a new run at level 1 in the Hafen of the same room. **"Zum Menü"** on the game-over screen leaves the room; **"Zum Menü" in the pause menu** leaves the room but **keeps your run** (version 6): it is saved and "Online weiterspielen" brings you back into the same room (for 30 minutes), as after a reload. After **5 minutes without any key, click, touch or movement** you leave the room automatically and continue alone (your place in the room is free again). Holding the touch stick and swimming count as activity (until version 4 a phone player who steered for 5 minutes without lifting the thumb was taken out of the room by mistake).

**Reloading the page:** online runs are saved every ~8 seconds like single-player runs, together with their room. After a reload the main menu shows **"🌐 Online weiterspielen · Korallenriff #1 · Lv 12 · 8:30"** (the same button is on the "Wie willst du spielen?" screen). It takes you back into the same room with your level, XP, weapons, passives, HP, pearls and time. If the run was saved less than 60 s ago you continue **at the same spot with your enemies and pickups** (after the 3-second countdown); after longer you start in the Hafen with 5 s protection. Joining the same room with its code or through Schnellspiel restores the run too. If the private room no longer exists, you continue in Schnellspiel of the same area. A saved online run is kept for 30 minutes; starting a new online run elsewhere ends it — in both cases its pearls are banked. If you were downed when the page closed, the run counts as over (pearls banked).

**Connection problems:** if the connection drops, the game keeps running alone and reconnects by itself (up to 4 tries); if that fails, you continue alone (and the run can be resumed like a single-player run). Messages explain wrong codes ("gibt es nicht"), full rooms (Schnellspiel simply finds another room), an unreachable server, **"Der Online-Modus ist für heute voll"** (the server's free daily limit is used up; it resets at 00:00 UTC, which is 1:00 or 2:00 at night in Switzerland — the message shows the local time) and an outdated page ("Bitte lade die Seite neu").

**Technical numbers** (for tuning): the game sends its state **10 times per second** while another player is within 2,400 units (or one of your enemies is near them), **6.7 per second** when more than 6 players are on one screen and **5 per second** with more than 12; **once per second** when everyone is far away, every 2 s while paused or on the game-over screen, and **nothing at all while you're alone in the room** (the room then sleeps and costs nothing). Friends and their enemies are shown 130 ms in the past so they move smoothly (in a crowd, the time between their messages plus 30 ms, at most 300 ms). A friend who sends nothing for 3.5 s counts as asleep. Values from other players are capped (damage per hit 1,000 and at most 60 % of your max HP, PvP hits 25 %, XP per kill 1,000). A message is about 0.5–1.5 KB. Measured: two players together send about 10 messages and 5–10 KB per second each; four players together about 14 KB/s up and 41 KB/s down each; 24 players on one screen about 82 KB/s down each (bot test against the real server software). Knobs in `index.html`: `ONLINE_SERVER`, `NET_NEAR`, `NET_LIVE`, `NET_TICK_NEAR` / `FAR` / `IDLE`, `NET_CROWD`, `NET_DELAY`, `NET_ASLEEP`, `NET_GROUP_HP`, `WORLD_BOSS_HP`, `WORLD_BOSS_GAP`, `HAFEN_R`, `HAFEN_PROTECT`, `DOWN_TIME`, `DOWN_NEAR`, `REVIVE_R`, `REVIVE_TIME`, `REVIVE_HP`, `LVLBAR_TIME`, `QUICK_MSGS`, `QUICK_SHOW`, `QUICK_GAP`, `Net.afk`, `ONLINE_SNAP_TTL`, `PVP_BATCH`, `PVP_GAP`, `PVP_ENEMY_XP`, `PVP_KO_XP`, `TEAM_NAMES` / `_COLORS`, `LF_POINTS`, `LF_WINDOW`, `LF_WINDUP`, `LF_RIDE_SPEED` / `_MIN` / `_MAX`, `LF_SKIP`, `LF_RING`, `LF_WAVE_R`, `LF_STUN`, `LF_PROTECT`, `LF_FAR`, `LF_BONUS` / `_TIME` / `_R`, `LF_IDLE`; in the server's `room-core.js`: `CAP_GLOBAL`, `CAP_PRIVATE`, `ROOM_TTL_MS`, `GLOBAL_TTL_MS`, `REPORT_EVERY_MS`, the name lists and the `LF` block (crown minimum, margin, grace, call cooldown, point rate limit, team switching).

---

## 13b. Strategie (Test, version 7.2 – step 1 of 5)

Main menu **🏰 Strategie (Test)**. Step 1: your base alone, saved in this browser (the account and the shared map come in steps 2 and 3). All numbers are first guesses for play-testing.

- **Your Blobi** fights as in Survivors (shop upgrades apply) and keeps its **level, weapons and passives** between sessions. Each level needs **5 ×** the XP of Survivors. No pearls drop. **Dying:** back in the Muschelburg at level 1 with only the Blasenschuss; half the XP in the bar drops as orbs; 3 s protection. The **Zweite Chance** works once per day.
- **Base:** a grid of 48-unit tiles around the **Muschelburg** (3×3, can't be destroyed – at 0 it stays at 1 HP and recovers 1 %/s). Start: Muschelburg, Korallenfarm, Perlentresor and 200 Korallen. **🔨 Bauen** (inside your base) lists the buildings; tap a free spot (green outline). Tap a building for **Ausbauen**, **Verschieben** (free), **Reparieren** (a ruin: 30 % of its level's cost), and its own actions.
- **Muschelburg levels:** 1 (grid 9×9) · 2: 300 Korallen (9×9) · 3: 800 (11×11) · 4: 1,500 + 60 Kristalle, 3 min (11×11) · 5: 3,000 + 150, 7 min (13×13). Other buildings can't go above the Muschelburg level. Building level n costs base × 1.8^(n−1) Korallen, from level 3 also Kristalle (8 % of the base × 1.8^(n−3)); levels 1–3 are instant, level 4 takes 2 min, level 5 5 min; one timed build at a time; timers run while the game is closed.
- **Buildings** (base Korallen · from Muschelburg): Korallenfarm 60 · 1 (60 Korallen/h, +50 % per level, also offline; up to 3) · Lager 80 · 1 (cap +400 Korallen / +40 Kristalle ×1.6 per level; without one 300 / 30) · Perlentresor 80 · 1 (holds 150 XP ×1.6 per level) · Harpunenturm 100 · 1 (range 420 + 30/level, 18 damage +30 %/level, pierces 3, every 1.2 s) · Brutstätte 150 · 2 (army 2 + 4 per level) · Korallenmauer 10 · 2 (blocks enemies, 12 per Muschelburg level) · Leuchtturm 120 · 2 (waves warned 15 s ahead instead of 5) · Kristallbohrer 200 · 3 (6 Kristalle/h, +50 %/level) · Blasenkanone 220 · 3 (10 damage to all within 160 every 1.4 s) · Stachelfalle 60 · 3 (hidden, 60 damage in r 70, re-arms after 8 s) · Tintenwerfer 260 · 4 (slows everything within 180) · Heilquelle 240 · 4 (heals your Blobi and troops in the base 4 %/s per level) · Fischschule 300 · 4 (troop levels for 30 Kristalle × level, +20 % HP and damage each) · Elektroaal-Turm 400 · 5 (22 damage chaining to 4 enemies). Building HP +40 % per level.
- **XP and troops:** in the Perlentresor tap **🟢 Einzahlen**: the XP in your bar goes into the vault (your level stays, the bar starts at 0). The Brutstätte trains troops with vault XP (one after another, also offline): Schwarmfisch (Muschelburg 2, 10 XP, 5 s, 40 HP, melee 6) · Pfeilfisch (3, 25 XP, 10 s, 30 HP, shoots 9 at 260) · Panzerkrebs (4, 60 XP, 20 s, 160 HP, melee 12) · Kugelfisch (5, 40 XP, 15 s, bursts for 70 in r 110). Troops that die are gone. **Folgen** (escort your Blobi), **Halten** (stay where you are now), **Schicken** (tap a spot; they swim there and fight). Your troops have a white outline, a scarf in your colour and a small chevron.
- **Waves:** the first after 40 s, then every **2.5 minutes**; size 4 + 1.2 × strength (Muschelburg × 3 + levels of all defenses), enemy HP +12 % per strength point; every 4th wave brings a Riff boss (from the shared boss pool), from Muschelburg 4 every 2nd wave a champion. Enemies attack whatever is nearest: you, your troops or your buildings (bosses deal double to buildings). Kills give 1–2 Korallen (+10 % per Muschelburg level); bosses +60 Korallen and 20 + 10 × level Kristalle; champions 8 Kristalle.

## 14. Grafik, Klang & Leistung (Graphics, sound and performance)

- **Same view on every device:** the game zooms so that every screen shows about the same amount of world (about 1.3 million square units, e.g. 1,520 × 855 units on a 16:9 screen). Phones show everything a little smaller, big monitors a little larger (zoom limited to 0.7 – 2), so neither enemy spawns, weapon reach nor difficulty depend on your screen size any more. Name tags, champion tags, speech bubbles and the Hafen sign are drawn at a fixed size on small screens, so they stay readable.
- **Dynamic resolution:** if the game runs below 75 % of its target frame rate (45 fps at 60 Hz) for two seconds in a row, it lowers its internal resolution one step (100 % → 80 % → 65 % → 50 %, never below 0.6 pixels per CSS pixel) and raises it again after 12 seconds above 95 % (57 fps at 60 Hz).
- **Even frame pacing (version 6):** fast screens (90 or 120 Hz, e.g. the Realme 6) show a new picture every 11 or 8 ms. A phone that can't draw that fast drops frames irregularly, which looks choppier than an even, lower rate. The game notices the missed frames and then draws only every second frame (an even 45 or 60 frames per second; the game logic still runs every frame). After a long calm stretch it tries the full rate again, waiting longer each time it has to step back. 60 Hz screens are not affected.
- **Glows without blur:** every glow (shots, bubbles, Blobis, the shield, companions, bosses' auras) is a pre-drawn gradient instead of the browser's `shadowBlur`, which is very slow on weak phones. Enemies, bosses and projectiles are pre-drawn once and then only copied.
- **Art — simple where it is background, detailed where it matters:** the backgrounds and normal enemies keep the calm, minimalist look (soft colour gradient, dot grid, faint scenery). Detailed art is used for what you should notice: **champions** (animated drawings, Section 5), **bosses** (outlines, animations, bigger, Section 4), and the parts of the world that do something: **lava pools** (smooth glowing magma without an outline, bubbling and cooling), **kelp patches** (the slowing areas: dense, swaying kelp with leaves and floats and a visible rim), and the **pickups** (XP cores, pearls, hearts, chests). Shots have shapes: the Blasenschuss is a bubble, the piercing shot a water drop, the Korallenspeer a spear, the companions' shots small glowing orbs. The Schwarm-Freund companions are small mint-green blobs, like the player's own style.
- **Fonts:** Baloo 2 and Nunito are embedded in `index.html` (cut down to the characters the game uses, about 95 KB, plus Nunito's Cyrillic letters for Ukrainian, about 58 KB), so the game makes no request to Google Fonts and looks the same offline.
- **Sound (version 6, reworked in version 7):** the sounds are small synthesizer voices instead of simple beeps — bubbles, splashes, bells, a horn for the Schwarmruf, a whoosh and a current for the ride. Everything runs through a compressor, so loud moments don't distort; each voice has an envelope, many glide in pitch and get a little randomness, so repeated sounds don't sound mechanical. Frequent sounds are throttled, and at most 28 voices play at once. **Version 7:** a short underwater reverb gives the sounds space; your own hits make a quiet tick; collecting orbs and pearls quickly one after another climbs a scale (up to two octaves, the chain resets after 0.38 s); quick kills in a row sound brighter each time (up to +7 semitones, reset after 0.65 s; Elites thump more); defeating a boss or champion has its own big sound (boom, rising chord, sparkle); a PvP knockout has a punchy two-note sting; buying in the Shop or the Blobi selection jingles; the level-up chord is fuller; menu buttons make a soft bubble and going one step further in the online menus two rising notes. The 🔊 button in the menu switches sound on and off; in the pause menu the button says **"🔊 Ton: an" / "🔇 Ton: aus"**.

---

## 15. Lite-Version (TurboWarp) — differences

The TurboWarp port ("Lite", `blobfisch-survivors-lite.html` / `.sb3`) plays like the browser game, but it is a Scratch project and has not received versions 4, 5 and 6 yet (it is still called "Blobfisch Survivors Lite" and is German only). As of 2026-10-30:

- **No online mode**, **no languages** and **no mid-run resume** ("Weiterspielen" after a reload doesn't exist; progress *between* runs is saved).
- **Version 3 rules:** all four Blobis as before (Turbo and Panzer from the start, Glücks at level 25, nothing to buy), the old Shop (40 × 2, 35 × 1.9, 55 × 2.1, 35 × 1.9, 70 × 2.4, Zweite Chance 300 — 6,022 pearls in total, no tiers), Zweite Chance revives automatically, pearls 11 % / 22 % / 16.5 % / 22 % × 1 / 1 / 2 / 2, bosses drop 8–13 pearls instead of a Boss-Schatz, the Hai-König charges 1 / 2 / 2 times, no late-game flood, lava doesn't burn enemies, the Korallenspeer stops at the first enemy, the Tintenwolke deals full damage to champions.
- **Look:** baked costumes instead of canvas drawing (close, not pixel-identical): the version 3 enemies (champions also use the simple blobs, with aura, crown and name tag), the version 3 bosses (baked animation frames, without the version 5 outlines and poses), the old lava pools and kelp patches.
- **Screen and input:** a fixed 960 × 540 stage scaled to the window (the view does not adapt to the screen like Section 14); WASD / arrow keys and a mouse-drag stick (touch not tested); ESC or P pauses; the game pauses itself after a long frame instead of on window blur.
- **Performance:** reduced particles, ambient bubbles and pickup caps; TurboWarp's high-quality pen is on, which costs frame rate on phones (switching it off for phones is planned for the Lite update).
- **Saving:** in the browser's local storage under `cloudvariables:blobfisch-survivors-lite` (separate from the browser game's save).

The plan is to bring version 5 to Lite after it has been play-tested in the browser game.

---

## 16. Sprachen (Languages)

- **Toggle:** the start menu has a well-visible language switch at the top: **🌐 DE · EN · UA** (German, English, Ukrainian). The choice is saved with your progress. On the first visit the game follows the browser: German for German browsers, Ukrainian for Ukrainian ones, English for everything else.
- **What is translated:** everything you see — menus, the Shop, Blobis, areas, achievements, the instructions, the upgrade cards with their numbers, messages, the HUD, boss and champion names (champion names are built per language, e.g. "Swift, Armored Crab" / "Швидкий, броньований краб"), the pause, Zweite Chance and game-over screens, and all online screens and room messages. Numbers follow the language (2,5 / 2.5 / 2,5; 1.000 / 1,000 / 1 000), and so do the units (s / с, m / м). In English the Hafen is the **Harbor**, the Leitfisch the **Lead Fish**, the Schwarmruf the **Swarm Call**.
- **For changes:** the game code keeps writing German. A translation layer turns each text into the chosen language when it reaches the screen: page text (watched with a MutationObserver), text drawn on the canvas (`fillText`, `strokeText`, `measureText`) and messages. The dictionary `I18N_DATA` holds rows of `[German, English, Ukrainian]`; `{}` marks a number or name that is filled in. A new German text without a row stays German in EN and UA, so every new text needs a row. `webtest/browser_i18n.js` visits every screen in all languages and lists any text that still looks German; `I18N_LANG=en node webtest/net_checks.js` does the same for online messages.
- This guide keeps the German in-game names (Blasenring, Hafen, Leitfisch …) because they are the names in the code and in the German version.
