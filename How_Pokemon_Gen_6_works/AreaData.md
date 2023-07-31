# AreaData

AreaData are archive files responsible for setting the general look and feel of an area. They've been used ever since Gen 3 to configure rendering properties of different Zones. The way this works is that each Zone can subscribe to an AreaData using an `AreaDataID` field in their header, then the game will use that AreaData's information when assembling the zone together.

AreaData archives are BinLinker archives with the AD magic, there's 170 of them and they store:

- 0 - Prop registry file (custom format) 
- 1 - Prop textures (.bch file)
- 2 - "World Animations" (.bch file) [TODO: look into what this does]
- 3 - Camera data (custom format)
- 4 - Fragment shader Day/Night cycle parameters (custom format?)
- 5 - Environment assets (clouds, extra lighting) (.bch file)
- 6 - Default camera data (custom format)
- 7 - Extended area collision (custom format)
- 8 - Map LOD assets (.bch files stored inside LL BinLinker files stored inside a single AL file)
- 9 - Global LOD assets (.bch files stored inside LL BinLinker files stored inside a single AL file)
- 10 - Unused in both XY and ORAS (Secondary global LOD assets according to reverse engineering) [TODO: what??]
- 11 - World textures (.bch file)

[TODO: look into exactly what ZoneData and AreaData archives store, and their formats]

[TODO: look into NPC registries and Building registries]