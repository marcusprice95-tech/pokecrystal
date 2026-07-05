# Crystal Modern Engine Manifest

## Base

- Upstream base commit: `06ec23cce` (`Fix some issues with C tools, and build them with -std=c17 (#1259)`)
- Engine branch: `engine-modernisation`
- Source branch point: `master` / `origin/master`
- Content branch separation: custom Pokemon content such as the Snom/Hoothoot changes currently belongs outside this engine branch.
- Save format version: TBD
- Link compatibility policy: TBD

## Battle Mechanics

- Physical/Special split: Implemented; move category is stored in the high bits of `MOVE_TYPE`
- Fairy type: Implemented as raw type ID after `DARK`; remains below `TYPE_MASK`
- Type chart: Modern type chart, including Fairy and modern Steel neutrality to Ghost/Dark
- Battle bug fixes applied: None in this branch yet
- Known battle limitations: Vanilla battle mechanics and known Crystal bugs still apply unless documented otherwise.

## Move System

- Design authority: See `MOVE_BIBLE.md`
- Max move ID: Vanilla `NUM_ATTACKS`
- Reserved move IDs: Vanilla unused move/animation IDs only; final policy TBD
- Move data fields: animation, effect, power, category-coded type, accuracy, PP, effect chance
- Move category storage: `MOVE_TYPE = category bits | raw type id`; use `TYPE_MASK` before raw type lookups
- Existing Fairy-type move retcons: `SWEET_KISS`, `CHARM`, `MOONLIGHT`
- Phase A Fairy move replacements: `BARRAGE` -> `DISARMING_VOICE`, `SHARPEN` -> `PLAY_ROUGH`, `KINESIS` -> `MOONBLAST`, `PSYWAVE` -> `DRAINING_KISS`
- Phase A new move effects: None; all four moves reuse existing effects
- Phase A known move behavior: `DRAINING_KISS` uses existing 50 percent drain behavior
- Batch B coverage move replacements: `COMET_PUNCH` -> `SHADOW_CLAW`, `SMOG` -> `POISON_JAB`, `TWINEEDLE` -> `X_SCISSOR`, `SPIKE_CANNON` -> `FLASH_CANNON`, `CLAMP` -> `POWER_GEM`, `RAZOR_WIND` -> `AIR_SLASH`, `PRESENT` -> `SEED_BOMB`
- Batch B new move effects: None; all seven moves reuse existing effects
- Batch B TM status: No TMs added; distribution is intentionally deferred to the custom Pokedex and TM passes
- Animation policy: Reuse existing animations unless a new move requires a documented custom animation.
- New move effect policy: TBD

## Pokemon Data

- Max species: Vanilla one-byte species ID range
- Species ID policy: Keep 251-species compatibility for engine v1.0; custom Pokemon should replace existing species unless a later plan explicitly expands species IDs.
- Base data structure: Vanilla pokecrystal base data structure
- Vanilla species Fairy retcons: Not applied yet; no existing species base types have been changed to Fairy in this branch
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
- Time Capsule/link compatibility: Out of scope for Crystal Modern engine features; no compatibility work was added for Fairy type.

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
