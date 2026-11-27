# Existing Project Status — Walsall Game 5.8 / Living World

**Purpose:** record the technical starting point for Living World, based on the project brief supplied by the founder.  
**Engine/project:** Walsall Game 5.8 (Unreal Engine 5.8)  
**Future prototype location:** Hackney, London  
**Status source:** founder-provided `Living_World_Project_Brief.md`; this document records the reported status and does not independently verify the local build.

## Project direction

Living World will continue from the existing Walsall Game 5.8 project. The project is not being restarted from a blank Unreal template. Walsall is the current technical/code foundation; Hackney will be the selected location for the next prototype environment.

The supplied brief describes the goal as procedural city generation using OpenStreetMap (OSM) data. The next location task is to configure the existing data/generation pipeline for a compact Hackney area and validate the output, while preserving the known-good Walsall setup.

## Reported completed work

The founder's project brief reports:

- Build compiles successfully.
- Intersection culling fix: kerbs no longer overlap at three-or-more-way intersections.
- Previous code fixes preserved.
- `InteractionComponent::GetCurrentInteractable()` returns `AActor*`.
- Procedural house generator re-enabled.
- `BP_DynamicBuildingSpawner` compiled and saved.
- Procedural terrain heightfield generated from road centreline Z values.
- Sidewalk and kerb visibility improvements, including terrain line traces for `PaveLOuter` and `PaveROuter`, and double-sided sidewalk surfaces/kerb riser faces.
- Save-game and weather/HTTP subsystem fixes listed below.

### Fixes recorded in the supplied brief

- `WALLSALLGAME_API` changed to `WALSALL_GAME_API`.
- Corrected GameInstanceSubsystem include path.
- Removed inappropriate API macro from `InteractionComponent.h`.
- Removed Tick override from `WeatherSubsystem.h`.
- Added `FTickableGameObject` to `WorldDataSubsystem.h` and `WeatherPollingSubsystem.h`.
- Fixed `OnProcessRequestComplete()`, `EHttpResponseCodes::Type` cast and missing braces in `OpenMeteoWeatherFetcher.cpp`.
- Changed `WeatherPollingSubsystem.cpp` from `BindLambda` to `AddDynamic` UFUNCTION handlers.
- Fixed `TransformUnrealPositionToLongitudeLatitudeHeight` in `CesiumGeoHelper.cpp`.
- Fixed `DeleteSaveGame` in `LivingWorldSaveSubsystem.cpp`.
- Set `GameInstanceClass=/Script/Walsall_Game.Walsall_GameInstance` in `DefaultEngine.ini`.

## Pending work recorded in the supplied brief

- Enable/configure wall textures (Content Browser search required).
- Enable/configure roof materials (Content Browser search required).
- Configure door/window placeholders (Content Browser search required).
- Complete house entry/interaction testing in Play-in-Editor (PIE).
- Hook up `ApplyWeatherToRoadParameters` in `BP_DynamicBuildingSpawner`.
- Implement the blend zone and Cesium hiding/overlap handling.

The brief describes offline capability as partial: the procedural heightfield is cached, while Cesium requires an online connection.

## Existing geospatial roadmap

The supplied project brief records this sequence:

1. **Procedural terrain heightfield from road centreline Z values — complete.**
2. **Blend zone + Cesium hiding — pending.** Smooth the transition between procedural terrain and Cesium and handle overlapping surfaces.
3. **Full Cesium replacement — optional future phase.** The brief describes this as a later option, not a required immediate step.

Living World should preserve the current procedural terrain foundation while the blend-zone approach is developed and tested. Full Cesium replacement should remain an explicit future decision, not be assumed as the next task.

## Hackney location migration — next work

1. Retain the existing Walsall project and a known-good build/map as a regression reference.
2. Select a compact Hackney test boundary.
3. Obtain and inspect OSM data for that boundary.
4. Check road centreline/elevation inputs, junction types, building footprints and relevant OSM tags.
5. Run the existing procedural pipeline in a separate Hackney test map/level.
6. Compare generated roads, kerbs, sidewalks, terrain and buildings with the source data.
7. Record data gaps and generator assumptions before changing core algorithms.
8. Test player movement and house entry/interaction in the Hackney map.
9. Continue the procedural/Cesium blend-zone work separately, validating coordinate alignment, elevation, surface overlap and performance.

The exact Hackney boundary, OSM extract/provider and any supplementary datasets still need to be selected and documented.

## Camera design carried into the prototype

The agreed Living World camera requirements are:

- First-person is the default in-game view.
- A front-facing external view (the project's informal "second-person" option) is available.
- Third-person follow view is available.
- Top-down view supports both world observation and future world-management interactions.
- Camera switching is available through both keyboard/controller shortcuts and an on-screen selection menu.
- All views use the same player character and preserve player position and gameplay state.

See [Camera System Design](CAMERA_SYSTEM.md).

## Important distinction

This document records what the founder's supplied project brief says is complete or pending. It does not mean the assistant has opened the local Unreal project, inspected source files, run a build or verified the current editor state. Any change to the local project should be made against the actual project files and tested in Unreal Engine.
