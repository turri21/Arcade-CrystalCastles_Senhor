-=(CrystalCastles_Senhor notes)=-

Tested: Working Video 720p, 1080p & Sound.

Dev notes: Clocks swapped in sys.tcl
___
# [Arcade: Crystal Castles](https://en.wikipedia.org/wiki/Crystal_Castles_(video_game)) for [MiSTer FPGA](https://mister-devel.github.io/MkDocs_MiSTer/)
An FPGA implementation of the __Crystal Castles__ arcade hardware by __Atari__ for the MiSTer platform.

## General Description
Author: [Enceladus](https://github.com/0xECEAD)<br>
From: Atari 1983<br>
Date: Aug-Nov 2022<br>
Version: playable<br>
SDRAM: no<br>

## Info
Game Clock: 10 MHz<br>
Pixel Clock: 5 Mhz<br>
Horizontal: counter 320, visible 252, hsync => 15.625 kHz<br>
Vertical: counter 256, visible 232, vsync => 61.03 Hz<br>
VGA scan doubler working (forced_scandoubler=1 in mister.ini)<br>

## Known Issues
In cocktail mode the player 2 upside down screen and sprites are not positioned correctly.<br>

## Todo
Check sprite horizontal location on actual hardware. <br>
Keep high-scores, copy NVRAM data back to the MiSTer. <br>
Use logic analyzer on Atari Potato chip to check scrolling and memory addressing (clamp 0-23 => 24 ???). <br>

## Controller
This version can be played with an actual TrackBall connected to the SNAC connector (best experience!).<br>
USER_IN[0]=Jump/Start, USER_IN[1]=Coin Left. Both switch to GND.<br>
USER_IN[2]=Vertical Quadrature encoder A, USER_IN[3]=Vertical Quadrature encoder B,<br>
USER_IN[4]=Horizontal Quadrature encoder A, USER_IN[5]=Horizontal Quadrature encoder B.<br>
<br>
Emulation of a TrackBall is also provided for digital joystick, analog joystick or mouse. <br>
You can set the sensitivity for your device in the OSD menu.

## Credits, acknowledgments, and thanks
- [__Enceladus__](https://github.com/0xecead): Core design and implementation.
- Original 6502 core by Arlet Ottens, 65C02 extensions by David Banks and Ed Spittles.
- Atari Pokey by Mark Watson (c) 2013 (VHDL), conversion to Verilog by (?).
- Trackball Emulator based on work by [__Jim Gregory__](https://github.com/JimmyStones).

## Modifications
- Pokey: Added clock-enable (CE) to make clock divider redundant.
- Trackball Emulator: Adopted for 4x Quadrature, Added option for a true TrackBall on the SNAC connector.

## FPGA implementation
- Created using original schematics, and insight from own tools and tests with a custom diagnostic rom.
- TTL74 logic has been simplified, and re-engineered where necessary. 
- 82S129 PROMs were replaced by their equivalent logic expressions.
- Clock dividers were replaced with equivalent clock-enable signals. So the game clock (10MHz) only connects to clock inputs, and logic signals only connect to logic inputs (not clocks). This results in a cleaner FPGA synchronous design (citation needed).

## Quartus Version
Cores must be developed in **Quartus v17.0.x**. It's recommended to have updates, so it will be **v17.0.2**. Newer versions won't give any benefits to FPGA used in MiSTer, however they will introduce incompatibilities in project settings and it will make harder to maintain the core and collaborate with others. **So please stick to good old 17.0.x version.** You may use either Lite or Standard license.

## ROM Files Instructions

ROMs are not included! In order to use this arcade core, you will need to provide the correct ROM file yourself.

To simplify the process .mra files are provided in the releases folder, that specify the required ROMs with their checksums. The ROMs .zip filename refers to the corresponding file from the MAME project.

Please refer to [Arcade Roms and MRA files](https://mister-devel.github.io/MkDocs_MiSTer/developer/mra/) for information on how to setup and use the environment.

Quick reference for folders and file placement:
```
/_Arcade/Crystal Castles.mra
/_Arcade/cores/CrystalCastles_20221121.rbf
/_Arcade/mame/ccastles.zip
```
