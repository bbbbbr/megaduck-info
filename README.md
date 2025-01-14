# Mega Duck / Cougar Boy Console Info
A collection of technical information and resources for the Mega Duck console brought together in one place. Much of it researched by others, some by me (minor sound reg fixes, laptop model docs, some ports and patches, etc).

[Web version](https://bbbbbr.github.io/megaduck-info/)

## References
- [Sean Riddle](https://www.seanriddle.com/megaduck.html)
- MAME: [1](https://github.com/mamedev/mame/blob/cd2b19164f38de66ff2e0f3b2f923b1abab598dd/src/devices/bus/gameboy/mdslot.cpp) [2](https://github.com/mamedev/mame/blob/ac3c4190eeb647596523182572e535424106421c/src/devices/bus/gameboy/rom.cpp) [3](https://github.com/mamedev/mame/blob/cd2b19164f38de66ff2e0f3b2f923b1abab598dd/hash/megaduck.xml)
- [MiSTer](https://github.com/MiSTer-devel/Gameboy_MiSTer/blob/4b06b6600683cf6b8b242d00c75baab160cd61ee/rtl/megaswizzle.sv)

## Credits / Thanks
Sean Riddle, Ruud van Falier, Nitro2k, Toxa, Youkal3, Zwenergy, Inside Gadgets, Kuddel


# Software

### Homebrew Games / Programs
- Browse releases (and find source code links) on the [MegaDuck Homebrew and ROM Hack showcase](https://bbbbbr.github.io/megaduck-gallery/).
  - There's also a view for [showing what's new](https://bbbbbr.github.io/megaduck-gallery/?sortSelector=Recently+Added)

### ROM Patches
Patches for running Game Boy games on the MegaDuck
- See ROM patches in the [MegaDuck Homebrew and ROM Hack showcase](https://bbbbbr.github.io/megaduck-gallery/index.html?softwareTags=ROM+Hack)

### Homebrew Music Tools
- [Droneboy for MegaDuck](https://github.com/bbbbbr/Droneboy_MegaDuck)


### Emulators/FPGA Re-implementations
- [Super Junior SameDuck](https://github.com/bbbbbr/SuperJuniorSameDuck): Fork of SameBoy with support for MegaDuck Handheld and Laptop models. Has correct audio emulation. Development oriented.
  
- [MAME](https://www.mamedev.org/), [Arcade DB Entry](http://adb.arcadeitalia.net/dettaglio_mame.php?game_name=megaduck), [Cart list xml](https://github.com/mamedev/mame/blob/4a6c54dd5e4fc06ef535816fa6c2f4597d2f593f/hash/megaduck.xml#L4)
- [SameDuck](https://github.com/LIJI32/SameBoy/compare/SameDuck) branch of SameBoy (modified version of SameBoy, not pre-built)
- [MiSTer](https://github.com/MiSTer-devel/Gameboy_MiSTer/issues/168): Has correct audio emulation
- [Analogue Pocket OpenFPGA core](https://github.com/spiritualized1997/openFPGA-Megaduck)


### Development Tools

#### SDKs / Build related

##### C language
- [GBDK-2020](https://github.com/gbdk-2020/gbdk-2020): C dev kit, supports Mega Duck as a build target
- [Cate83](https://github.com/inufuto/Cate) - A C-like programming language compiler for sm83 cpus (MegaDuck, Game Boy)
  - There are [several example game programs](https://github.com/inufuto/Cate_examples/tree/main/megaduck) for the MegaDuck

##### ASM
- [hardware.inc for MegaDuck](https://github.com/bbbbbr/hUGEDriver/blob/uncap_megaduck/include/hardware.inc): Hardware constants and addresses for use with asm/RGBDS
  - Newer [hardware.inc](https://github.com/bbbbbr/hUGEDriver/blob/master_megaduck/include/hardware.inc) base version
- [Asm83](https://github.com/inufuto/asm8) - An Assembler, linker and librarian for retro CPUs including the sm83 (MegaDuck, Game Boy)

#### Music / SFX
- [Mega Duck port of the hUGE Driver](https://github.com/bbbbbr/hUGEDriver) Game Boy music driver
- [Mega Duck port of the CBTFX](https://github.com/bbbbbr/CBT-FX) Game Boy Sound FX driver
#### Peripherals
- Sample code for interfacing with the MegaDuck Laptop model Keyboard, RTC and speech module (Quique and Junior Computer). See related partial [docs](https://github.com/bbbbbr/megaduck-quique-disasm/blob/main/docs/Megaduck%20Quique%20info.md)
  - [GBDK examples](https://github.com/gbdk-2020/gbdk-2020/tree/develop/gbdk-lib/examples/megaduck) 
  - [RGBDS asm examples](https://github.com/bbbbbr/megaduck_laptop_asm_examples)
- [Audio recordings](https://github.com/bbbbbr/megaduck-info/tree/main/assets/laptop_speech/) of the 6 built-in speech phrases for the German and Spanish MegaDuck Laptop models


# Hardware

### Flash Cartridges
- [picoDuck by zwenergy](https://github.com/zwenergy/picoDuck) an Open-source RP2040-based flash cart
  - [Alternate firmware](https://github.com/bbbbbr/picoDuck/releases/tag/1MB_MD2_only_v1.0) which supports up to 1MB ROMs with the MD2 (only) type MBC (required for some homebrew and rom patches)
- [A2 Heaven multi-flash cart](http://www.a2heaven.com/webshop/index.php?rt=product/product&product_id=172)
- [Inside Gadgets 32K flash cart](https://shop.insidegadgets.com/product/megaduck-32kb-flash-cart/) - Compatible with [GBXCart flasher](https://www.gbxcart.com/)
- [3D Printable cartridge shell](https://github.com/bbbbbr/megaduck_cartridge_shell)

### Display mod / LCD Header info
- [Display adapter board by zwenergy](https://github.com/zwenergy/MegaDuck-GB-IPS-Adapter) for Game Boy DMG style display kits
- [Ruud van Falier's DMG IPS adapter mod](https://hackaday.io/project/191431-mega-duck-aka-cougarboy-ips-screen-mod)
  - [3D printable bracket for the DMG IPS display](https://www.thingiverse.com/thing:6590836)
- [Game Boy Pocket (MGB) to Mega Duck display adapter](/assets/Diagram_Game_Boy_Pocket_MGB_to_Mega_Duck_to_display_adapter.jpg)

### Laptop model Gamepad
- [Info for building a replacement Gamepad / "Mouse"](/docs/Quique_gamepad.md) for the MegaDuck Laptop model

### Serial Link Port
- The link port has a different conenctor style (bare header) than the Game Boy, but the pin order and signals appear to be the same. With the use of a connector style adapter a Mega Duck and a Game Boy can exchange data over their link ports. Catskull has [Game Boy link port parts](https://catskullelectronics.com/collections/game-boy/products/gba-gbc-link-port) that can be used to build an adapter.
- The serial link registers appear to have the same address, control flags and behavior as a classic Game Boy

### Cartridge Pinout
- [Mega Duck Cart Dumping](https://www.seanriddle.com/megaduck.html)
- Scans:
  - OEM (Pile Wonder) [Front](/assets/megaduck_cartridge_oem_1200dpi_front.jpg) / [Back](/assets/megaduck_cartridge_oem_1200dpi_back.jpg)
  - IG 32K  [Front](/assets/megaduck_cartridge_insidegadgets32k_1200dpi_front.jpg) / [Back](/assets/megaduck_cartridge_insidegadgets32k_1200dpi_back.jpg)

### AC Adapters
Handheld
  - 3.5 mm exterior, 1.35mm interior
  - 6 volts, centrer NEGATIVE polarity

Laptop
  - 3.5 mm exterior, 1.35mm interior
  - 9 volts, centrer POSITIVE polarity
  - [Example picture](/assets/megaduck_super_quique_laptop_universal_ac_adapter_9v.jpg)

### MBCs / Bank Switching

#### MBC Controllers
**Laptop model System ROM MBC (CEFA Super Quique, Hartung Super Junior Computer):**
  - Informal MBC Number: `0xE0` (SuperJuniorSameDuck emulator)
  - Informal extension: `.md0`
  - Register: `0x1000`
    - ROM Bank
      - Selected by writing (`0 - 15`) in Lower Nibble (mask `0x0F`)
      - Bank Size/Region: Switches the full 32K ROM region- 
    - External plug-in Memory Cart SRAM Bank
      - Selected by writing (`0 - 3`) in Upper Nibble (mask `0x30`)
      - Bank Size/Region: 8k mapped at `0xA000 - 0xBFFF`
  - Note: Uses a delay of ~41 M-Cycles (executed from WRAM) after writing the bank switch before resuming execution from ROM. Unclear if required.

**OEM Games:**
- 32K with NO switchable banks
  - Sometimes with extension: `.bin`, but that may also be used for banked ROMs with some emulators
  - Games: Arctic Zone, Bomb Disposer, Magic Maze, Pile Wonder, Street Rider, The Brick Wall, Trap and Turn, Vex 
- 32K switchable banks
  - Sometimes with extension: `.md1`
  - Informal MBC Number: `0xE1` (SuperJuniorSameDuck emulator)
  - Register: Bank selected by writing `0 - 1` to `0xB000`
  - Bank Size/Region: Switches the full 32K ROM region
  - Games: Puppet Knight, Suleiman’s Treasure
- Upper switchable 16K banks
  - Sometimes with extension: `.md2`
  - Informal MBC Number: `0xE2` (SuperJuniorSameDuck emulator)
  - Register: Bank selected by writing `1 - 3` or `1-7` to `0x0001` depending on total ROM size (64K or 128K)
  - Bank Size/Region: 16K in the Upper ROM region `0x4000 - 0x7FFF` (lower 16K at `0x0000 - 0x3FFF` is fixed bank 0)
  - Games: 2nd Space, Ant Soldiers, Armour Force, Beast Fighter, Black Forest Tale, Captain Knick Knack, Commin Five in One, Duck Adventures, Four in One, Magic Tower, Railway, Snake Roy, Worm Visitor, Zipball

MBC type per game is according to [Reddit](https://www.reddit.com/r/AnaloguePocket/comments/zgmwqh/question_about_the_mega_duck_core_and_rom_file/)

#### Implementation in emulators
Game Boy ROMs contain an embedded meta-data header which (usually) indicates the type of MBC (Memory Bank Controller) used. This allows emulators to automatically emulate the correct cart hardware (the Game Boy hardware itself ignores this and doesn't need it since the cart hardware is present). 

OEM Mega Duck ROMs lack this header which means that emulators have to use other methods to infer what type of cart MBC is required by a given ROM.

The main methods for selecting the right MegaDuck cart MBC:
- By File Extension (`.md1` = 32K banks, `.md2` = Upper 16K Banks, `.bin` = 32k no mbc)
  - Analogue Pocket OpenFPGA MegaDuck Core
- By hashes of the ROMs
  - MAME (partially)
- By emulating both MBC styles at the same time in case a game uses either. This works since the two MBCs use a different register address.
  - MAME (partially), MiSTer


# System ROMs
- Handheld Model: No System/Boot ROM
- CEFA Toys Super Quique Laptop Model: [Partial disassembly of the System ROM](https://github.com/bbbbbr/megaduck-quique-disasm/)
- Hartung Super Junior Computer: ...


# Porting from Game Boy to Mega Duck
Developing for the Mega Duck is mostly identical (cpu & integrated peripherals) to the Original Game Boy though it has a couple changes listed below.

Register and flag names will mostly follow those in the Game Boy dev `hardware.inc`, but may have some GBDK-isms.

Most of this research was done by others, I've added a small amount.

### Summary of Hardware changes versus the Game Boy:

Physical / Hardware:
  - Different cartridge pinout / connector
  - Different serial link port connector shape

Programming:
 - No Boot ROM
 - Cartridge Boot Logo: not present on Mega Duck
 - Cartridge Header data: not present on Mega Duck
   - Checksum header: not present on Mega Duck. **Do not apply checksum to ROM** after building as on the Game Boy
 - Program Entry Point: `0x0000` (on Game Boy: `0x0100` )
 - Initial registers
   - Handheld Models: (`AF, BC, DE, HL, SP`) are random at startup (due to lack of boot rom) with some affinity toward `0xFFFF` / `0x0000`
   - Laptop Model: Based on System ROM design (no stack init before first call/ret) it appears SP is NOT `0x0000` at power-on
     - Possibly it's something like 0xFFFE or lower which would allow pushing and popping the stack before init without a resulting crash
 - Serial control
   - Laptop Mode: Based on System ROM design and behavior it seems possible to use SC and SB reg outside normal GB guidelines (Sending still works when triggering SC to send **before** loading the send value into SB).
 - Display registers address and flag definitions: Some changed (details below)
 - VRAM data:
   - The user program should clear it before use.
   - For Handhelds: since a boot ROM does not run on startup it means Tile Map and Pattern data are not cleared and will have (consistent) random data.
    - For Laptop models: The System ROM will not clear VRAM before launching a user program from the system menu. The font patterns left in VRAM on program startup can be used to tell the difference between the Super Quique (Spanish) and Super Junior (German) laptop models. See [example code](https://github.com/bbbbbr/megaduck_laptop_gbdk_examples/blob/main/megaduck_keyboard/src/megaduck_model.c).
  - Audio registers address and flag definitions: Some changed (details below)
  - Different MBC bank switching register addresses than Game Boy MBCs

Laptop:
  - Built-in System ROM
  - Additional Cart Slot for add-on Memory Card (access not yet documented)
  - Peripherals attached via Serial/Link port
    - Keyboard + Piano Keys
    - RTC
    - Cart
    - Detached Gamepad
    - Mechanism to launch cartridges in the Cart Slot
    - External communication port for the printer (type not yet documented)

### Sound Register Value/Data Changes
These changes should be kept in mind when porting Sound Effects and Music Drivers written for the Game Boy.

1. Registers `NR12, NR22, NR42, and NR43` have their contents nybble swapped.
    - To maintain compatibility with the Game Boy the value to write (or the value read) can be converted this way: `((uint8_t)(value << 4) | (uint8_t)(value >> 4))`
2. Register `NR32` has the volume bit values changed.
    - `Game Boy:  Bits:6..5 : 00 = mute, 01 = 100%, 10 = 50%, 11 = 25%`
    - `Mega Duck: Bits:6..5 : 00 = mute, 01 = 25%,  10 = 50%, 11 = 100%`
    - To maintain compatibility witht he Game Boy the value to write (or the value read) can be converted this way: `(((~(uint8_t)value) + (uint8_t)0x20u) & (uint8_t)0x60u)`

### Sound Register Changes Table
- `Addr Change` means deviation from the expected linear incrementing register address order per sound channel that the Game Boy registers follow. The shuffled order on the Mega Duck can break assumptions in Game Boy sound drivers which attempt to write each channel as a sequential block using an incrementing register pointer.

| Reg  | Alt Name   | Game Boy | Mega Duck | Data Change        | Addr Change |
| ---- | ---------- | -------- | --------- | ------------------ | ----------- |
| NR10 | rAUD1SWEEP | 0xFF10   | 0xFF20    |                    |             |
| NR11 | rAUD1LEN   | 0xFF11   | 0xFF22    |                    | Addr +1     |
| NR12 | rAUD1ENV   | 0xFF12   | 0xFF21    | nybble swap        | Addr -1     |
| NR13 | rAUD1LOW   | 0xFF13   | 0xFF23    |                    |             |
| NR14 | rAUD1HIGH  | 0xFF14   | 0xFF24    |                    |             |
|      |            |          |           |                    |             |
| NR21 | rAUD2LEN   | 0xFF16   | 0xFF25    |                    | Addr -1     |
| NR22 | rAUD2ENV   | 0xFF17   | 0xFF27    | nybble swap        |             |
| NR23 | rAUD2LOW   | 0xFF18   | 0xFF28    |                    |             |
| NR24 | rAUD2HIGH  | 0xFF19   | 0xFF29    |                    |             |
|      |            |          |           |                    |             |
| NR30 | rAUD3ENA   | 0xFF1A   | 0xFF2A    |                    |             |
| NR31 | rAUD3LEN   | 0xFF1B   | 0xFF2B    |                    |             |
| NR32 | rAUD3LEVEL | 0xFF1C   | 0xFF2C    | volume bit swizzle |             |
| NR33 | rAUD3LOW   | 0xFF1D   | 0xFF2E    |                    | Addr +1     |
| NR34 | rAUD3HIGH  | 0xFF1E   | 0xFF2D    |                    | Addr -1     |
|      |            |          |           |                    |             |
| NR41 | rAUD4LEN   | 0xFF20   | 0xFF40    |                    |             |
| NR42 | rAUD4ENV   | 0xFF21   | 0xFF42    | nybble swap        | Addr +1     |
| NR43 | rAUD4POLY  | 0xFF22   | 0xFF41    | nybble swap        | Addr -1     |
| NR44 | rAUD4GO    | 0xFF23   | 0xFF43    |                    |             |
|      |            |          |           |                    |             |
| NR50 | rAUDVOL    | 0xFF24   | 0xFF44    |                    |             |
| NR51 | rAUDTERM   | 0xFF25   | 0xFF46    |                    | Addr +1     |
| NR52 | rAUDENA    | 0xFF26   | 0xFF45    |                    | Addr +1     |


### Graphics Register Bit Flag Changes

| LCDC Flag       | Game Boy | Mega Duck |        | Purpose                                          |
| --------------- | -------- | --------- | ------ | ------------------------------------------------ |
| LCDCF_B_ON      | .7       | .7        | (same) | Bit for LCD On/Off Select                        |
| LCDCF_B_WIN9C00 | .6       | .3        |        | Bit for Window Tile Map Region Select            |
| LCDCF_B_WINON   | .5       | .5        | (same) | Bit for Window Display On/Off Control            |
| LCDCF_B_BG8000  | .4       | .4        | (same) | Bit for BG & Window Tile Data Region Select      |
| LCDCF_B_BG9C00  | .3       | .2        |        | Bit for BG Tile Map Region Select                |
| LCDCF_B_OBJ16   | .2       | .1        |        | Bit for Sprites Size Select                      |
| LCDCF_B_OBJON   | .1       | .0        |        | Bit for Sprites Display Visible/Hidden Select    |
| LCDCF_B_BGON    | .0       | .6        |        | Bit for Background Display Visible Hidden Select |

### Graphics Register Address Changes

| Register | Game Boy | Mega Duck |
| -------- | -------- | --------- |
| LCDC     | 0xFF40   | 0xFF10    |
| STAT     | 0xFF41   | 0xFF11    |
| SCY      | 0xFF42   | 0xFF12    |
| SCX      | 0xFF43   | 0xFF13    |
| LY       | 0xFF44   | 0xFF18    |
| LYC      | 0xFF45   | 0xFF19    |
| DMA      | 0xFF46   | 0xFF1A    |
| BGP      | 0xFF47   | 0xFF1B    |
| OBP0     | 0xFF48   | 0xFF14    |
| OBP1     | 0xFF49   | 0xFF15    |
| WY       | 0xFF4A   | 0xFF16    |
| WX       | 0xFF4B   | 0xFF17    |

