# Copilot Instructions for BAS-N_Solver_Mod

This repository contains a mod for **Blade & Sorcery: Nomad** (Nexus Mods template-based) that adds Solver-themed spells and skills using the **ThunderRoad game engine**.

## Thematic Context: Murder Drones Solver

The **Solver** is a reality-altering "dev tool" from the YouTube series *Murder Drones* (Glitch Productions), used by characters Uzi, Doll, and Cyn. This mod recreates the Solver as a playable magic system in Blade & Sorcery: Nomad.

### Aesthetic & Design Direction
- **Visual theme:** Dark, glitchy, geometric (hexagons, angular patterns, digital artifacts)
- **Color palette:** Deep purples, blacks, with neon accents (cyan/magenta)
- **Feel:** Reality-breaking, "dev tool" manipulation, synthetic/digital rather than organic magic
- **Audio:** Synthetic, digital, glitchy—avoid traditional fantasy magic sounds

### Current Implementation Goals (from README)
- Replace generic magic colors with Solver's dark/purple palette
- Change spell shapes to geometric/hexagonal forms (not spheres)
- Add a visible Solver glyph/symbol on the player's hand when casting
- Create custom audio with a digital, glitchy aesthetic
- Add visual effects that convey reality distortion/corruption

## Repository Structure

- **`manifest.json`** - Mod metadata (name, author, version, game version)
- **`Spells/`** - Spell definitions (Gravity, Telekinesis, etc.)
  - Each spell is a JSON file with `$type` set to a ThunderRoad spell class (e.g., `SpellCastGravity`)
- **`Skills/`** - Skill definitions (BoostJump, FeatherFall, etc.)
  - Each skill is a JSON file with `$type` set to a ThunderRoad skill class (e.g., `SkillBoostJump`)
- **`Effects/`** - Visual and audio effect definitions
  - Each effect contains modules for particles, audio, haptics using ThunderRoad's `EffectData` type
- **`Statuss/`** - Status effect definitions (Floating, PlayerHover, etc.)
- **`Items/`** - Item definitions (if used by spells/skills)

## JSON Configuration Format & Conventions

### Common Structure
All definitions follow the ThunderRoad JSON schema:
```json
{
  "$type": "ThunderRoad.ClassName, ThunderRoad",
  "id": "UniqueIdentifier",
  "sensitiveContent": "None",
  "sensitiveFilterBehaviour": "Discard",
  "version": 0,
  // spell/skill/effect-specific properties
}
```

### Key Patterns
- **IDs must be unique** across their category (Spells, Skills, Effects)
- **Effect references** use the effect's `id` (not file name). Example: spell references `"chargeEffectId": "SpellGravityChargeNE"`
- **Audio addresses** use hierarchical paths like `"Bas.AudioGroup.Spell.Gravity.Push"`
- **Animation curves** are stored as `UnityEngine.AnimationCurve` with keyframes for smooth transitions
- **Numeric parameters** like `pushLevel`, `chargeSpeed`, `playerBoostForce` control spell/skill behavior

### Spell Properties (SpellCastGravity Example)
- `halfSphereRadius` - Area of effect radius
- `pushLevel` - X and Y push force values (affects throw strength)
- `pushMaxForce` - Maximum force cap
- `chargeSpeed` - How fast spell charges when held
- `minChargeToPushCreature` - Minimum charge to affect creatures
- Effect IDs: `chargeEffectId`, `fingerEffectId`, `throwEffectId`, `readyEffectId`, `pushEffectId`

### Effect Module Types
- `EffectModuleParticle` - Visual particles linked to effect intensity
- `EffectModuleAudio` - Audio playback with curves, haptic feedback, filtering

## Current State & Known Items

From README.md (TODO list):
- Change colors and gravity spell shape to solver-like things
- Adjust spell strength values
- Add custom sounds
- Add visual effects
- Add solver symbol on hand when in use

**Note:** This is a WIP (Work in Progress) mod - many features are still being implemented.

## When Modifying Files

- Always update the corresponding effect/spell/skill ID in referencing files
- Test audio address paths exist in the game's audio system
- Animation curve changes should preserve the keyframe structure
- The `version` field can be incremented when making significant changes
- Maintain consistent naming: Spell IDs use `Spell_`, Effect IDs use `Effect_`, etc.

## No Build/Test System

This is a configuration-only mod (JSON files). There are no build commands, tests, or linters. Changes are loaded directly by the game engine when the mod is installed.
