# Crystal Modern Move Migration Table

## Purpose

This document is the authoritative mapping for move ID replacements in Crystal
Modern. When an existing Gen 2 move ID is reused for a new move, the replacement
must be recorded here before implementation.

Move replacements are preferred over broad move table expansion when the old move
is obsolete, low-impact, or unsuitable for Crystal Modern's battle design.

## Status Key

- Approved: Design approved for implementation, but code has not been changed.
- Planned: Candidate replacement under discussion.
- Implemented: Replacement has been applied in code and tested.

## Phase A: Fairy Move Foundation

| Original move | Original move ID | Replacement move | New type | New category | Reason for replacement | Distribution impact | Status |
| --- | ---: | --- | --- | --- | --- | --- | --- |
| `BARRAGE` | `$8c` | `DISARMING_VOICE` | Fairy | Special | Weak, inaccurate Normal multi-hit move with little unique value. It is a low-disruption slot for an early Fairy attack. | Appeared only in two vanilla level-up entries and no TM/HM/trainer data. Those entries now use `EGG_BOMB` to preserve Exeggcute/Exeggutor flavor without granting accidental Fairy coverage. | Implemented |
| `SHARPEN` | `$9f` | `PLAY_ROUGH` | Fairy | Physical | Narrow Porygon-focused setup move with minimal distribution. Replacing it creates needed physical Fairy STAB without expanding move IDs. | Appeared in one vanilla level-up entry and no TM/HM/trainer data. That Porygon entry now uses `AGILITY` to avoid accidental Fairy coverage. | Implemented |
| `KINESIS` | `$86` | `MOONBLAST` | Fairy | Special | Obscure accuracy-drop move with very small distribution. The slot is suitable for the primary late-game special Fairy attack. | Appeared in two vanilla level-up entries and one trainer moveset. Abra/Kadabra/Alakazam references now use `FLASH` to preserve an accuracy-lowering role without granting accidental Fairy coverage. | Implemented |
| `PSYWAVE` | `$95` | `DRAINING_KISS` | Fairy | Special | Confusing variable-damage move with poor player clarity. Replacing it creates a simple Fairy sustain option using existing 50 percent drain behavior. | Appeared in one vanilla level-up entry and two egg move entries. Those references now use `CONFUSE_RAY` or `PSYBEAM` to avoid accidental Fairy coverage. | Implemented |

## Batch B: Core Coverage

| Original move | Original move ID | Replacement move | New type | New category | Reason for replacement | Distribution impact | Status |
| --- | ---: | --- | --- | --- | --- | --- | --- |
| `COMET_PUNCH` | `$04` | `SHADOW_CLAW` | Ghost | Physical | Low-power Normal multi-hit move with limited unique value. The slot adds a clear physical Ghost option while keeping `SHADOW_BALL` available. | Vanilla level-up and trainer references now use `MACH_PUNCH` or `MEGA_PUNCH` to avoid accidental Ghost coverage. | Implemented |
| `SMOG` | `$7b` | `POISON_JAB` | Poison | Physical | Weak, inaccurate Poison move whose role is covered by `POISON_GAS`, `SLUDGE`, and `SMOKESCREEN`. The slot adds needed physical Poison STAB. | Vanilla level-up and trainer references now use `POISON_GAS`, `SMOKESCREEN`, `EMBER`, `ROAR`, or `SLUDGE` depending on species role. | Implemented |
| `TWINEEDLE` | `$29` | `X_SCISSOR` | Bug | Physical | Beedrill-only legacy move with awkward low power. The slot adds a reliable physical Bug staple. | Vanilla Beedrill level-up and trainer references now use `PIN_MISSILE` to preserve Bug flavor without granting `X_SCISSOR` by accident. | Implemented |
| `SPIKE_CANNON` | `$83` | `FLASH_CANNON` | Steel | Special | Redundant Normal multi-hit move with sparse distribution. The slot adds a simple special Steel attack. | Vanilla Cloyster/Corsola/Omastar references now use `AURORA_BEAM`, `BUBBLEBEAM`, or `ANCIENTPOWER`. | Implemented |
| `CLAMP` | `$80` | `POWER_GEM` | Rock | Special | Inaccurate trapping move with narrow distribution and inherited trap text/AI hooks. The slot adds needed special Rock coverage. | Vanilla Shellder reference now uses `WHIRLPOOL`; Rain Dance AI and trap text references were removed so `POWER_GEM` does not inherit Clamp behavior. | Implemented |
| `RAZOR_WIND` | `$0d` | `AIR_SLASH` | Flying | Special | Two-turn Normal attack with poor clarity and low practical value. The slot adds a special Flying attack with a simple flinch effect. | Vanilla egg move references now use `GROWTH`, `WING_ATTACK`, or `SLASH`; charge-turn/high-crit metadata was removed from the old slot. | Implemented |
| `PRESENT` | `$d9` | `SEED_BOMB` | Grass | Physical | Confusing variable-damage/healing move with poor player clarity. The slot adds a clean physical Grass attack. | Vanilla level-up, egg, and trainer references now use nearby Normal/status/flavor moves such as `PECK`, `SWIFT`, `DIZZY_PUNCH`, `HEADBUTT`, or `DEFENSE_CURL`. | Implemented |

## Batch C: Polish Coverage

| Original move | Original move ID | Replacement move | New type | New category | Reason for replacement | Distribution impact | Status |
| --- | ---: | --- | --- | --- | --- | --- | --- |
| `DRAGON_RAGE` | `$52` | `DRAGON_PULSE` | Dragon | Special | Fixed 40 HP damage is useful early but poor for long-term balancing and custom move progression. The slot adds a clear special Dragon STAB option. | Vanilla level-up, trainer, Battle Tower, and egg move references now use `TWISTER` to preserve Dragon flavor without granting `DRAGON_PULSE` by accident. | Implemented |
| `VICEGRIP` | `$0b` | `DRAGON_CLAW` | Dragon | Physical | Redundant Normal physical attack with limited identity. The slot adds a simple physical Dragon STAB option. | Vanilla Krabby/Kingler/Pinsir and trainer references now use `BUBBLE`, `BIND`, or `STOMP` to avoid accidental Dragon coverage. | Implemented |
| `PIN_MISSILE` | `$2a` | `BUG_BITE` | Bug | Physical | Weak, inaccurate multi-hit move with awkward overlap after `X_SCISSOR` was added. The slot adds a compact mid-power Bug attack. | Vanilla Beedrill, Jolteon, Qwilfish, trainer, and egg move references now use `FURY_CUTTER`, `SWIFT`, `POISON_STING`, or `SPIKES` to avoid accidental Bug Bite distribution. | Implemented |

## Notes

- Phase A should not expand `NUM_ATTACKS`.
- Phase A should not add new TMs.
- Phase A should not change Hidden Power.
- Phase A should use existing move effects where practical.
- Batch B should not expand `NUM_ATTACKS`.
- Batch B should not add new TMs.
- Batch B should not intentionally distribute its new coverage to vanilla
  Pokemon; custom distribution belongs to the custom Pokedex pass.
- Batch C should not expand `NUM_ATTACKS`.
- Batch C should not add new TMs.
- `BUG_BITE` intentionally has no berry-eating effect for now.
- Old save files containing a replaced move ID will display and behave as the new
  move. This is expected for ID reuse and must be documented per milestone.
