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
| `BARRAGE` | `$8c` | `DISARMING_VOICE` | Fairy | Special | Weak, inaccurate Normal multi-hit move with little unique value. It is a low-disruption slot for an early Fairy attack. | Appears only in two vanilla level-up entries and no TM/HM/trainer data. Existing references must be reviewed so no species inherits Fairy coverage accidentally. | Approved |
| `SHARPEN` | `$9f` | `PLAY_ROUGH` | Fairy | Physical | Narrow Porygon-focused setup move with minimal distribution. Replacing it creates needed physical Fairy STAB without expanding move IDs. | Appears in one vanilla level-up entry and no TM/HM/trainer data. The old Porygon learnset reference must be replaced or removed deliberately. | Approved |
| `KINESIS` | `$86` | `MOONBLAST` | Fairy | Special | Obscure accuracy-drop move with very small distribution. The slot is suitable for the primary late-game special Fairy attack. | Appears in two vanilla level-up entries and one trainer moveset. Abra/Kadabra and the trainer reference must be updated to avoid accidental Fairy coverage. | Approved |
| `PSYWAVE` | `$95` | `DRAINING_KISS` | Fairy | Special | Confusing variable-damage move with poor player clarity. Replacing it creates a simple Fairy sustain option using existing drain behavior. | Appears in one vanilla level-up entry and two egg move entries. These references must be reviewed during implementation. | Approved |

## Notes

- Phase A should not expand `NUM_ATTACKS`.
- Phase A should not add new TMs.
- Phase A should not change Hidden Power.
- Phase A should use existing move effects where practical.
- Old save files containing a replaced move ID will display and behave as the new
  move. This is expected for ID reuse and must be documented per milestone.
