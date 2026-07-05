# Burn Correctness Test Checklist

Use this checklist for manual emulator testing after `Make burn physical-only`.
Mark each item pass/fail and record the ROM, save, party, opponent, and move used.

## Build And Data Checks

| Test | Expected result | Pass/Fail notes |
| --- | --- | --- |
| Clean build | `make clean && make` completes successfully. | |
| Manifest | `ENGINE_MANIFEST.md` documents burn as physical-only with 1/8 residual damage. | |
| No critical-hit changes | Critical-hit multiplier and crit chance behavior are unchanged in this commit. | |

## Damage Behavior

| Test | Suggested setup | Expected result | Pass/Fail notes |
| --- | --- | --- | --- |
| Physical move while burned | Burn a physical attacker and compare `TACKLE`, `BODY_SLAM`, `SHADOW_CLAW`, or another Physical move against the same target before/after burn. | Physical move damage is reduced while burned. | |
| Special move while burned | Burn a special attacker and compare `FLAMETHROWER`, `SURF`, `THUNDERBOLT`, or another Special move against the same target before/after burn. | Special move damage is not reduced by burn. | |
| Physical/Special split regression | Use a same-type pair such as `FIRE_PUNCH` and `FLAMETHROWER` from the same burned Pokemon. | `FIRE_PUNCH` is reduced; `FLAMETHROWER` is not. | |
| Minimum damage | Use a very weak burned physical attacker against a high-defense target. | Physical damage remains at least 1 before final battle damage flooring. | |

## Residual Damage

| Test | Suggested setup | Expected result | Pass/Fail notes |
| --- | --- | --- | --- |
| Burn residual | Burn any Pokemon with easy-to-count max HP. | End-of-turn burn damage remains 1/8 max HP. | |
| Faint from burn | Leave a burned Pokemon at low HP. | Burn residual can still faint the Pokemon normally. | |

## Stat And Switch Regression

| Test | Expected result | Pass/Fail notes |
| --- | --- | --- |
| Attack stat display/derived behavior | Burn should not act as a persistent Attack stat rewrite; its reduction is applied to physical move damage. | |
| Switch while burned | Switch a burned Pokemon out and back in, then use a Physical and Special move. | Physical damage is still reduced; Special damage is still not reduced. | |
| Stat stages | Apply Attack boosts/drops while burned and use a Physical move. | Stat stages and burn damage reduction both apply without affecting Special damage. | |

## Immunity And Cure Regression

| Test | Expected result | Pass/Fail notes |
| --- | --- | --- |
| Fire-type burn immunity | Fire-type targets still cannot be burned by standard burn effects. | |
| Burn cure item | Burn Heal, Full Heal, or equivalent status cure removes burn and removes the physical damage reduction. | |
| Held burn cure | Existing held-item burn cure behavior still works. | |
