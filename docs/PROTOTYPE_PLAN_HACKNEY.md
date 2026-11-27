# First Prototype Plan — Hackney / Tower Hamlets

**Engine target:** Unreal Engine 5.8  
**Geospatial layer:** Cesium for Unreal  
**Working location:** Victoria Park / Bethnal Green / Regent's Canal, on the Hackney–Tower Hamlets side of East London  
**Initial scope:** one compact neighbourhood, not both boroughs  
**Status:** proposal for founder approval; exact playable boundary still to be selected after the first Cesium inspection

## 1. Why this location

The Victoria Park–Bethnal Green–Regent's Canal area offers a useful mix for the first Living World experiment:

- residential streets and housing;
- a large public green space;
- canal-side pedestrian routes;
- shops, cafés and everyday local destinations;
- roads, junctions and public transport context;
- a mixture of urban forms and building heights.

This gives us enough variety to test ordinary daily life without requiring a large world.

## 2. Recommended initial boundary

Start with a compact test window of approximately 500–800 metres across, anchored around the south-western edge of Victoria Park and nearby Bethnal Green / canal-side streets. Treat this as a visualisation and performance test boundary, not a final game-world border.

The exact rectangle should be selected in the editor after checking:
- how well the available Cesium imagery and building data cover the area;
- whether the chosen streets and park paths are represented clearly enough;
- whether there are suitable public-facing landmarks for navigation;
- streaming quality, draw calls, memory use and frame rate.

Do not attempt to make all of Hackney and Tower Hamlets playable in this first milestone.

## 3. First prototype goals

### Milestone A — Geospatial scene
- Create a clean Unreal Engine 5.8 project.
- Install a Cesium for Unreal release explicitly supporting UE 5.8.
- Add Cesium World Terrain and an appropriate permitted imagery/building source.
- Set the CesiumGeoreference origin near the selected neighbourhood.
- Inspect ground-level appearance and data coverage.
- Save a repeatable test level and document plugin/data versions.

**Acceptance:** the selected neighbourhood loads consistently in-editor, and the team can identify what is and is not represented by the chosen datasets.

### Milestone B — Player movement
- Add a third-person character and camera.
- Establish a safe starting point on a known street or open space.
- Test walking, turning, camera collision and ground contact.
- Check collision behaviour against streamed geometry.
- Test entering/exiting Play-in-Editor and Standalone modes.

**Acceptance:** the character can walk around a small test route without falling through the ground or becoming detached from the geospatial scene.

### Milestone C — Local environment
- Add local time and a controllable sun/lighting cycle.
- Add a weather abstraction with a manual test mode first.
- Connect an external weather source only after the data model and fallback path work.
- Label data as observation, forecast, simulated or developer override.
- Ensure the scene remains usable when the network is unavailable.

**Acceptance:** changing time and test weather produces a predictable visual response, with no dependency on a live API to launch the prototype.

### Milestone D — First signs of life
Only after the geospatial and player foundations are stable:
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

- **Geospatial:** Cesium georeference, tilesets, anchors and location utilities.
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

1. Confirm UE 5.8 installation and project location.
2. Confirm Cesium for Unreal plugin is installed and record its exact version.
3. Create a blank third-person project named `LivingWorld` (or agreed project name).
4. Enable Cesium and restart the editor.
5. Create an empty level and add Cesium geospatial actors using the current Quickstart.
6. Fly to the Victoria Park / Bethnal Green candidate area.
7. Inspect terrain, imagery and building coverage from several heights.
8. Save screenshots and record performance observations.
9. Decide the exact 500–800m test boundary.
10. Only then add the playable character.

## 8. Definition of done for the first demonstrator

The first demonstrator is complete when:
- UE 5.8 opens the project without errors;
- Cesium loads the chosen neighbourhood;
- the scene can be entered repeatedly in Play mode;
- the player can walk a short route;
- the project has a documented data/attribution record;
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

- Exact starting boundary within the Victoria Park / Bethnal Green / canal-side area.
- Whether the first build uses only Cesium-provided data or supplements it with separately licensed local datasets.
- Target hardware and minimum acceptable frame rate.
- Whether the first demo is editor-only or a packaged Windows build.
- Whether Git LFS or Perforce will be used for the Unreal project assets.
