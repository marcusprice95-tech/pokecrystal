# Batch B Coverage Moves Test Checklist

Use this checklist for manual emulator testing after `Add Batch B coverage moves`.
Mark each item pass/fail and record the ROM, save, map, party, and opponent used.

## Build And Data Checks

| Test | Expected result | Pass/Fail notes |
| --- | --- | --- |
| Clean build | `make clean && make` completes successfully. | |
| Move constants | `COMET_PUNCH`, `SMOG`, `TWINEEDLE`, `SPIKE_CANNON`, `CLAMP`, `RAZOR_WIND`, and `PRESENT` do not appear in active move data, learnsets, trainer parties, egg moves, AI helper lists, or battle effect checks. | |
| Move names | `SHADOW CLAW`, `POISON JAB`, `X-SCISSOR`, `FLASH CANNON`, `POWER GEM`, `AIR SLASH`, and `SEED BOMB` display without obvious overlap in battle and move-summary UI. | |
| TM list | No new TMs are added for Batch B moves. | |

## Move Behavior

| Move | Suggested setup | Expected result | Pass/Fail notes |
| --- | --- | --- | --- |
| `SHADOW_CLAW` | Teach the reused `$04` slot to a test Pokemon and battle a Psychic- or Ghost-type target. | Ghost / Physical / 70 power / 100 accuracy / 15 PP. Uses Attack and Defense. Has a high critical-hit ratio. | |
| `POISON_JAB` | Teach the reused `$7b` slot and battle a neutral target. | Poison / Physical / 80 power / 100 accuracy / 20 PP. Uses Attack and Defense. Has a 30 percent poison chance. | |
| `X_SCISSOR` | Teach the reused `$29` slot and battle a Psychic-, Dark-, or Grass-type target. | Bug / Physical / 80 power / 100 accuracy / 15 PP. No secondary effect. | |
| `FLASH_CANNON` | Teach the reused `$83` slot and battle a neutral target. | Steel / Special / 80 power / 100 accuracy / 10 PP. Uses Special Attack and Special Defense. Has a 10 percent Special Defense drop chance. | |
| `POWER_GEM` | Teach the reused `$80` slot and battle a Flying-, Fire-, Bug-, or Ice-type target. | Rock / Special / 80 power / 100 accuracy / 20 PP. No trap effect, no Clamp text, and no Rain Dance AI association. | |
| `AIR_SLASH` | Teach the reused `$0d` slot and battle a neutral target. | Flying / Special / 75 power / 95 accuracy / 15 PP. Has a 30 percent flinch chance. Does not charge for one turn or show Razor Wind preparation text. | |
| `SEED_BOMB` | Teach the reused `$d9` slot and battle a Water-, Ground-, or Rock-type target. | Grass / Physical / 80 power / 100 accuracy / 15 PP. No Present random power or healing behavior. | |

## Type And Category Regression

| Test | Expected result | Pass/Fail notes |
| --- | --- | --- |
| Physical categories | `SHADOW_CLAW`, `POISON_JAB`, `X_SCISSOR`, and `SEED_BOMB` use Attack and Defense. Burn Attack reduction should affect their damage. | |
| Special categories | `FLASH_CANNON`, `POWER_GEM`, and `AIR_SLASH` use Special Attack and Special Defense. Burn Attack reduction should not affect their damage. | |
| Type effectiveness | Ghost, Poison, Bug, Steel, Rock, Flying, and Grass effectiveness follows the modern Crystal Modern type chart. | |
| STAB | A Pokemon matching each move type receives STAB. | |

## Distribution Regression

| Area | Expected result | Pass/Fail notes |
| --- | --- | --- |
| Vanilla level-up moves | Vanilla Pokemon that previously learned old Batch B moves do not accidentally learn the new Batch B coverage moves. | |
| Vanilla trainer parties | Trainers that previously used old Batch B moves do not accidentally use the new Batch B coverage moves. | |
| Vanilla egg moves | Egg move lists do not accidentally grant the new Batch B coverage moves. | |
| Custom distribution | Any future custom Pokemon or trainer use of Batch B moves must be added deliberately in a separate content pass. | |

## Animation Regression

| Move | Expected reused animation | Pass/Fail notes |
| --- | --- | --- |
| `SHADOW_CLAW` | Slash-style animation. | |
| `POISON_JAB` | Poison Sting-style animation. | |
| `X_SCISSOR` | Cut-style animation. | |
| `FLASH_CANNON` | Zap Cannon-style animation. | |
| `POWER_GEM` | AncientPower-style animation. | |
| `AIR_SLASH` | Gust-style animation. | |
| `SEED_BOMB` | Egg Bomb-style animation. | |

## AI Smoke Tests

| Test | Expected result | Pass/Fail notes |
| --- | --- | --- |
| Super-effective choice | Trainer AI still prefers a Batch B move when it is the clearly strongest super-effective option. | |
| Rain Dance helper | Rain Dance AI is not encouraged by `POWER_GEM`. | |
| Old trap helper | `POWER_GEM` never applies trapping turns or Clamp battle text. | |
