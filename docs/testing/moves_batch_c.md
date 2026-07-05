# Batch C Polish Moves Test Checklist

Use this checklist for manual emulator testing after `Add Batch C polish moves`.
Mark each item pass/fail and record the ROM, save, map, party, and opponent used.

## Build And Data Checks

| Test | Expected result | Pass/Fail notes |
| --- | --- | --- |
| Clean build | `make clean && make` completes successfully. | |
| Move constants | `DRAGON_RAGE`, `VICEGRIP`, and `PIN_MISSILE` do not appear in active move data, learnsets, trainer parties, egg moves, Battle Tower parties, or battle effect checks. | |
| Move names | `DRAGONPULSE`, `DRAGON CLAW`, and `BUG BITE` display without obvious overlap in battle and move-summary UI. | |
| TM list | No new TMs are added for Batch C moves. | |

## Move Behavior

| Move | Suggested setup | Expected result | Pass/Fail notes |
| --- | --- | --- | --- |
| `DRAGON_PULSE` | Teach the reused `$52` slot to a test Pokemon and battle a Dragon-type and a Fairy-type target. | Dragon / Special / 85 power / 100 accuracy / 10 PP. Uses Special Attack and Special Defense. No secondary effect. Fairy is immune. | |
| `DRAGON_CLAW` | Teach the reused `$0b` slot to a test Pokemon and battle a Dragon-type and a Fairy-type target. | Dragon / Physical / 80 power / 100 accuracy / 15 PP. Uses Attack and Defense. No secondary effect. Fairy is immune. | |
| `BUG_BITE` | Teach the reused `$2a` slot to a test Pokemon and battle a Psychic-, Dark-, or Grass-type target. | Bug / Physical / 60 power / 100 accuracy / 20 PP. Uses Attack and Defense. No secondary effect. Does not eat or consume held berries. | |

## Type And Category Regression

| Test | Expected result | Pass/Fail notes |
| --- | --- | --- |
| Dragon type chart | `DRAGON_PULSE` and `DRAGON_CLAW` are super-effective against Dragon, resisted by Steel, and have no effect on Fairy. | |
| Bug type chart | `BUG_BITE` follows the modern Crystal Modern Bug matchups. | |
| Physical categories | `DRAGON_CLAW` and `BUG_BITE` use Attack and Defense. Burn Attack reduction should affect their damage. | |
| Special category | `DRAGON_PULSE` uses Special Attack and Special Defense. Burn Attack reduction should not affect its damage. | |
| STAB | A Pokemon matching each move type receives STAB. | |

## Distribution Regression

| Area | Expected result | Pass/Fail notes |
| --- | --- | --- |
| Vanilla level-up moves | Vanilla Pokemon that previously learned old Batch C moves do not accidentally learn `DRAGON_PULSE`, `DRAGON_CLAW`, or `BUG_BITE`. | |
| Vanilla trainer parties | Trainers that previously used old Batch C moves do not accidentally use `DRAGON_PULSE`, `DRAGON_CLAW`, or `BUG_BITE`. | |
| Battle Tower parties | Battle Tower sets that previously used `DRAGON_RAGE` do not accidentally use `DRAGON_PULSE`. | |
| Vanilla egg moves | Egg move lists do not accidentally grant the new Batch C moves. | |
| Custom distribution | Any future custom Pokemon or trainer use of Batch C moves must be added deliberately in a separate content pass. | |

## Animation Regression

| Move | Expected reused animation | Pass/Fail notes |
| --- | --- | --- |
| `DRAGON_PULSE` | Dragonbreath-style animation. | |
| `DRAGON_CLAW` | Slash-style animation. | |
| `BUG_BITE` | Bite-style animation. | |

## AI Smoke Tests

| Test | Expected result | Pass/Fail notes |
| --- | --- | --- |
| Super-effective choice | Trainer AI still prefers a Batch C move when it is the clearly strongest super-effective option. | |
| Fixed-damage regression | `DRAGON_PULSE` no longer deals fixed 40 HP damage. | |
| Berry-effect regression | `BUG_BITE` does not eat, steal, or consume berries. | |
