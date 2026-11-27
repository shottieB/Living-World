# LIVING WORLD

### Procedural real-world (re)generation. A living world simulation.

**Living World** is an ambitious open-world life simulation being developed with Unreal Engine 5.8, Cesium for Unreal, C++, Blueprints and custom procedural generation systems.

The idea is simple to describe, but ambitious to build:

**Use the real world as the foundation to generate our own environment — then bring that environment to life with a society that continues to evolve around the player.**

Living World brings together two essential parts:

- **Procedural world regeneration:** reconstructing real-world environments as custom Unreal Engine worlds, designed for visual quality, consistency, interaction and gameplay.
- **A living society:** simulating people, homes, businesses, jobs, relationships, routines and everyday activities so that the world feels inhabited rather than populated by background crowds.

The player is part of this world, not the centre of it.

---

## The core idea

### 1. Regenerate the real world

Cesium for Unreal provides a geographical foundation and access to spatial information such as terrain, 3D Tiles, meshes and available feature-identification data.

The aim is not simply to use Cesium's streamed representations as the finished game environment. Those representations are valuable geographical references, but they are not necessarily built for the visual quality, consistency, interaction and gameplay requirements of a life simulation.

Living World aims to use available geographical and spatial information to procedurally reconstruct its own Unreal Engine environments.

The longer-term generation system is intended to cover:

- Roads, streets, junctions and pathways.
- Terrain and landscape features.
- Buildings and architectural structures.
- Infrastructure and surrounding environments.
- The details that make locations visually coherent and recognisable.

**The real world supplies the reference. Our procedural systems generate the playable environment.**

### 2. Architecture that belongs to its region

Buildings should reflect the places they belong to. Architecture changes between countries, regions, towns, neighbourhoods and periods — a single generic building style would lose that local character.

The proposed **Regional Procedural Architecture System** is based on one reusable building-generation engine, driven by regional architectural profiles.

Profiles will define rules and controlled variation for building types, proportions, roof forms, facades, materials, windows, doors, plot layouts and local details. The same generation framework can then support different architectural regions without creating a completely separate building generator for each one.

The system is a development direction, not a claim that a worldwide catalogue of regional architecture already exists. The first profiles and their scope will be developed progressively.

### 3. Bring the world to life

The life simulation is just as important as the environment. The ambition is to create a persistent society of fictional people who have their own lives, destinations, responsibilities and relationships.

Over time, NPCs should be able to:

- Live in homes and visit familiar places.
- Work, shop, eat and socialise.
- Follow routines and make independent decisions.
- Build friendships, relationships and families.
- Use businesses, services and public spaces.
- Respond to weather, time and local circumstances.
- Continue their lives when the player is elsewhere.

The goal is not merely to generate crowds. It is to give people reasons to exist, places to go and things to do.

---

## A world with its own daily rhythm

Towns and cities should change character throughout the day.

**Morning and daytime**
- Commuters travelling to work.
- Shops opening and customers arriving.
- Busy high streets, cafés, restaurants and workplaces.
- School journeys, deliveries and everyday errands.

**Evening**
- People finishing work and heading home.
- Restaurants and pubs becoming busier.
- Friends meeting, shopping and socialising.

**Night-time**
- Clubs and nightlife venues filling with people.
- Groups meeting up and travelling into town.
- Taxis, late-night food and overnight workers.
- Busy entertainment areas alongside quieter residential streets.

**Overnight and early morning**
- Deliveries, cleaning and maintenance.
- People finishing night shifts or nights out.
- Early commuters and businesses preparing to open.

These are ambitions for the simulation to produce through schedules, destinations, businesses and autonomous behaviour — not simply crowds that appear at particular times.

---

## Real-world weather and conditions

Living World is intended to connect the environment to real-world conditions.

Local real-world weather is intended to update every **15 minutes**. Weather can influence the appearance of the environment as well as the behaviour and choices of people within it.

Potential effects include:

- Rain, snow and precipitation.
- Wind, foliage and surface conditions.
- Cloud cover, lighting, fog and visibility.
- Temperature and comfort.
- Outdoor activities, travel and NPC routines.

The project distinguishes real-world information — such as geographical data and weather observations or forecasts — from fictional game systems such as NPCs, businesses, relationships and events. Simulated people and events are part of the game, not claims about real individuals or real-world activity.

---

## The player's place

The player inhabits the world as an ordinary person. They can explore, work, travel, shop, socialise, develop relationships and create their own routine.

There does not need to be a constant stream of compulsory missions. Everyday life, unexpected encounters and opportunities created by the simulation should provide much of the experience.

The wider world should continue to function whether or not the player is present.

---

## Technology and development

**Technical foundation**
- Unreal Engine 5.8.
- Cesium for Unreal.
- C++ and Unreal Blueprints.
- Procedural city, building and terrain generation.
- Geographical positioning and spatial data.
- Weather and environmental integration.

**Longer-term development areas**
- More advanced real-world environment reconstruction.
- Regional architectural profiles and building variation.
- Roads, buildings, terrain and infrastructure generation.
- Autonomous NPC routines and social behaviour.
- Businesses, employment and local economies.
- Persistent world simulation and environmental response.
- Expansion to larger geographical areas.

The project is being developed progressively. Some underlying procedural systems and fixes are already recorded in the working project; the full regeneration framework and deep life simulation remain ongoing development goals.

---

## Project repositories

This public repository is for the **Living World project introduction, documentation, planning and selected progress updates**.

The Unreal Engine project and its source files are maintained separately in a private GitHub repository. The public repository does not contain the private game project or its large assets.

The working Unreal project and module retain the name `Walsall_Game`. **Living World** is the public-facing project identity; the underlying project was not renamed as part of the GitHub setup.

---

## Public development and reuse

Living World is developed in public, but this repository is **not currently open source**. Public visibility does not grant permission to reuse, copy, modify, redistribute or commercially exploit project materials unless an explicit licence or written permission says otherwise.

Third-party software, datasets, imagery, plugins and assets remain subject to their own licences and terms. See [LICENSE](LICENSE) and [LICENSING.md](LICENSING.md).

## Get involved

Constructive feedback, research, design ideas, testing, documentation, art and development contributions are welcome.

- Read [CONTRIBUTING.md](CONTRIBUTING.md).
- Browse the [development roadmap](ROADMAP.md).
- Review the [project overview](docs/PROJECT_OVERVIEW.md).
- Discuss substantial contributions before starting work.

The roadmap describes priorities, not guaranteed delivery dates. It will evolve as prototypes and technical work establish what is practical.

---

## Guiding principle

**First, regenerate the world. Then bring it to life.**

A world that doesn't revolve around the player — because everyone and everything has a life of its own.
