# Crystal Modern Engine Manifest

## Base

- Upstream base commit: `06ec23cce` (`Fix some issues with C tools, and build them with -std=c17 (#1259)`)
- Engine branch: `engine-modernisation`
- Source branch point: `master` / `origin/master`
- Content branch separation: custom Pokemon content such as the Snom/Hoothoot changes currently belongs outside this engine branch.
- Save format version: TBD
- Link compatibility policy: TBD

## Battle Mechanics

- Physical/Special split: Not implemented
- Fairy type: Not implemented
- Type chart: Vanilla Pokemon Crystal
- Battle bug fixes applied: None in this branch yet
- Known battle limitations: Vanilla battle mechanics and known Crystal bugs still apply unless documented otherwise.

## Move System

- Max move ID: Vanilla `NUM_ATTACKS`
- Reserved move IDs: Vanilla unused move/animation IDs only; final policy TBD
- Move data fields: Vanilla move table fields: animation, effect, power, type, accuracy, PP, effect chance
- Move category storage: Not implemented
- Animation policy: Reuse existing animations unless a new move requires a documented custom animation.
- New move effect policy: TBD

## Pokemon Data

- Max species: Vanilla one-byte species ID range
- Species ID policy: Keep 251-species compatibility for engine v1.0; custom Pokemon should replace existing species unless a later plan explicitly expands species IDs.
- Base data structure: Vanilla pokecrystal base data structure
- TM/HM compatibility capacity: `NUM_TM_HM_TUTOR` packed flag array in base data
- Custom Pokemon constraints: TBD after engine feature freeze

## Items / TMs / HMs

- TM reuse policy: Vanilla single-use TMs
- HM policy: Vanilla HMs
- TM/HM pocket behavior: Vanilla TM/HM pocket
- Duplicate acquisition policy: Vanilla behavior

## Quality Of Life Features

- Implemented: None in this branch yet
- Deferred: reusable TMs, TM/HM move names, Repel reuse, Running Shoes, move reminder/relearner

## Save Compatibility

- SRAM/WRAM changes: None in this branch yet
- Migration policy: TBD
- Breaking changes: None known in this branch yet

## Testing Matrix

- Required build commands: `make`
- Clean build command: `make clean` followed by `make`
- Required smoke tests: boot ROM, start/load game, wild battle, trainer battle, save/load
- Feature regression checklist: TBD per feature branch before implementation

## Attribution

- Upstream references: pret/pokecrystal repository and wiki
- Tutorials consulted during planning: Physical/Special split, Add a new type, Add a new move, Add a new TM/HM, Infinitely reusable TMs, Show TM/HM move names, Automatically reuse Repel
- Code copied vs reimplemented: No feature implementation copied in this branch
- Licence notes: pret/pokecrystal and several reference hacks do not expose a GitHub-detected licence; reuse decisions should be documented before importing nontrivial external code.
