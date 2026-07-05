# Crystal Modern Move Bible

## Purpose

The Move Bible defines how moves should be designed, selected, implemented, and
balanced for Crystal Modern. It is a design document, not a feature request list.
Every new move, changed move, TM, HM, animation, and move effect should be judged
against this document before implementation.

The goal is a curated Gen II-plus move system: readable like Pokemon Crystal,
balanced around the Physical/Special split and modern type chart, and small
enough that every move has a reason to exist.

## Current Move System Status

- Physical/Special/Status categories are implemented per move.
- Move category is stored in the high bits of `MOVE_TYPE`.
- Raw move type lookups must mask `MOVE_TYPE` with `TYPE_MASK`.
- Fairy type is implemented as a raw type below `TYPE_MASK`.
- The modern type chart is implemented, including Steel neutrality to Ghost and
  Dark.
- Existing Fairy status retcons are `SWEET_KISS`, `CHARM`, and `MOONLIGHT`.
- Phase A Fairy damaging moves are implemented by ID replacement:
  `DISARMING_VOICE`, `PLAY_ROUGH`, `MOONBLAST`, and `DRAINING_KISS`.
- Batch B core coverage moves are implemented by ID replacement:
  `SHADOW_CLAW`, `POISON_JAB`, `X_SCISSOR`, `FLASH_CANNON`, `POWER_GEM`,
  `AIR_SLASH`, and `SEED_BOMB`.
- Batch C polish coverage moves are implemented by ID replacement:
  `DRAGON_PULSE`, `DRAGON_CLAW`, and `BUG_BITE`.
- Hidden Power remains unchanged and must not become Fairy.
- The move table still uses the vanilla move ID range and vanilla move data
  structure.
- Reusable TMs, expanded move IDs, and additional move batches are not
  implemented yet.

## Category Rules

Every move must explicitly be one of three categories:

- Physical: damage uses Attack and Defense.
- Special: damage uses Special Attack and Special Defense.
- Status: the move does not deal direct category-based damage.

Category should follow official Gen IV+ behavior unless Crystal Modern has a
documented design reason to deviate. Deviations must be intentional, reviewed,
and recorded near the move decision.

Type and category are separate decisions. A move being Fire, Electric, Ghost,
Dark, or Fairy does not imply its category.

## Modern Move Eligibility

A modern move may be considered when it:

- Solves a real gameplay or balance need.
- Has an effect a player can understand from Crystal-style battle text.
- Fits the Game Boy Color battle pace and UI.
- Can reuse or lightly adapt existing animation language.
- Does not require absent systems such as Abilities, Terrain, forms, or complex
  hidden state.
- Improves species identity, type balance, TM design, or trainer variety.

A move should not be added only because it exists in a later generation.

## Allowed Generations

Moves from any later generation may be considered. Eligibility is based on fit,
clarity, and engine cost rather than generation of origin.

Preferred sources:

- Simple later-generation staples that fill category gaps.
- Moves that give under-supported types reliable STAB.
- Moves that are easy to communicate with existing Crystal battle text.
- Moves that can be represented by existing or modestly adjusted animations.

## Excluded Move Types

The following move families are excluded by default:

- Ability-dependent moves.
- Terrain-dependent moves.
- Dynamax, Z-Move, Mega Evolution, or Terastallization moves.
- Raid, doubles-only, or battle-format-specific moves.
- Moves that require extensive form logic.
- Moves that require large new battle state or new UI panels.
- Moves whose value depends on obscure exceptions the player cannot inspect.
- Large one-off mechanics that exist only for a single move.

Exceptions require design review before implementation.

## Move Effect Complexity Policy

Prefer clear effects already native to Crystal:

- Direct damage.
- Status conditions.
- Stat changes.
- Recovery.
- Recoil.
- Draining.
- Priority.
- Charging or recharge turns.
- Multi-hit.
- Simple secondary effects.
- Weather interaction, used sparingly.

Avoid effects that create long chains of conditionals, persistent hidden state,
or rules that cannot be explained in one short sentence.

When a move needs a new effect, first ask whether an existing effect can express
the same role cleanly. If not, implement the smallest general-purpose effect
that can support multiple moves.

## Animation Reuse Policy

Crystal Modern should look like Pokemon Crystal. Reuse existing animations where
they communicate the move clearly.

Animation priority:

1. Reuse an existing animation unchanged.
2. Recombine existing visual elements.
3. Lightly edit an existing animation.
4. Create a new animation only for important moves, signature moments, or cases
   where reuse would mislead the player.

Do not let animation ambition drive move selection. A good move with a simple
clear animation is better than a flashy move that strains the engine.

## Signature Move Policy

Signature moves are allowed, but they must justify their slot.

A signature move should:

- Reinforce a Pokemon's role or identity.
- Be understandable immediately.
- Avoid bespoke rules unless the Pokemon is built around them.
- Be useful enough to matter, but not so efficient that it invalidates normal
  move design.

If a signature move would improve the wider ecosystem, consider whether it should
become a limited-distribution regular move instead.

## STAB And Coverage Philosophy

Every battle-ready Pokemon should have reasonable access to STAB. Lack of STAB
may be used temporarily for progression, but should not be the default state of
finished Pokemon.

Coverage should create team-building choices, not erase weaknesses. Strong
coverage should be distributed deliberately, especially on fast or high-offense
Pokemon.

Good move pools should:

- Support the Pokemon's intended role.
- Give the player meaningful choices between power, accuracy, utility, and PP.
- Leave counterplay intact.
- Avoid giving every attacker the same best coverage package.

## Fairy Move Needs

Fairy now has a small Phase A damaging package: `DISARMING_VOICE`,
`DRAINING_KISS`, `MOONBLAST`, and `PLAY_ROUGH`. These moves exist to make Fairy
usable without broad TM distribution or a large modern move import.

Remaining Fairy move needs:

- Fairy TM support only after the final Fairy roster and TM philosophy are
  reviewed.
- Final level-up distribution after the custom Pokedex identifies which Pokemon
  are meant to use Fairy STAB.
- `DRAINING_KISS` currently uses Crystal's existing 50 percent drain behavior.
  Review later whether it should receive a custom 75 percent drain effect.

Do not add broad Fairy coverage until the custom Pokedex identifies which
Pokemon are meant to use it.

## Physical Electric, Ghost, And Dark Needs

The Physical/Special split creates useful new design space, but some types need
physical support to avoid awkward move pools.

Priority gaps to review later:

- Physical Electric: needed if Crystal Modern includes physical Electric
  attackers. Avoid over-distributing strong Electric coverage.
- Physical Ghost: `SHADOW_CLAW` and `SHADOW_BALL` now serve this role.
- Physical Dark: needed for Dark attackers. Bite and Crunch currently serve this
  role, with Crunch corrected to Physical.

Add only enough moves to support the Pokedex. Do not build a full modern
competitive move catalog.

## TM Move Philosophy

TMs should eventually be reusable, so TM selection must assume permanent
acquisition rather than single-use scarcity.

TM moves should:

- Encourage experimentation.
- Support multiple Pokemon without erasing species identity.
- Provide useful but controlled coverage.
- Include role-defining utility, not only attacks.
- Be placed as meaningful exploration and progression rewards.

TM compatibility should be curated per species. A Pokemon should receive a TM
because it supports its role, not because the move is broadly convenient.

## HM Move Philosophy

HMs are part of Crystal's exploration identity, but they should not punish team
building.

Preferred HM direction:

- Keep field progression readable and world-based.
- Avoid forcing weak utility moves onto long-term party members.
- Consider HM-like moves, key-item progression, or improved HM move quality
  during a dedicated HM/TM milestone.

Do not redesign HMs incidentally while adding battle moves.

## Move ID Policy

For now, Crystal Modern uses the vanilla one-byte move ID range and vanilla move
table structure.

Before adding moves, the project must decide whether to:

- Replace weak or obsolete vanilla moves inside the existing move ID range.
- Reuse unused vanilla move IDs where safe.
- Expand move capacity as a dedicated technical milestone.

Move ID expansion must not be bundled into ordinary move additions.

## Reserved Move IDs

Reserved move IDs are TBD pending a formal move-capacity audit.

Until that audit is complete:

- Treat all vanilla move IDs as occupied or historically meaningful.
- Treat unused move and animation slots as reserved, not free.
- Do not assign new moves to unused IDs without documenting the chosen ID, old
  purpose, animation impact, TM impact, trainer impact, and save/link risk.

## Replacing Weak Or Obsolete Gen II Moves

A weak or obsolete Gen II move may be replaced only when most of the following
are true:

- The move has little meaningful use in Crystal Modern's design.
- Its removal does not damage early-game teaching, flavor, or encounter identity.
- A replacement fills a more important role.
- Existing learnsets, trainer movesets, animations, TMs, and documentation can be
  updated coherently.
- The replacement still feels plausible in a Crystal-style game.

Do not replace a move merely because it is low power. Weak moves can be useful
for early-game pacing, capture setup, progression, or flavor.

## Future Moves To Consider Later

This is a review queue, not an approval list. Each move still needs a separate
implementation plan.

- Physical Electric: Spark, Thunder Fang, Wild Charge, or Nuzzle if a status
  utility role is needed.
- Physical Dark: Knock Off, Assurance, Sucker Punch, or Night Slash, with strong
  caution around effects that require item loss, prediction, or complex AI.
- Dragon coverage: `DRAGON_PULSE` and `DRAGON_CLAW` are implemented as the
  simple special and physical Dragon standards.
- Clean utility: U-turn, Will-O-Wisp, Taunt, or Helping Hand only if the battle
  format and AI can support them gracefully.
- Type balance candidates: Energy Ball or other simple coverage moves only if
  specific custom Pokemon need them. `POWER_GEM`, `X_SCISSOR`,
  `FLASH_CANNON`, and `AIR_SLASH` are already implemented.

Future additions should remain small, targeted, and justified by the custom
Pokedex, TM plan, or trainer design. Do not add another batch until the current
move ecosystem has been manually tested in emulator.

## Large Batch Warning

Do not add large batches of moves without review.

Large move additions create cascading risk across animations, move effects,
trainer movesets, AI scoring, TMs, learnsets, move descriptions, save data,
documentation, and balance. Crystal Modern should add moves in small batches,
with a clear reason, a test checklist, and a build after each batch.

Every move added should earn its place.
