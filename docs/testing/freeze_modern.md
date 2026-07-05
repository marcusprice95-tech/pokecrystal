# Freeze Modernization Manual Test Checklist

Crystal Modern keeps freeze as a rare hard status, but modernizes natural thawing to approximately 20 percent per action check. Frostbite is intentionally out of scope.

## Build And Data Checks

- [ ] `make clean && make` passes.
- [ ] `ENGINE_MANIFEST.md` documents the modern freeze behavior.
- [ ] No critical-hit, burn, sleep, or confusion logic changed in the freeze commit.

## Natural Thaw Chance

Suggested setup:
- Use Ice Punch, Ice Beam, Blizzard, or another move capable of freezing.
- Test against a durable target that can survive multiple turns after being frozen.

Expected result:
- A frozen Pokemon remains unable to move while frozen.
- On later action checks, it has an approximately 20 percent chance to thaw naturally.
- A Pokemon should not thaw from this random check on the exact turn it was frozen.

Pass/fail notes:

| Case | Pass? | Notes |
| --- | --- | --- |
| Natural thaw occurs across repeated trials |  |  |
| Natural thaw feels closer to 20 percent than vanilla 10 percent |  |  |
| Newly frozen Pokemon does not immediately random-thaw |  |  |

## Fire Moves Thaw The Target

Suggested moves:
- Ember
- Fire Punch
- Flamethrower
- Fire Blast
- Sacred Fire

Expected result:
- If a frozen Pokemon is hit by these Fire damaging moves and survives, it is thawed by the move script.
- Damage and type effectiveness still resolve normally.

Pass/fail notes:

| Move | Pass? | Notes |
| --- | --- | --- |
| Ember thaws frozen target |  |  |
| Fire Punch thaws frozen target |  |  |
| Flamethrower thaws frozen target |  |  |
| Fire Blast thaws frozen target |  |  |
| Sacred Fire thaws frozen target |  |  |

## Self-Thaw Moves

Suggested moves:
- Flame Wheel
- Sacred Fire

Expected result:
- A frozen user can select Flame Wheel or Sacred Fire.
- The move bypasses the normal "frozen solid" failure path.
- The user thaws as part of the move's effect.

Pass/fail notes:

| Move | Pass? | Notes |
| --- | --- | --- |
| Flame Wheel can be used while frozen and thaws the user |  |  |
| Sacred Fire can be used while frozen and thaws the user |  |  |

## Non-Fire Moves

Suggested moves:
- Tackle
- Surf
- Thunderbolt
- Psychic

Expected result:
- Frozen Pokemon cannot use normal moves until thawed.
- Non-Fire damaging moves do not thaw a frozen target.
- Non-Fire moves do not bypass the frozen-solid failure path.

Pass/fail notes:

| Case | Pass? | Notes |
| --- | --- | --- |
| Frozen user cannot use ordinary moves |  |  |
| Non-Fire damage does not thaw target |  |  |
| Status move does not thaw user or target |  |  |

## Party And HUD Consistency

Expected result:
- When a Pokemon thaws naturally, its battle HUD status clears.
- Its party status clears as well.
- If an opposing trainer Pokemon thaws, the opponent party status remains consistent.

Pass/fail notes:

| Case | Pass? | Notes |
| --- | --- | --- |
| Player HUD clears FRZ after thaw |  |  |
| Player party status clears FRZ after thaw |  |  |
| Enemy HUD clears FRZ after thaw |  |  |
| Trainer enemy party status clears FRZ after thaw |  |  |

## Known Limitations

- Freeze remains a hard "cannot move" status.
- Crystal Modern does not add Frostbite.
- The random thaw chance should be validated by repeated emulator testing rather than a single trial.
