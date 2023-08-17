# BinLinker file format

Accessing binary blobs directly using simple offsets is often faster than executing filesystem calls to access files. As such depending on the amount of performance gained it might be viable to drop the concept of filesystems altogether and bundle files directly into one binary blob with a table of offsets.

GameFreak experimented with this idea in gen 5 and packed related asset files for any given thing into binary blobs, called "Binary Linked archives" (also known as BinLinkers). As the approach was successful they carried it over to gen 6 and 7 respectively.

These files use a variable two letter magic, letting the game identify what kinds of items are stored inside the BinLinker file. For example a BinLinker archive with the magic "AD" most likely has AreaData related files inside it.

> Despite their variable magic BinLinker files always have the extension .pack


```c++
struct BinLinkerHeader{
    /*0x0*/ char magic[2];                   // can be anything.
    /*0x2*/ uint16_t fileCount;              // number of files stored inside
    /*0x4*/ uint32_t fileOffsets[fileCount]; // array of starting offsets to file data
}
```
As you can see BinLinker files don't support file names either, this is because their assumed content is hardcoded by the game's code and tracked there.
