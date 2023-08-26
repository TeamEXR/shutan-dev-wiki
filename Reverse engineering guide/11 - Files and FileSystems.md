# Files and FileSystems
We've already learned that everything in a computer system is encoded to 0s and 1s. and so far we've worked with binary blobs that could represent anything we want.

But what if we want different binary blobs, decoded differently, organized and tagged properly?

For this we use a highly useful abstraction called a "File system". In this abstraction every blob of code is assigned a "header" that describes information about the blob, turning it into a file. Then all the files are organized in a tree structure for easy accesss.

There are many different types of filesystems and they all differ in how they implement the abstraction. 

## Typical file and filesystem structures
Most files start with a **header** that provides info about the internals of the file (or in an archive/directory's case, about the files *inside*). The header usually has a unique sequence of bytes in the start, called the **magic**, to inform the format of the file.
Sometimes files end with **footers** too which accomplish the same roles as headers but it's rare.

Note that directories are technically files too, they're simply designed to only have information about the files inside them and nothing else.
