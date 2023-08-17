# Pawn Scripts

The gen 6, gen 7, and to some extent gen 8 Pokemon games use the Pawn Scripting Language for their scripts. Specifically a fork of Pawn version 3.3.4097 with hashed function names. These script files were written in a C-like language inside .p files then compiled into .amx Pawn Assembly files by a fork of the open sourced compiler.

The entire battle AI, text handling code for Battles, almost all of the NPC/Furniture behavior, and Amie interaction logic is implemented with pawn files. 

[TODO: confirm the following paragraph] Each Zone in the field can use a "Level Script" which always runs in the background. Additionally they can also use a different script file to define NPC behavior. In contrast "Global Script" files take care of things that aren't necessarily tied to zone-specific field behavior. 

[TODO: make a list of all global pawn script files and what they actually do]

ExeFS's code.bin has the core Pawn runtime embedded inside, while various CROs store "Script Commands" functions script files can invoke to do things.

[TODO: add list of known Script commands here]