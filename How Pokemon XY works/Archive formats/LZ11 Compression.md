# LZ11 Compression

Nintendo games can use a variety of compression formats provided by the SDK. Among these is two algorithms: LZ10 and LZ11 (called LZ77 and LZ77 Expert mode respectively). These two algorithms are forked from the LZSS compression algorithm, using different encodings and some tricks to tweak compression efficiency.

Many files in Pokemon XY GARCs are LZ11 compressed to help reduce it to a size that can be fit into a cartridge. It is currently unknown how LZ11 compression is decided (GARC level vs Individual files).

[TODO: Explain how LZ11 works]

[TODO: Make a list of every LZ11 compressed file inside XY]
