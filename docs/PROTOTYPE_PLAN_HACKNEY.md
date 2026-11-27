# Living World Prototype Plan — Hackney

**Engine target:** Unreal Engine 5.8  
**Technical foundation:** existing Walsall Game 5.8 codebase, to be renamed/rebranded as the LivingWorld Unreal project  
**World generation:** existing OpenStreetMap-driven procedural city systems and procedural terrain heightfield  
**Geospatial integration:** retain the current procedural foundation; develop the planned Cesium blend zone and evaluate fuller Cesium replacement as a later option  
**Working location:** Hackney, London — exact compact test boundary to be selected  
**Status:** existing project is reported ready and compiling; project rename and Hackney-specific data setup/testing remain to be done

## 1. Why this location

The Hackney area will be the first Living World test location. Victoria Park / Bethnal Green / Regent's Canal remains a suggested candidate area, subject to the founder's final boundary choice. It offers a useful mix for the first experiment:

- residential streets and housing;
- a large public green space;
- canal-side pedestrian routes;
- shops, cafés and everyday local destinations;
- roads, junctions and public transport context;
- a mixture of urban forms and building heights.

This gives us enough variety to test ordinary daily life without requiring a large world.

## 2. Recommended initial boundary

Start with a compact test window of approximately 500–800 metres across. Victoria Park / Bethnal Green / Regent's Canal is a candidate area only; the founder will select the exact Hackney boundary.

Choose the rectangle after checking:
- OSM road, junction, building-footprint and relevant tag coverage;
- the quality of the available road-centreline elevation inputs;
- how the existing procedural generator handles the selected street layout;
- whether any Cesium terrain/imagery/building layers align with the procedural result;
- generated geometry quality, memory use and frame rate.

Do not attempt to make all of Hackney playable in this first milestone.

## 3. First prototype goals

### Milestone A — Move the existing procedural city to Hackney
The existing Walsall Game 5.8 project is the technical base and is to be renamed/rebranded as LivingWorld. The uploaded project brief reports that the C++ build compiles successfully and that the procedural terrain heightfield and intersection culling fixes are complete.

- Preserve the existing OSM-driven procedural roads/buildings, terrain heightfield, building spawner and completed fixes.
- Configure or import the OSM source data for the selected Hackney test boundary.
- Verify road, junction, building-footprint and elevation coverage before changing generator logic.
- Run the procedural generation in a separate Hackney test level/map so the existing pre-migration setup can be retained as a known-good reference.
- Record any location-specific assumptions, missing OSM tags, unsupported geometry and data-cleaning requirements.
- Keep Cesium integration as a distinct layer/phase; do not remove or replace the procedural heightfield as part of the location move.

**Acceptance:** the existing procedural pipeline can generate a repeatable Hackney test area without regressions to the known-good pre-rename build.

### Milestone B — Player movement and multi-perspective camera
- Add one player character with **first-person as the default in-game view**.
- Provide four switchable camera perspectives:
  1. **First-person:** primary immersive play view for walking, looking and interacting.
  2. **Front-facing external view ("second-person" option):** camera faces the player character, useful for seeing expressions and character presentation. This is a project-defined view, not a standard camera category.
  3. **Third-person:** camera follows behind the character at an adjustable distance.
  4. **Top-down:** overhead view for both observing the simulated neighbourhood and, in later milestones, interacting with world-management tools.
- Support camera switching through **both** keyboard/controller shortcuts and an on-screen camera selection menu.
- Keep the character, movement, position, inventory and interaction state continuous when changing views; switching cameras must not possess a different pawn.
- Add camera collision/obstruction handling, sensible zoom limits and smooth transitions where practical.
- Establish a safe starting point on a known street or open space.
- Test walking, turning, camera collision and ground contact in each relevant perspective.
- Check collision behaviour against streamed geometry.
- Test entering/exiting Play-in-Editor and Standalone modes.

**Acceptance:** first-person is the default; all four perspectives can be selected using both input methods; changing perspective does not reset or alter player state; the character can walk around a small test route without falling through the ground or becoming detached from the geospatial scene.

### Camera implementation direction
Keep camera switching inside the player-character/camera system rather than creating separate player pawns. A possible Blueprint setup is `BP_LW_PlayerCharacter` plus a camera manager/component responsible for mode selection, view targets, transitions, collision and zoom. Exact component layout can be decided during implementation.

### Milestone C — Cesium blend zone and geospatial integration
This follows the existing project roadmap:
- **Phase 1 — Procedural terrain heightfield:** reported complete in the project brief.
- **Phase 2 — Blend zone + Cesium hiding:** pending; develop a controlled transition between procedural terrain and Cesium content, including rules for hiding or blending overlapping surfaces.
- **Phase 3 — Full Cesium replacement:** optional future evaluation, not a prerequisite for the Hackney prototype.

Before implementation, verify coordinate alignment, elevation consistency, surface overlap, visual seams, collision and streaming performance. Keep the procedural solution available as a fallback.

**Acceptance:** the selected Hackney test area has a documented and repeatable procedural/Cesium relationship, or a documented decision to defer Cesium blending.

### Milestone D — Local environment
- Add local time and a controllable sun/lighting cycle.
- Add a weather abstraction with a manual test mode first.
- Connect an external weather source only after the data model and fallback path work.
- Label data as observation, forecast, simulated or developer override.
- Ensure the scene remains usable when the network is unavailable.

**Acceptance:** changing time and test weather produces a predictable visual response, with no dependency on a live API to launch the prototype.

### Milestone E — First signs of life
Only after the Hackney procedural environment and player foundations are stable:
- Add a small number of placeholder residents.
- Give each a simple schedule: home, walk, destination, return.
- Use a small number of hand-authored destinations.
- Add one basic interaction, such as greeting a resident or entering a simple shop interaction.
- Profile NPC navigation and tick costs before increasing population.

**Acceptance:** residents follow simple routines without being directed by the player.

## 4. Unreal project structure proposal

Keep the project organised by responsibility. Names can be adjusted to match the final project naming convention.

```
LivingWorld/
  Config/
  Content/
    Core/
    Geospatial/
    Environment/
    Characters/
    NPC/
    Gameplay/
    UI/
    Maps/
      Prototype_Hackney/
    Developer/
  Plugins/
  Source/
    LivingWorld/
      Core/
      Geospatial/
      Environment/
      Data/
      NPC/
      Gameplay/
  Docs/
```

Do not commit generated folders such as `Binaries`, `Intermediate`, `Saved` or `DerivedDataCache`. Keep large Unreal binary assets out of Git unless Git LFS has been configured and the team has agreed how to use it.

## 5. Suggested technical boundaries

Avoid coupling gameplay directly to a particular external provider.

- **Procedural world generation:** OSM ingestion/normalisation, road and junction generation, procedural buildings and terrain heightfield.
- **Geospatial integration:** coordinate transforms and, when enabled, Cesium georeference, tilesets, anchors and blend/hide logic.
- **World data:** normalised internal types for location, time and weather.
- **Data services:** provider requests, caching, validation, rate limiting and offline fallback.
- **Environment:** time-of-day, lighting and weather presentation.
- **Player:** movement, camera and interaction.
- **NPC simulation:** schedule, current activity, destination and simple needs.
- **Persistence:** initially save only a small amount of player and world state.

Use Blueprints for fast visual iteration and C++ where reusable foundations, data interfaces or performance justify it. Do not introduce a large AI framework before the first few routines prove what is needed.

## 6. Data and licensing cautions

- Cesium terrain, imagery, OSM buildings, Google Photorealistic 3D Tiles and other sources have different terms, attribution rules and availability.
- Do not assume that streamed data can be downloaded, baked into the game, redistributed or committed to GitHub.
- Keep API tokens out of source control and out of distributed clients where they provide privileged access.
- Record the provider, asset ID, terms, attribution and date checked for each dataset.
- Use synthetic placeholder assets where redistribution rights are unclear.
- Keep this public plan free of secrets, private assets and proprietary implementation details.

## 7. Suggested first sprint

1. Rename the existing Walsall Game 5.8 project to the LivingWorld project in place; do not create a replacement project. Preserve a backup and a known-good commit before renaming.
2. Confirm the current build still compiles and preserve a known-good backup/commit.
3. Choose the exact compact Hackney test boundary.
4. Obtain and inspect OSM data for that boundary; confirm the required roads, junctions, building footprints and elevation inputs.
5. Configure the existing procedural generator for the Hackney data in a separate test map/level.
6. Compare the generated result with the source data and record missing/unsupported features.
7. Test the existing player and house interaction flow in the Hackney map.
8. Continue the pending blend-zone + Cesium-hiding work as a separate phase, after documenting coordinate and elevation alignment.
9. Retain full Cesium replacement as optional, not an assumed requirement.
10. Implement/verify the agreed four-perspective camera system: first-person default, front-facing, third-person and top-down, with both shortcuts and on-screen selection.

## 8. Definition of done for the first demonstrator

The first demonstrator is complete when:
- UE 5.8 opens the project without errors;
- the existing OSM procedural pipeline generates the chosen Hackney neighbourhood;
- the scene can be entered repeatedly in Play mode;
- the player can walk a short route in first-person and switch between all four planned camera perspectives using both shortcut input and the on-screen menu;
- the project has a documented OSM and any Cesium data/attribution record;
- the team can reproduce the setup from written instructions;
- known limitations and performance observations are recorded.

## 9. Official starting references

- Cesium for Unreal Quickstart: https://cesium.com/learn/unreal/unreal-quickstart/
- Cesium for Unreal documentation: https://cesium.com/learn/unreal/
- Cesium for Unreal releases (check the UE 5.8 package): https://github.com/CesiumGS/cesium-unreal/releases
- Placing objects on the globe: https://cesium.com/learn/unreal/unreal-placing-objects/
- Georeferenced sublevels: https://cesium.com/learn/unreal/unreal-sublevels/
- Cesium content usage and attribution: https://cesium.com/learn/ion/content-usage-and-attribution-guide/

## 10. Decisions still needed

- Exact starting boundary within Hackney (Victoria Park / Bethnal Green / Regent's Canal remains a candidate, not a final selection).
- Which OSM extract/provider and any supplementary datasets will be used, including their licences and attribution requirements.
- Target hardware and minimum acceptable frame rate.
- Exact shortcut mapping and controller bindings for the four camera modes.
- Whether top-down world-management interactions are enabled in the first demonstrator or remain a later extension.
- Whether/when the Cesium blend-zone phase should be included in the first playable Hackney build.
- Whether the first demo is editor-only or a packaged Windows build.
- Whether Git LFS or Perforce will be used for the Unreal project assets.
