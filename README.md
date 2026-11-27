# Living World

**An evolving, real-world-inspired simulation built with Unreal Engine 5.8 and Cesium for Unreal.**

Living World explores a persistent world in which people, places, weather and everyday events continue to exist independently of the player. The player inhabits the world as an ordinary person; they are part of it, not the centre of the universe.

## The vision

The project combines three layers:

1. **Real-world foundation** — geospatial context, terrain, imagery, buildings and carefully selected live information such as local time and weather.
2. **Simulation** — fictional residents with routines, needs, relationships, memories and reactions to their surroundings.
3. **Player experience** — exploration, work, social activity and everyday choices in a world that continues around the player.

## First playable target

Prove the idea in one small town or neighbourhood before attempting a global simulation.

The initial prototype will explore:
- one Cesium-backed location;
- third-person movement;
- local time and a limited weather system;
- a small group of autonomous NPCs;
- a few meaningful interactions and one simple activity loop;
- basic persistence.

This is an early-stage plan, not a claim that these systems are implemented.

## Technology direction

- Unreal Engine 5.8
- Cesium for Unreal
- C++ for reusable foundations and performance-sensitive systems
- Blueprints for rapid gameplay and content iteration
- A controlled data layer for external APIs, caching, validation and fallback behaviour
- GitHub for public planning and selected project materials

## Public development, restricted reuse

Living World is developed in public, but this repository is **not currently open source**. Unless a file has its own explicit licence or written permission notice, all rights are reserved. Public visibility does not grant permission to reuse, copy, modify, redistribute or commercially exploit project materials.

Selected code and assets will remain private in separate repositories or storage. Third-party software, datasets, imagery, plugins and assets remain subject to their own licences and terms. See [LICENSE](LICENSE) and [LICENSING.md](LICENSING.md).

## Get involved

All experience levels are welcome. You can contribute through research, design, code, art, testing, documentation and constructive feedback.

1. Read [CONTRIBUTING.md](CONTRIBUTING.md).
2. Browse [ROADMAP.md](ROADMAP.md).
3. Look for beginner-friendly or help-wanted issues.
4. Discuss substantial work before starting.

The Founder and Creative Director retains final responsibility for creative direction, scope and project releases.

## Project references

- [Project overview](docs/PROJECT_OVERVIEW.md)
- [Development roadmap](ROADMAP.md)
- [Discord structure proposal](docs/DISCORD_STRUCTURE.md)
- [Licensing policy](LICENSING.md)
- [Fluid Planet case study](https://cesium.com/blog/2023/08/31/fluid-planet-immerses-young-students-in-the-outdoors/)
- [Fluid Planet video](https://vimeo.com/857165355)
- [HOK Centre Block Digital Twin video](https://www.youtube.com/watch?v=YxnaFAOJdU8)
- [Cesium for Unreal documentation](https://cesium.com/learn/unreal/)

The roadmap describes priorities, not guaranteed delivery dates. We will adjust it as prototypes teach us what is practical.
