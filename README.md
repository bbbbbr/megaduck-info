# Mega Duck / Cougar Boy Console Info
A collection of technical information and resources for the Mega Duck console.

[Web version](https://bbbbbr.github.io/megaduck-info/)

# Software

### Emulators
- [MAME](https://www.mamedev.org/), [Arcade DB Entry](http://adb.arcadeitalia.net/dettaglio_mame.php?game_name=megaduck), [Cart list xml](https://github.com/mamedev/mame/blob/4a6c54dd5e4fc06ef535816fa6c2f4597d2f593f/hash/megaduck.xml#L4)
- [SameDuck](https://github.com/LIJI32/SameBoy/compare/SameDuck) branch of SameBoy (modified version of SameBoy, not pre-built)

### Development Tools
- [GBDK-2020](https://github.com/gbdk-2020/gbdk-2020): C dev kit, supports Mega Duck as a build target
- [Mega Duck port of the hUGE Driver](https://github.com/bbbbbr/hUGEDriver) Game Boy music driver
- [Mega Duck port of the CBTFX](https://github.com/bbbbbr/CBT-FX) Game Boy Sound FX driver

### Homebrew Games
- [Mega Duck games](https://itch.io/c/2884652/mega-duck-console-homebrew-roms) on itch.io

### ROM Patches
- [Patch](http://blog.rarit.ee/2023/02/puzzle-game-archeology-or-idiot-duck.html) for the Mega Duck Dice Block game to disable the timer
- [Patch](https://github.com/bbbbbr/megaduck-tetris-patch) for Game Boy Tetris so it runs on the Mega Duck

# Hardware

### Flash Cartridges
- [A2 Heaven multi-flash cart](http://www.a2heaven.com/webshop/index.php?rt=product/product&product_id=172)
- [Inside Gadgets 32K flash cart](https://shop.insidegadgets.com/product/megaduck-32kb-flash-cart/) - Compatible with [GBXCart flasher](https://www.gbxcart.com/)
- [3D Printable cartridge shell](https://github.com/bbbbbr/megaduck_cartridge_shell)

#### LCD Header
#### Serial Link Port
#### Cartridge Pinout


# Porting from Game Boy to Mega Duck
Programming for the Mega Duck is mostly identical (cpu & integrated peripherals) to the Original Game Boy though it has a couple changes listed below.

Register and flag names will mostly follow those in the Game Boy dev `hardware.inc`, but may have some GBDK-isms.

Most of this research was done by others, I've only added a small amount.

### Summary of Hardware changes versus the Game Boy:
  - Cartridge Boot Logo: not present on Mega Duck
  - Cartridge Header data: not present on Mega Duck
    - Checksum header: not present on Mega Duck. **Do not apply checksum to ROM** after building as on the Game Boy
  - Program Entry Point: `0x0000` (on Game Boy: `0x0100` )
  - Display registers address and flag definitions: Some changed (details below)
  - Audio registers address and flag definitions: Some changed (details below)
  - MBC ROM bank switching register address: `0x0001` (many Game Boy MBCs use `0x2000 - 0x3FFF`)


### Sound Register Value/Data Changes
These changes should be kept in mind when porting Sound Effects and Music Drivers written for the Game Boy.

1. Registers `NR12, NR22, NR42, and NR43` have their contents nybble swapped.
    - To maintain compatibility with the Game Boy the value to write (or the value read) can be converted this way: `((uint8_t)(value << 4) | (uint8_t)(value >> 4))`
2. Register `NR32` has the volume bit values changed.
    - `Game Boy:  Bits:6..5 : 00 = mute, 01 = 100%, 10 = 50%, 11 = 25%`
    - `Mega Duck: Bits:6..5 : 00 = mute, 01 = 25%,  10 = 50%, 11 = 100%`
    - To maintain compatibility witht he Game Boy the value to write (or the value read) can be converted this way: `(((~(uint8_t)value) + (uint8_t)0x20u) & (uint8_t)0x60u)`

### Table of Sound Register Changes
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

### Detailed Register Address Changes

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
