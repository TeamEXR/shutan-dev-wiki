# Archive files in gen 6 games

Generation 6 and 7 of Pokemon games pack up their assets inside special archive files, which are then further packed into other archive files.

The top level files inside the `a/` directory inside the pokemon games' romfs are GARC files. GARC stands for "**G**amefreak **ARC**hive". It's a fork of a well known Nintendo DS format called NARC ("**N**intendo **ARC**hive") that lets gamefreak refer to archives as an enum and obscure the actual file names during building. Turning something like `assets/pokemon_model.garc` into `a/0/0/7.garc` and referring to it as `POKEMON_MODELS_GARC = 007`

> While GARC files don't support folders, they actually support multiple language versions for the same files. This is mostly used in GARCs that store GUI textures.

> ! Gen 6 games use GARC version 4 while gen 7 games use GARC version 6. This page only describes the GARC 4 format.

## GARC file format

The GARC header consists of the main header, followed by three "Block"s: 

- "File Allocation Table Offset" (FATO): Stores offsets to each entry in the FATB.
- "File Allocation Table Block" (FATB): Describes the name, language ID, compressed size, and uncompressed size of each file in the GARC.
- "File Image Block" (FIMB): Specifies the size of the data block, not counting the size of the header

All the data for the files inside the GARC follows after the header. It is unknown how the file data is ordered but they're accessible through offsets specified in their FATB entries.

> GARCs don't support file names. 

```c++
struct GARCHeader{
    MainGARCHeader header;
    FATO fato;
    FATB fatb;
    FIMB fimb;
};

struct MainGARCHeader{
    /*0x00*/ char magic[4];            // == "CRAG"
	/*0x04*/ uint32_t sectionSize      // Size of the entire MainGARCHeader, must be 0x1C
    /*0x08*/ uint16_t endianness;      // Byte Order Marker, should be read in an endianness that reads it as "0xFEFF" (GARC headers are always little endian(?))
    /*0x0A*/ uint16_t version;         // == 4 for XY/ORAS
    /*0x0C*/ uint32_t blockCount;      // apparently all GARCs only have 4 "blocks": GARC, FATO, FATB, FIMB
    /*0x10*/ uint32_t dataOffset;      // offset to the end of the header and the start of the data
    /*0x14*/ uint32_t archiveSize;     // size of the entire archive (not sure if header size is counted)
    /*0x18*/ uint32_t largestDataSize; // size of the largest file in the GARC. not sure why this is kept track of
}; //size = 0x1C

struct FATO{
    /*0x00*/ char magic[4];                // == "OTAF"
    /*0x04*/ uint32_t sectionSize;         // size of the entire FATO
    /*0x08*/ uint16_t entryCount;          // number of FATO entries
    /*0x0A*/ uint16_t padding;             // padding, always 0xFFFF
    /*0x0C*/ uint32_t offsets[entryCount]; // offsets to FATB entries
};

struct FATB{
    /*0x00*/ char magic[4];                 // == "BTAF"
    /*0x04*/ uint32_t sectionSize;          // size of the entire FATB
    /*0x08*/ uint32_t entryCount;           // number of FATB entries
    /*0x0C*/ FATBEntry entries[entryCount]; // list of FATB entries (unsure if stored inside FATB's header or further deep inside the file)
}; 

struct FATBEntry{
    /*0x00*/ uint32_t languageBits{
        	LANG_DEF : 1; // NULL/Not Localized
        	LANG_JPN : 1; // Japaneese
        	LANG_USA : 1; // American English
        	LANG_FRA : 1; // French
        	LANG_ITA : 1; // Italian
        	LANG_DEU : 1; // German
        	LANG_DMY : 1; // Uhhhh Chineese? [TODO: ask Zero what this is] (unused)
        	LANG_ESP : 1; // Spanish
        	LANG_KOR : 1; // Korean
        	LANG_RUS : 1; // Russian (unused)
        	LANG_NLD : 1; // Dutch (unused)
        	LANG_PRT : 1; // Portugeese (unused)
        	UNUSED : 20;
    };
    /*0x04*/ uint32_t startOffset;   // Offset to the start of the file data 
    /*0x08*/ uint32_t endOffset;     // Offset to the end of the file data
    /*0x0C*/ uint32_t unpaddedSize; // Unpadded size of the file 
}; //size = 0x10

struct FIMB{
    /*0x00*/ char magic[4];          // == "BMIF"
    /*0x04*/ uint32_t sectionSize;   // Size of the entire FIMB (== 0x0C)
    /*0x08*/ uint32_t imageSize;     // Size of the Archive file's data section
} //size = 0x0C
```

## BinLinker file format

While the NARC format supports directories, the GARC format doesn't. This is because GameFreak experimented with bundling related files into a single binary file in Gen 5 and found accessing those files to be faster than when using directories. This lead them to create a format called "Binary Linker files" (BinLinker, .pack) that acts as a replacement for folders. These files are also known as TwoCC files because they use arbitrary two letter magics like AD and MM. 

> Despite their variable magic BinLinker files always have the extension .pack

The top level BinLinkers in every GARC are compressed. This helps reduce the game's size in GARCs that contain a lot of data (the biggest example of this is the GARC containing models, textures, and animation for every single pokemon). The accurate extension  for these files would be .pack.lz

```c++
struct BinLinkerHeader{
    /*0x0*/ char magic[2];                   // can be anything.
    /*0x2*/ uint16_t fileCount;              // number of files stored inside
    /*0x4*/ uint32_t fileOffsets[fileCount]; // array of starting offsets to file data
}
```

BinLinker files do not support file names either.

## BinLinker Compression

Nintendo games can use a variety of compression formats provided by the SDK. Among these is two algorithms: LZ10 and LZ11 (called LZ77 and LZ77 Expert mode respectively). These two algorithms are forked from the LZSS compression algorithm, using different encodings and some tricks to tweak compression efficiency.

All BinLinker files in the pokemon games are compressed using LZ11 algorithm, also called LZ77 Expert mode.
