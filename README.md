# Mortal Kombat Trilogy PC PSX Decompressor
## Reversing a 1996 Win95 Game
Work in progress Reverse Engineering MKTrilogy with the help of the symbols<br>
PC version is basically the PS1 Version, they did use PSY-Q and compile with OpenWatcom, the version is a "Beta" that's why there was embedded debug symbols 😂.

# spdriver aka Sprite Driver
This is managing the drawing process and texture cache management.

# The PC Version is in fact the PS1 Version Ported to PC

It seem that it load the data into the VRAM texture cache (mostly our Fighter data .DAT), it then iterate the texture cache and uncompress the texture(s) if it's flagged as compressed then it assign the palette by looking at the Color LookUp Table, there's a good global called 'decompBuffer' or something, it's used a lot by the game, once all of their algorithm has finished to decompress what's inside the texture cache, the sprite driver will create a new object and 'clip' a rectangle on the screen, which is our sprite x/y/u/v mapped, as the PS1 used PolyFT4 to draw a RECT as a primitive (Sprite).

It is important to note that Motaro and Shao Kahn are 'compressed' because they are huge, but by this i mean, their file seem more than simply encoded (or is all files just compressed 🤔 dunno yet).

I just started today and i found it quite amazing, it has even the globals marked which contain all the routine of the fighter animation since this game is a combination of "C" and ".S/.ASM" file, the game has many part of code which doesn't look right because it's there where they 'assembled' their file and it make sense when we know that.

Any character/background is called a "Module" as defined by the debug symbol, basically a "Module" is simply the character/background data that was assembled on this SEGMENT,it seem to be about the "commands/routine" it execute to call/spawn the attack/special moves, for the background it's perhaps that 'assembled' Module that handle the coordinate of the 'tiles' and assemble all the textures to make the level (it's probably different than the background Animation table) which is surely only made to tell that at X/Y coord we want to "draw this" with that "Frame" and possibly play the next frame/adjust the X/Y coordinate to make it moving if it should.

# My Workflow
![image](https://user-images.githubusercontent.com/19496833/133936231-1cc1ff1a-03df-4618-8536-97163ed9d9a7.png)
