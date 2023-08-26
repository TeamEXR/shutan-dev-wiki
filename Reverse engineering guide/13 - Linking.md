# Linking

Linking is the process of concatenating multiple machine code files into one executable efficiently, therefore speeding up application performance and making it easier to manage the application files.
This is usually done by arranging the contents of each file together in memory, then "resolving" all cross-file function calls by converting them into hard offset jumps.

During the process of linkage any libraries used by the application can also be linked to the main executable, becoming a part of it and always loading into memory alongside it.
