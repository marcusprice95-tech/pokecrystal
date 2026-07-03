# Physical/Special Split Manual Emulator Test Checklist

This checklist verifies the Crystal Modern Physical/Special split in an emulator.
Use a save state before each test, repeat damage checks several times, and ignore
critical hits when comparing damage ranges.

Recommended setup:
- Use Pokemon and moves available in vanilla Pokemon Crystal.
- Prefer equal-level test Pokemon where possible.
- Use X Attack, X Special, Growl, Charm, or Screech to make stat-source changes
  obvious.
- Record the ROM build, emulator, save file, and any temporary party/trainer setup
  used for the test.
- If a move's intended category is disputed, record the observed result and flag it
  for move-table review instead of changing engine code during testing.

## Test Matrix

| ID | Behaviour | Suggested vanilla setup | Exact steps | Expected result | Pass/Fail notes |
| --- | --- | --- | --- | --- | --- |
| PSS-01 | Fire Punch uses Attack | Electabuzz, Magmar, or Hitmonchan with Fire Punch vs a neutral target such as Raticate or Fearow | 1. Use Fire Punch several times and record non-critical damage. 2. Reload. 3. Use X Attack on the Fire Punch user, then use Fire Punch several times. 4. Optional: reload and use X Special instead. | Fire Punch damage increases after Attack is raised. X Special should not produce the same clear increase. STAB, if present, still applies normally. |  |
| PSS-02 | Flamethrower uses Special Attack | Typhlosion, Magmar, Arcanine, or Houndoom with Flamethrower vs a neutral target such as Raticate or Fearow | 1. Use Flamethrower several times and record non-critical damage. 2. Reload. 3. Use X Special on the Flamethrower user, then use Flamethrower several times. 4. Optional: reload and use X Attack instead. | Flamethrower damage increases after Special Attack is raised. X Attack should not produce the same clear increase. |  |
| PSS-03 | Shadow Ball uses Attack | Gengar, Misdreavus, Sneasel, or another TM30-compatible Pokemon with Shadow Ball vs a neutral target such as Girafarig or Noctowl | 1. Use Shadow Ball several times and record non-critical damage. 2. Reload. 3. Use X Attack, then use Shadow Ball several times. 4. Optional: reload and use X Special instead. | Shadow Ball damage follows Attack for this checklist. If it instead follows Special Attack, mark the test failed and review whether the move table should keep modern Shadow Ball as special or use the requested Crystal Modern behaviour. |  |
| PSS-04 | Bite category behaviour | Crobat, Umbreon, Houndour, Houndoom, or Feraligatr with Bite vs a neutral target | 1. Record Bite damage. 2. Reload. 3. Raise Attack with X Attack and record Bite damage. 4. Reload. 5. Raise Special Attack with X Special and record Bite damage. | Bite should follow its assigned move category. For the current Crystal Modern checklist, Bite is expected to behave as physical: Attack changes damage; Special Attack does not. |  |
| PSS-05 | Crunch category behaviour | Houndoom, Tyranitar, or another Crunch user vs a neutral target | 1. Record Crunch damage. 2. Reload. 3. Raise Attack with X Attack and record Crunch damage. 4. Reload. 5. Raise Special Attack with X Special and record Crunch damage. | Crunch should follow its assigned move category. If Crystal Modern intends modern Dark coverage, Crunch should behave as physical. If it behaves as special, flag the move table for design review. |  |
| PSS-06 | Counter only works on physical moves | Wobbuffet, Heracross, Hitmonlee, or another Counter user vs opponents with Tackle, Headbutt, Fire Punch, Water Gun, or Flamethrower | 1. Let the Counter user take a physical hit such as Tackle, Headbutt, or Fire Punch. 2. Use Counter. 3. Reload. 4. Let the Counter user take a special hit such as Water Gun or Flamethrower. 5. Use Counter. | Counter succeeds only after physical damaging moves and fails after special damaging moves. Fire Punch should count as physical. |  |
| PSS-07 | Mirror Coat only works on special moves | Wobbuffet with Mirror Coat vs opponents with Water Gun, Flamethrower, Tackle, Headbutt, or Fire Punch | 1. Let Wobbuffet take a special hit such as Water Gun or Flamethrower. 2. Use Mirror Coat. 3. Reload. 4. Let Wobbuffet take a physical hit such as Tackle, Headbutt, or Fire Punch. 5. Use Mirror Coat. | Mirror Coat succeeds only after special damaging moves and fails after physical damaging moves. Flamethrower should count as special. |  |
| PSS-08 | Hidden Power remains special | Unown with Hidden Power, or any Pokemon taught Hidden Power, vs a neutral target | 1. Record Hidden Power damage. 2. Reload. 3. Raise Special Attack with X Special and record Hidden Power damage. 4. Reload. 5. Raise Attack with X Attack and record Hidden Power damage. | Hidden Power damage follows Special Attack regardless of its calculated type. Its calculated type should still affect effectiveness. |  |
| PSS-09 | STAB and type effectiveness still work | Typhlosion with Flamethrower vs Bellsprout; Feraligatr with Surf vs Geodude or Onix; Ampharos with ThunderPunch vs Gyarados; any non-STAB comparison user if available | 1. Use a same-type attack and record damage. 2. Compare against a similar non-STAB user if available. 3. Test super-effective, resisted, and immune matchups. | STAB still boosts damage. Super-effective, not-very-effective, and immune messages and damage still match the Gen 2 type chart currently implemented by the engine. |  |
| PSS-10 | Conversion does not produce invalid types | Porygon or Porygon2 with Conversion and a mixed move set such as Tackle, Psybeam, Thunderbolt, Ice Beam, or Shadow Ball | 1. Use Conversion repeatedly across different move sets. 2. Check the resulting type text in battle/status displays where visible. 3. Attack and be attacked after Conversion. | Conversion changes the user only to a valid raw type, never to PHYSICAL, SPECIAL, STATUS, blank text, or corrupt text. Battle continues without crash or display corruption. |  |
| PSS-11 | Conversion2 does not produce invalid types | Porygon or Porygon2 with Conversion2 vs opponents using Tackle, Flamethrower, ThunderPunch, Bite, Shadow Ball, or Hidden Power | 1. Let Porygon take a damaging move. 2. Use Conversion2. 3. Repeat with physical, special, and Hidden Power moves. | Conversion2 selects only a valid raw type that resists or is immune to the previous move's raw type. It never selects PHYSICAL, SPECIAL, STATUS, blank text, or corrupt text. |  |
| PSS-12 | Battle move info UI displays category and type cleanly | Any party Pokemon with mixed moves, for example Typhlosion with Fire Punch and Flamethrower, Houndoom with Bite and Crunch, or Unown with Hidden Power | 1. Enter battle. 2. Open the Fight menu. 3. Inspect each move's displayed type/category/power/accuracy information. 4. Check all four move slots where possible. | Type and category are readable and do not overlap move names, PP, power, accuracy, battle text, or screen borders. Hidden Power should display without corrupt category/type text. |  |
| PSS-13 | Pokemon move screen UI displays category and type cleanly | Party Pokemon with mixed physical, special, and status moves, for example Typhlosion, Houndoom, Porygon2, or Wobbuffet | 1. Open the party menu. 2. View the Pokemon's move details screen. 3. Inspect each move slot. 4. Repeat with long move names such as Flamethrower, ThunderPunch, Hidden Power, and Mirror Coat. | Type/category information is readable and does not overlap move names, PP, descriptions, screen borders, or other UI text. Status moves display as status rather than physical or special. |  |
| PSS-14 | AI still chooses sensible super-effective moves | Controlled trainer or link-style test with opponents such as Ampharos/Electabuzz with ThunderPunch vs Gyarados, Jynx with Ice Punch vs Dragonite, Typhlosion/Magmar with Flamethrower vs Forretress or Scizor, Houndoom with Bite/Crunch vs Alakazam | 1. Fight an AI-controlled Pokemon that has at least one super-effective damaging move and one neutral or resisted damaging move. 2. Repeat from a save state for several turns. 3. Include both physical and special super-effective moves. | AI continues to prefer sensible super-effective attacks often enough to look intentional. It should not ignore super-effective moves because category bits are mixed into type data. |  |

## Additional Notes

Use this section for emulator observations that do not fit a single row.

- ROM build:
- Emulator/version:
- Save/setup used:
- Tester:
- Date:
- General pass/fail summary:
- Move category decisions needing review:
- UI issues observed:
- AI issues observed:
- Crash/corruption notes:
