# ZoneData 

Pokemon XY's map is placed on a matrix, divided into 40x40 "Zones". These Zones, when occupied, are handled in-game as header files that specify a terrain model, NPC models, Building models, and a collision map to be assembled together into a map zone using rendering configurations as specified by AreaData.

ZoneData archives are BinLinker files with ZO magic. There are 349 of them and they store:

 * 0 - Zone header (custom format)
 * 1 - Zone entities (custom format)
 * 2 - Map script (.amx file)
 * 3 - Encounter data (custom format)
 * 4 - Reflections (NPC mirror)

## Zone Headers

Zone Headers (known as Map Headers in the gen 4 scene) specify general flags and data for each Zone.

```c++
struct ZoneHeader{
    /*0x00*/ uint8_t mapType; // defines map type, seems to be an enum
    /*0x01*/ uint8_t mapMove; // no idea what this is
    /*0x02*/ uint16_t areaDataID; // Index of the AreaData archive used by this zone
    /*0x04*/ uint16_t mapMatrixID; // Index of the Map Matrix file this zone is a part of
    /*0x06*/ uint16_t textID; // ID of the text archive used by this Zone?
    
    /*Background Music, this section seems to be a Gen 5 leftover as Gen 6 doesn't support seasons*/
    /*0x08*/ uint32_t BGMSpring; // This field is used in gen 6 to determine the Zone's BGM
    /*0x0C*/ uint32_t BGMSummer; // Unused in gen 6.
    /*0x10*/ uint32_t BGMAutumn; // Unused in gen 6.
    /*0x14*/ uint32_t BGMWinter; // Unused in gen 6.
    
    /*0x18*/ uint16_t scriptID; // This seems to be unused? 
    /*0x1C*/ uint16_t townMapGroup; // [TODO: Investigate how the town map works]
    
    /*0x20*/ uint16_t H0x1C {
  		parentMap : 10,
  		OLvalue : 6
	};
	/*0x22*/ uint16_t H0x1E {
  		weather : 5,
  		enableSkybox : 1,
  		enableRollerskates : 1,
  		battleBG : 7,
  		unused: 2
	};
	/*0x24*/ uint16_t H0x20 {
  		mapChangeEffect : 5,
  		unused : 5, //are we sure this is unused....?
  		enableCycling : 1,
  		enableRunning : 1,
  		enableEscapeRope : 1,
  		enableFlyFrom : 1,
  		enableCyclingBGM : 1,
  		unknownFlag : 1
	};
    
    /*0x26*/ uint16_t bgSysType; // unsure what this is
    /*0x28*/ uint16_t unusedField; // but are we actually sure this is unused....
    /*0x2A*/ uint16_t uniqueSequenceLibraryID; // Something related to Cameras....?
    
    /*0x2C*/ uint32_t unknownFlags {
        enableBloom : 1, // [TODO: investigate this]
        enableFlash : 1, // Apparently this field only enables flash in ORAS? what does it do in XY....
        enableInverseKinematics : 1, // The heck is an Inverse Kinematics??
        enableReverb : 1, // Que
        unknownFlags5to11 : 7,
        enableBreathFX : 1, // Enables the Breathing effects you can sometimes see in snowy cities a la Snowbelle City
        enableDowsingMachine : 1,
        unknownFlag14 : 1, // Hello says this flag is related to pss_interfare_window_proc in XY?
        unknownFlag15 : 1,
        enableStereostopic3D : 1, // This apparently enables 3D? [TODO: investigate this]
        stereo3DType : 4, // This needs investigation too
        isRail : 1, // Can't Zones use a mix of Rails and Grids? [TODO: investigate this]
        unused : 11
    };
    
    /*0x30*/ uint32_t flyX;
    /*0x34*/ uint32_t flyY;
    /*0x38*/ uint32_t flyZ;
}; // size = 0x3C
```

> ! This header info is exclusive to XY. Zone Headers in ORAS have a slightly different format.

## Zone Entities

The Zone Entities file keeps track of all NPCs, Furnitures, and Triggers in each zone.

```C++
struct ZoneEntities{
    /*0x00*/ uint32_t totalLength;
    /*0x04*/ uint8_t furnitureCount;
    /*0x05*/ uint8_t NPCCount;
    /*0x06*/ uint8_t warpCount;
    /*0x07*/ uint8_t normalTriggerCount;
    /*0x08*/ uint8_t silentTriggerCount;
    /*0x09*/ uint8_t unused[3]; // Oh my god did GF actually a Short to store all these instead of storing them in individual bytes
    Furniture furnitures[furnitureCount];
    NPC npcs[NPCCount];
    Trigger normalTriggers[normalTriggerCount];
    Trigger silentTriggers[silentTriggerCount];
};

struct Furniture{
    /*0x00*/ uint16_t script;
    /*0x02*/ uint16_t interestType;
    /*0x04*/ uint16_t interactDirection;
    /*0x06*/ uint16_t rail; // ??
    /*0x08*/ uint16_t x;
    /*0x0A*/ uint16_t y;
    /*0x0C*/ uint16_t w; // width?
    /*0x0E*/ uint16_t h; // height?
    /*0x10*/ uint16_t alt; // ??
};

struct NPC{
    /*0x00*/ uint16_t uniqueID;
    /*0x02*/ uint16_t uniqueModelID;
    /*0x04*/ uint16_t moveCode;
    /*0x06*/ uint16_t eventType;
    /*0x08*/ uint16_t spawnFlag;
    /*0x0A*/ uint16_t script;
    /*0x0C*/ uint16_t faceDirection;
    /*0x0E*/ uint16_t params[3]; // no clue what this is for
    /*0x10*/ uint16_t areaStartX;
    /*0x12*/ uint16_t areaStartY; 
    /*0x14*/ uint16_t areaWidth;
    /*0x16*/ uint16_t areaHeight;
    /*0x18*/ uint16_t multiZoneLinkOriginZone; // ??
    /*0x1A*/ uint16_t multiZoneLinkTargetZone; // ??
    /*0x1C*/ uint16_t multiZoneLinkHostZone; 
    /*0x1E*/ uint16_t multiZoneLink1Type;
    /*0x20*/ uint32_t isPositionRail;
    
    /*if isPositionRail is 1 then the NPC's position is Rail-based*/
    /*0x24*/ uint32_t railLineID;
    /*0x28*/ uint16_t railPosA;
    /*0x2A*/ uint8_t railPosB; 
    /*0x2B*/ uint8_t railLineDirection;
    
    /*if isPositionRail isn't 1 then the NPC's position is Grid-based*/
    /*0x24*/ uint16_t xTile;
    /*0x26*/ uint16_t yTile;
    /*0x28*/ float z3DCoordinate; // 4 bytes
};

struct Warp{
    /*0x00*/ uint16_t targetZone;
    /*0x02*/ uint16_t targetWarpID;
    /*0x04*/ uint8_t faceDirection;
    /*0x05*/ uint8_t transitionType;
    /*0x06*/ uint16_t isPositionRail;
    
    /*if isPositionRail is 1 then the Warp's position is Rail-based*/
    /*0x08*/ uint32_t railLineID;
    /*0x0C*/ uint16_t railPoseFront;
    /*0x0E*/ uint16_t railPosSide;
    /*0x10*/ uint16_t h; // "dim front"?
    /*0x12*/ uint16_t w; // "dim side"?
    
    /*if isPositionRail isn't 1 then the Warp's position is grid-based*/
    /*0x08*/ uint16_t gridX;
    /*0x0A*/ uint16_t alt; // ??
    /*0x0C*/ uint16_t gridZ;
    /*0x0E*/ uint16_t w;
    /*0x10*/ uint16_t h;
    /*0x12*/ uint16_t directionality;
    
    /*0x14*/ uint16_t unknown0x14;
    /*0x16*/ uint16_t unknown0x16;
};

struct Trigger{ // [TODO: investigate the difference between Silent Triggers and Normal Triggers]
    /*0x00*/ uint16_t script;
    /*0x02*/ uint16_t spawnWorkRefValue;
    /*0x04*/ uint16_t spawnWork;
    /*0x06*/ uint32_t isPositionRail; // Why is this an int instead of a byte??
    /*0x0A*/ uint16_t unknown0x0A; 
    /*0x0C*/ uint16_t x;
    /*0x0E*/ uint16_t y;
    /*0x10*/ uint16_t w; // width?
    /*0x12*/ uint16_t h; // height?
    /*0x14*/ uint16_t alt; // ??
    /*0x16*/ uint16_t unknown0x16;
};
```

## Map Script

This file is a compiled .amx file, storing all entity functionality related to the specific Zone. [TODO: it actually seems like some trainer functionality is stored inside global scripts? investigate this more]

## Zone Encounter tables

ZoneData stores encounter tables specifying the chance that the player will run into wild pokemon while:

- Going around using Surf
- Fishing
- Walking inside tall grass (or in the case of XY tall grass and flowers)
- Walking normally (for caves)
- Smashing rocks using the HM Rock Smash
- Walking around trying to get a Horde encounter

[TODO: locate where all these tables are stored]

## Reflections

This file is a table storing info about.... NPC reflections? [TODO: uh how do NPC reflections work?]