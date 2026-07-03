# Fairy Type Chart Manual Emulator Test Checklist

This checklist verifies the Crystal Modern Fairy type and modern type chart in an
emulator. Use a save state before each test, record the ROM build and emulator,
and ignore unrelated critical hits or damage variance when checking effectiveness.

Recommended setup:
- Use temporary debug parties, edited learnsets, or a controlled test trainer if
  needed. The current engine has Fairy status moves but no Fairy damaging move.
- Use a temporary Fairy-type test Pokemon only for manual testing until official
  species retcons are designed.
- Do not commit temporary species, learnset, trainer, or move edits used only to
  create test fixtures.
- Check both battle messages and damage behaviour where a damaging move is
  involved.

## Test Matrix

| ID | Behaviour | Suggested setup | Exact steps | Expected result | Pass/Fail notes |
| --- | --- | --- | --- | --- | --- |
| FTY-01 | Fairy type display | Temporary Fairy-type Pokemon, or a Pokemon temporarily given Fairy as one of its base types | 1. Open the Pokemon's stats/status screen. 2. Inspect the type label. 3. View the Pokemon in battle if type text is shown by the current debug setup. | `FAIRY` displays as readable type text with no blank, corrupt, or overlapping characters. |  |
| FTY-02 | Pokédex Fairy search | At least one seen/caught Pokemon temporarily assigned Fairy type | 1. Open the Pokédex. 2. Use type search. 3. Select Fairy. 4. Confirm the result list. | Fairy appears as a selectable Pokédex search type, and Fairy-type species appear in the result list. |  |
| FTY-03 | Fairy vs Dragon is super-effective | Temporary Fairy damaging test move, or temporarily retype a simple damaging move such as Pound to Fairy; target Dragonite, Dragonair, Dratini, or Kingdra | 1. Use the Fairy-type damaging move against a Dragon-type target. 2. Repeat against a neutral target for comparison. | Damage/message indicate Fairy is super-effective against Dragon. |  |
| FTY-04 | Dragon vs Fairy has no effect | Temporary Fairy-type target; Dragonite/Dragonair/Kingdra using DragonBreath, Twister, or another Dragon-type damaging move | 1. Use a Dragon-type damaging move against the Fairy-type target. 2. Repeat against a non-Fairy target to confirm the move itself works. | Dragon-type damage has no effect on Fairy. Battle shows the no-effect message and applies no damage. |  |
| FTY-05 | Poison vs Fairy is super-effective | Temporary Fairy-type target; Poison user with Sludge Bomb, Sludge, Poison Sting, or Acid | 1. Use a Poison-type damaging move against the Fairy-type target. 2. Repeat against a neutral target for comparison. | Poison is super-effective against Fairy. |  |
| FTY-06 | Steel vs Fairy is super-effective | Temporary Fairy-type target; Steelix, Scizor, Skarmory, or Forretress with Steel Wing or Iron Tail | 1. Use a Steel-type damaging move against the Fairy-type target. 2. Repeat against a neutral target for comparison. | Steel is super-effective against Fairy. |  |
| FTY-07 | Fighting vs Fairy is resisted | Temporary Fairy-type target; Fighting user with Karate Chop, Mach Punch, DynamicPunch, or Cross Chop | 1. Use a Fighting-type damaging move against the Fairy-type target. 2. Repeat against a neutral target for comparison. | Fighting is not very effective against Fairy. |  |
| FTY-08 | Bug vs Fairy is resisted | Temporary Fairy-type target; Bug user with Fury Cutter, Twineedle, or Megahorn | 1. Use a Bug-type damaging move against the Fairy-type target. 2. Repeat against a neutral target for comparison. | Bug is not very effective against Fairy. |  |
| FTY-09 | Dark vs Fairy is resisted | Temporary Fairy-type target; Dark user with Bite, Crunch, Pursuit, or Faint Attack | 1. Use a Dark-type damaging move against the Fairy-type target. 2. Repeat against a neutral target for comparison. | Dark is not very effective against Fairy. |  |
| FTY-10 | Ghost vs Steel is neutral | Steelix, Scizor, Skarmory, Forretress, or Magnemite/Magneton as target; Ghost user with Shadow Ball, Lick, or Night Shade where appropriate | 1. Use a Ghost-type damaging move against a Steel-type target. 2. Compare against a neutral target. | Ghost is neutral against Steel; it should not show a not-very-effective message solely because the target is Steel. |  |
| FTY-11 | Dark vs Steel is neutral | Steelix, Scizor, Skarmory, Forretress, or Magnemite/Magneton as target; Dark user with Bite, Crunch, Pursuit, or Faint Attack | 1. Use a Dark-type damaging move against a Steel-type target. 2. Compare against a neutral target. | Dark is neutral against Steel; it should not show a not-very-effective message solely because the target is Steel. |  |
| FTY-12 | Hidden Power never becomes Fairy | Unown with Hidden Power, or any Pokemon with Hidden Power; several DVs/IV setups if available | 1. Use Hidden Power across multiple Pokemon or save fixtures with different Hidden Power types. 2. Check displayed/calculated effectiveness against targets with known weaknesses. 3. Include Fairy-type targets if temporary test fixtures exist. | Hidden Power may resolve only to its supported legacy type set. It never resolves to Fairy and does not display Fairy as its calculated type. |  |
| FTY-13 | Conversion works with Fairy present | Porygon or Porygon2 with Conversion and at least one Fairy-type move in its move list, such as Sweet Kiss, Charm, Moonlight, or a temporary Fairy damaging move | 1. Use Conversion repeatedly with move sets containing Fairy moves. 2. Inspect resulting type display when visible. 3. Continue battle after the type change. | Conversion can select Fairy as a valid raw type when appropriate. It never selects category bits, blank text, corrupt text, or an invalid type. |  |
| FTY-14 | Conversion2 works with Fairy present | Porygon or Porygon2 with Conversion2; opponents using Fairy, Dragon, Poison, Steel, Fighting, Bug, Dark, Ghost, and Steel-relevant test moves where possible | 1. Let Porygon take a damaging move. 2. Use Conversion2. 3. Repeat with moves that interact with Fairy and modern Steel neutrality. | Conversion2 chooses only valid raw types and respects the updated type chart. It must not produce corrupt type text or invalid category-coded types. |  |

## Additional Notes

Use this section for emulator observations that do not fit a single row.

- ROM build:
- Emulator/version:
- Save/setup used:
- Tester:
- Date:
- General pass/fail summary:
- Temporary fixtures used:
- Type display issues observed:
- Pokédex search issues observed:
- Battle message/effectiveness issues observed:
- Conversion/Conversion2 issues observed:
- Crash/corruption notes:
