# Living World Camera System

**Status:** confirmed design direction for the first prototype  
**Default perspective:** first-person

## Goals

The player should experience Living World primarily from eye level, as an ordinary person inhabiting the simulation. Alternative perspectives should be available without breaking continuity or turning the player into a separate observer pawn.

## Camera modes

1. **First-person (default):** eye-level view for exploration, movement and interaction. This is the normal in-game perspective.
2. **Front-facing external view ("second-person" option):** a camera positioned in front of and looking towards the player character. This provides a view of the character's face and body. "Second-person" is the project's informal label for this option; it is not a universally standard camera-mode name.
3. **Third-person:** a trailing camera behind the character, with adjustable follow distance as appropriate.
4. **Top-down:** an overhead perspective. It must support both:
   - **World observation:** looking over streets, buildings and NPC activity.
   - **World management:** a foundation for future management or planning interactions. The first prototype may initially provide observation only while the interaction design is developed.

## Switching controls

Camera selection must be available through **both**:
- keyboard/controller shortcuts; and
- an on-screen camera selection menu.

Exact key and controller bindings are implementation decisions and should be documented once tested. The on-screen menu should make the current perspective clear and remain accessible without requiring a keyboard shortcut.

## Continuity requirements

All views use the same player character and the same underlying gameplay state. Switching camera perspective must not:
- move or respawn the player;
- change the selected pawn;
- reset movement or interaction state;
- change inventory or progression;
- grant the top-down camera control over the simulation simply by being selected.

Camera changes should be predictable and comfortable. Use collision/obstruction handling to reduce clipping through buildings and other geometry. Apply sensible zoom and rotation limits, especially in top-down mode. Smooth transitions are desirable where they do not interfere with control.

## Unreal implementation direction

A practical starting point is a single `BP_LW_PlayerCharacter` with a camera system/component that owns:
- the active camera mode;
- camera transforms and offsets for each mode;
- switching input and menu events;
- transition blending;
- collision/obstruction checks;
- zoom and rotation limits.

The exact implementation may use multiple camera components or a managed view target, but should avoid separate player pawns for each perspective. Keep camera selection separate from simulation authority and world-management permissions.

## Prototype acceptance criteria

- First-person is active when the prototype starts.
- The player can switch to all four camera perspectives.
- Both shortcut controls and the on-screen menu can change perspective.
- Switching perspective preserves player location and gameplay state.
- Top-down mode can be used to observe the neighbourhood and NPCs.
- Camera collision/obstruction behaviour is tested around buildings and street geometry.
- Any world-management interactions added later are explicit gameplay features, not an accidental side effect of camera selection.
