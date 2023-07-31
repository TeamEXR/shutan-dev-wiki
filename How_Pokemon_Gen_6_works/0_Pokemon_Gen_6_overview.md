## Pokemon Generation 6 Overview

Generation 6 of pokemon games consists of two pairs of games; Pokemon X and Y (codenamed Kujira internally) and Pokemon Omega Ruby and Alpha Sapphire (codenamed Sango internally).

These games consist of four major parts:

- "Field", aka the Overworld and everything that takes place in said overworld.
- "Battle", aka the pokemon battles
- "Kawaigari" aka Pokemon Amie
- "Apps", smaller self-contained pieces of game code that compliment the three main pillars above e.g. shopping for clothes, Phil the camera guy's photoshoots, and the Bag
  - This includes "Field app"s aka the different things you can access in the bottom panel while in the overworld (PSS, Super Training, Amie's minigames and decoration)

> There are also minor part of the game code not contained in the above such as savedata code, movie playing code, Live challenge code, etc.

The game code is shared between ORAS and XY with very minor changes outside of the addition of new features in ORAS such as the skytrip.

Both pair of games are built on GameFreak's internal game engine called gflib_cpp. And in turn gflib_cpp is built on the NintendoWare4CTR engine and the Nintendo 3DS SDK.

> NintendoWare4CTR is a middleware engine offered by Nintendo to help speed up the development of 3DS games. It includes a rendering pipeline, a GUI framework, and an audio processing pipeline. Many first party Nintendo games including Pokemon use it because it's optimized to run well on the console.

## The Gen 6 games are highly modular

The Gen 6 games consist of multiple, highly independent systems that come together to form what the player sees in a normal playthrough. With as much of the game stored inside assets as possible:

- Multiple individual components (ZoneData, AreaData, Collision maps, Camera configurations, NPC/Prop registries, a lot of model/animation files, map matrixes) are used to assemble the map together on runtime.
- Many of the games' systems (Pokemon reactions to getting touched in Amie, the entire battle AI, NPC behavior, progression gating) is done through scripts that were written in the Pawn Script language then compiled into .amx files
- Almost all of the game's stats, NPC/interactables information, and item/pokemon data is stored inside asset files. These are usually proprietary formats that were compiled from Excel spreadsheets or special .cdat files dating back to gen 3

Each one of those components can easily be swapped without breaking anything. 

The only components handled by code are things that are needed to run all of the asset based systems. Such as the Field engine, the Battle engine, the Amie engine, etc. As well as those "App"s mentioned earlier.

## The Gen 6 games have a lot of obsfucation

There's many weird design choices involved in how gen 6 games handle their assets such as Pawn Script command names being hashed, assets being stored inside archive files without any names, and GUI elements using hashed names. These can only be explained as obfuscations meant to prevent modders like us from having an easy time, or to prevent data from leaking before they're meant to be shown (mostly in the case of event pokemon).

