# Blobfisch Survivors and Blobfisch Survivors Lite: changelog

Release of 2026-10-23, built from the six change requests of 2026-10-18.
All six changes are in the browser game (`index.html`) and in Lite (`.sb3` / standalone `.html`) with the same numbers, unless noted.
`guide.md` has been rewritten to match.

## 1. Bosses are harder

- **More life.** Base HP is now 2,200 / 2,400 / 2,500 / 3,200 for Hai-König / Riesenkrake / Meeresungeheuer / Lava-Titan (was 750 / 1,350 / 2,100 / 3,000).
- **HP scaling.** HP is multiplied by the stage factor, by +15 % for every earlier appearance in the run, and by a level factor `clamp((level / 21)^1.3, 0.7, 6)`. Bosses stay a threat however fast you level. Damage grows +20 % per earlier appearance.
- **Three phases.** At 66 % and 33 % life the boss roars (1.1 s), shoots a ring of projectiles and calls helpers (Kleine Haie, Quallen, Tintenfische or Krebse, depending on the boss). The HUD shows `×N · Phase N`, with notches on the life bar.
- **Tiers.** Each boss fights with attacks of tier `min(3, phase + appearance − 1)`. Later phases and later appearances add more charges, slams, rings, spirals and magma waves. Speed is ×1 / 1.1 / 1.2 and delays are ×1 / 0.85 / 0.7 per tier.
- **Duel rule.** While a boss lives, waves bring half as many enemies (at least 1) at a 1.4× longer interval, with no elites, and the Piranha ring waits.
- **Loot.** A heart (+40 % max life) and 8–13 pearls worth `pearl value × (2 + appearance)`.

## 2. Pearls and economy

- **Pearls scale with the map.** Chance per kill × value per pearl is 0.11 × 1 (Korallenriff), 0.22 × 1 (Kelpwald), 0.165 × 2 (Tiefsee-Graben), 0.22 × 2 (Vulkanschlucht). That is ×1 / ×2 / ×3 / ×4 pearls per kill compared with the Korallenriff, and the stage cards show the multiplier.
- **Elites** drop +3 pearls.
- **Maxed level-ups.** A level-up where everything is already maxed gives 3 × pearl value.
- **Shop.** Prices now rise per purchase (`base × multiplier^n`): 40×2, 35×1.9, 55×2.1, 35×1.9, 70×2.4, and 300 for Zweite Chance. Buying everything costs **6,022** pearls (was 3,366).

## 3. Blasenring (Bubble Ring)

- No bubble ever pops up to ring level 3.
- From level 4, every enemy shot a bubble blocks wears that bubble: cracks, a pink tint and trembling, plus a `⭕ 8/8` pill in the HUD.
- After 12 hits a bubble pops. At most one pop per 50 s, and no new pop until a level-up has been offered. The remaining bubbles are relieved to at most 6 hits.
- The next level-up always shows the ring card (pinned).
  - At ring level 4 this is the normal upgrade to level 5, which brings a full ring.
  - At ring level 5 it is the new free **Mehr Blasen** card. It restores every missing bubble and repairs all cracks, and appears only while a bubble is missing.
- Other upgrades are never punished.

## 4. Pearls and XP orbs drift together

- Far-away orbs and pearls no longer vanish when merged. Off-screen ones combine invisibly. On-screen ones, which only merge when the field is crowded (over 200 orbs in the browser game, over 160 in Lite), drift slowly into the first orb of their patch and add up on arrival.
- An orb that comes within pickup reach becomes a single orb again. Hearts never merge.

## 5. More detailed lava and bosses

- **Bosses:** three look phases per boss, with auras, scars and glowing veins in later phases, extra animation frames, and tired poses for the Hai-König.
- **Lava:** cracked lava pools with warning rings in the heat stages, tentacle slams and magma arcs.
- **Lite:** bosses and lava are pre-drawn frames (3 phases × 3 animation frames × 2 facings per boss). The browser game animates them live.

## 6. Achievements

- Unlocking and claiming are now separate. A new achievement gets a gold **NEU** tag, the menu button shows an "N NEU" badge, and you collect rewards by hand with **Einlösen** (per row) or **Alle einlösen** (when two or more are waiting).
- The game-over screen lists new achievements with a shortcut button instead of showing a banner.
- Rows are sorted new → claimed → locked. Rewards are unchanged (810 pearls in total).
- Old saves count their existing achievements as already claimed.

## Also changed

- **Browser game only:** fixed a freeze after Zweite Chance (the revival emptied the enemy projectile list while the game loop was still going through it).
- The achievement banner no longer covers the game-over panel.
- The instructions are split into three balanced pages and now cover pearls, bosses, defence and achievements.
- `guide.md` is rewritten for this version. It covers boss formulas, the pearl and shop tables, ring wear and claiming, and it was checked against the code.

## Lite notes

- Files: the `.sb3` is about 6.9 MB and the standalone `.html` about 10.4 MB.
- Lite still has no mid-run resume. Progress uses the same saved variables as before. Achievements now also store a claimed state, and saves from the first Lite version are migrated automatically (their achievements count as claimed).

## Tuning knobs

| What | Browser game (`index.html`) | Lite (`gen/`) |
|---|---|---|
| Boss HP, damage, speed | `BOSS_TYPES` | `defs.py` `BOSS_TYPES` |
| Boss delays and speed per tier | `BOSS_CD`, `BOSS_SPD` | `defs.py` |
| Encounter +15 %, level factor | `spawnEnemy` (`encounterMult`, `levelMult`) | `m_core.py` (`encm`, `lvm`) |
| Boss heart (+40 %) | `killEnemy` | `m_core.py` |
| Pearl chance and value per map | `STAGES` | `defs.py` `STAGES` |
| Shop prices | `SHOP_UPGRADES` | `defs.py` `SHOP` |
| Ring wear | `RING_*` constants | `m_core.py` constants |
| Orb merge threshold | `mergeFarPickups` | `m_core.py` |

Possible follow-up: boss pearl loot uses the stage's pearl value (1 / 1 / 2 / 2), so the Kelpwald boss pays the same as the Riff boss.
