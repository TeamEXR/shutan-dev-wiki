# How 3DS games are structured
Nintendo 3DS games/apps always exist in a specific format called NCCH, which is wrapped inside other formats depending on how it's meant to be used:

- If the game is meant to go inside a cartridge, it goes inside a "CTR Cartridge Image" file (.cci). In most homebrew circles Cartridge dumps have a .3ds format
- If the game is meant to be installed into the system rather than existing on a cartridge, it gets wrapped into a "CTR Installable Archive" (.cia)

The NCCH for all 3DS games consists of two parts: Executable FileSystem and ROM FileSystem.

The ExeFS is a giant binary blob containing everything needed for the game to be recognized as an authentic 3DS game by the console. While the RomFS is a proper filesystem that contains every file that isn't a part of ExeFS. In the case of Pokemon XY this means all the CROs and asset files for the game.

The ExeFS contains the static module of the game's code (in the form of code.bin). That said 3DS games can store different parts of their code as relocatable modules that get compiled into "CTR Relocatable Objects" (CROS/.cro) and are stored at the RomFS root.

Pokemon (both gen 6 and 7), Mario Kart 7, and Animal Crossing games use CROs a lot to optimize on memory usage.