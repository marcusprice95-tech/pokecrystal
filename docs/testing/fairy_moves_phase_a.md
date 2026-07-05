# Phase A Fairy Moves Manual Emulator Test Checklist

This checklist verifies the first Crystal Modern Fairy move batch:
`DISARMING_VOICE`, `PLAY_ROUGH`, `MOONBLAST`, and `DRAINING_KISS`.

Use a save state before each test. Record the ROM build, emulator, and any
temporary test fixtures. Do not commit temporary learnset, trainer, or species
fixtures used only for emulator testing.

Recommended setup:
- Use a temporary Fairy-type test Pokemon with all four Phase A moves.
- Use neutral, Dragon, Fighting, Dark, Fire, Poison, and Steel targets.
- Use equal-level Pokemon where possible.
- Ignore critical hits when comparing damage.

## Test Matrix

| ID | Behaviour | Suggested setup | Exact steps | Expected result | Pass/Fail notes |
| --- | --- | --- | --- | --- | --- |
| FMA-01 | Move names fit UI | Test Pokemon with all four moves | 1. Open the Pokemon move screen. 2. Enter battle and open the Fight menu. 3. Inspect all move names. | `DISARM VOICE`, `PLAY ROUGH`, `MOONBLAST`, and `DRAIN KISS` fit without overlap or corrupt text. |  |
| FMA-02 | Move data matches approved specs | Same test Pokemon | 1. Inspect battle move info if available. 2. Compare type/category/power/accuracy/PP to the approved specs. | Disarm Voice: Fairy/Special/40/100/15. Play Rough: Fairy/Physical/90/90/10. Moonblast: Fairy/Special/95/100/15. Drain Kiss: Fairy/Special/50/100/10. |  |
| FMA-03 | Disarming Voice always hits | User with lowered accuracy or target with raised evasion | 1. Lower the user's accuracy or raise target evasion. 2. Use Disarming Voice several times. | Disarming Voice continues to hit like an always-hit move. |  |
| FMA-04 | Play Rough uses Attack | Physical attacker with Play Rough vs neutral target | 1. Record non-critical damage. 2. Reload. 3. Raise Attack with X Attack and repeat. 4. Reload and raise Special Attack for comparison. | Play Rough damage follows Attack, not Special Attack. |  |
| FMA-05 | Moonblast uses Special Attack | Special attacker with Moonblast vs neutral target | 1. Record non-critical damage. 2. Reload. 3. Raise Special Attack with X Special and repeat. 4. Reload and raise Attack for comparison. | Moonblast damage follows Special Attack, not Attack. |  |
| FMA-06 | Draining Kiss uses Special Attack and drains | Special attacker with Draining Kiss vs neutral target | 1. Damage the user first. 2. Use Draining Kiss. 3. Compare recovered HP to damage dealt. | Draining Kiss deals special Fairy damage and restores HP using existing Crystal drain behavior: 50 percent of damage dealt, not the later 75 percent value. |  |
| FMA-07 | Play Rough secondary effect | Target with visible Attack stat stage impact | 1. Use Play Rough repeatedly from save states. 2. Watch battle messages. 3. Confirm later physical damage decreases after the drop. | Play Rough can lower target Attack. |  |
| FMA-08 | Moonblast secondary effect | Target with visible Special Attack impact | 1. Use Moonblast repeatedly from save states. 2. Watch battle messages. 3. Confirm later special damage decreases after the drop. | Moonblast can lower target Special Attack. |  |
| FMA-09 | Fairy super-effective matchups | Dragon, Fighting, and Dark targets | 1. Use each damaging Fairy move against each target type where practical. 2. Compare messages and damage. | Fairy moves are super-effective against Dragon, Fighting, and Dark. |  |
| FMA-10 | Fairy resisted matchups | Fire, Poison, and Steel targets | 1. Use each damaging Fairy move against each target type where practical. 2. Compare messages and damage. | Fairy moves are not very effective against Fire, Poison, and Steel. |  |
| FMA-11 | Animations look damaging | Test all four moves in battle | 1. Use each move. 2. Watch animation timing and graphics. 3. Repeat from both player and enemy sides. | Animations play cleanly, do not corrupt graphics, and read as attacks rather than healing moves. |  |
| FMA-12 | AI can use Fairy coverage | AI trainer with one Fairy move and one neutral move | 1. Battle with Dragon/Fighting/Dark targets and resisted targets. 2. Repeat several turns from save states. | AI can choose Fairy moves sensibly for type advantage and does not overvalue them into resisted targets. |  |
| FMA-13 | Old move references are cleaned | Vanilla Pokemon formerly using Barrage, Sharpen, Kinesis, or Psywave | 1. Inspect or encounter affected Pokemon/trainers. 2. Confirm their movesets. | Exeggcute/Exeggutor, Porygon, Abra/Kadabra/Alakazam, Misdreavus, Gastly, Koffing, and Psychic Mark do not accidentally receive Fairy coverage. |  |
| FMA-14 | No TM behaviour changed | TM/HM pocket and compatibility | 1. Inspect TM/HM list. 2. Use normal TMs. 3. Confirm no Phase A Fairy move appears as a TM. | No new Fairy TMs exist in Phase A and existing TM behavior is unchanged. |  |

## Additional Notes

- ROM build:
- Emulator/version:
- Save/setup used:
- Tester:
- Date:
- General pass/fail summary:
- Temporary fixtures used:
- UI issues observed:
- Animation issues observed:
- AI issues observed:
- Secondary effect notes:
- Crash/corruption notes:
