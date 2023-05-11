# Mega Duck Info
A collection of technical information and resources for the Mega Duck console.

## Software

### Emulators
- [MAME](https://www.mamedev.org/), [Arcade DB Entry](http://adb.arcadeitalia.net/dettaglio_mame.php?game_name=megaduck), [Cart list xml](https://github.com/mamedev/mame/blob/4a6c54dd5e4fc06ef535816fa6c2f4597d2f593f/hash/megaduck.xml#L4)
- [SameDuck](https://github.com/LIJI32/SameBoy/compare/SameDuck) branch of SameBoy (modified version of SameBoy, not pre-built)

### Development Tools
- [GBDK-2020](https://github.com/gbdk-2020/gbdk-2020): C dev kit, supports Mega Duck as a build target
- [hUGE Driver](https://github.com/bbbbbr/hUGEDriver): Port of this music driver to the Mega Duck
- CBTFX: Port of this sound effects driver to the Mega Duck

### Homebrew Games
- itch.io
- 

## Hardware

### Flash Carts
- A2 Heaven
- Inside Gadgets
- 3D Printable cartridge shell

#### LCD Header
#### Serial Link Port
#### Cartridge Pinout


## From Game Boy to Mega Duck / Cougar Boy
The Mega Duck is (for practical purposes) functionally identical to the Original Game Boy though it has a couple changes listed below.

### Summary of Hardware changes versus the Game Boy:
  - Cartridge Boot Logo: not present on Mega Duck
  - Cartridge Header data: not present on Mega Duck
    - Checksum header: not present on Mega Duck- do not apply after building as on the Game Boy
  - Program Entry Point: `0x0000` (on Game Boy: `0x0100` )
  - Display registers and flag definitions: Some changed
  - Audio registers and flag definitions: Some changed (See Soung Register Changes)
  - MBC ROM bank switching register address: `0x0001` (many Game Boy MBCs use `0x2000 - 0x3FFF`)


### Sound Register Value Changes
These changes should be kept in mind when porting Sound Effects and Music Drivers written for the Game Boy.

1. Registers NR12, NR22, NR42, and NR43 have their contents nybble swapped.
    - To maintain compatibility the value to write (or the value read) can be converted this way: `((uint8_t)(value << 4) | (uint8_t)(value >> 4))`
2. Register NR32 has the volume bit values changed.
    - `Game Boy:  Bits:6..5 : 00 = mute, 01 = 100%, 10 = 50%, 11 = 25%`
    - `Mega Duck: Bits:6..5 : 00 = mute, 01 = 25%,  10 = 50%, 11 = 100%`
    - To maintain compatibility the value to write (or the value read) can be converted this way: `(((~(uint8_t)value) + (uint8_t)0x20u) & (uint8_t)0x60u)`

### Graphics Register Bit Changes
These changes are handled automatically when their GBDK definitions are used.

| LCDC Flag   | Game Boy | Mega Duck |        | Purpose                                          |
| -------------------- | -------- | --------- | ------ | ------------------------------------------------ |
| LCDCF_B_ON      | .7       | .7        | (same) | Bit for LCD On/Off Select                        |
| LCDCF_B_WIN9C00 | .6       | .3        |        | Bit for Window Tile Map Region Select            |
| LCDCF_B_WINON   | .5       | .5        | (same) | Bit for Window Display On/Off Control            |
| LCDCF_B_BG8000  | .4       | .4        | (same) | Bit for BG & Window Tile Data Region Select      |
| LCDCF_B_BG9C00  | .3       | .2        |        | Bit for BG Tile Map Region Select                |
| LCDCF_B_OBJ16   | .2       | .1        |        | Bit for Sprites Size Select                      |
| LCDCF_B_OBJON   | .1       | .0        |        | Bit for Sprites Display Visible/Hidden Select    |
| LCDCF_B_BGON    | .0       | .6        |        | Bit for Background Display Visible Hidden Select |


### Detailed Register Address Changes
These changes are handled automatically when their GBDK definitions are used.

| Register      | Game Boy | Mega Duck |
| ------------- | -------- | --------- |
| LCDC | 0xFF40   | 0xFF10    |
| STAT | 0xFF41   | 0xFF11    |
| SCY  | 0xFF42   | 0xFF12    |
| SCX  | 0xFF43   | 0xFF13    |
| LY   | 0xFF44   | 0xFF18    |
| LYC  | 0xFF45   | 0xFF19    |
| DMA  | 0xFF46   | 0xFF1A    |
| BGP  | 0xFF47   | 0xFF1B    |
| OBP0 | 0xFF48   | 0xFF14    |
| OBP1 | 0xFF49   | 0xFF15    |
| WY   | 0xFF4A   | 0xFF16    |
| WX   | 0xFF4B   | 0xFF17    |
| -    | -        | -         |
| NR10 | 0xFF10   | 0xFF20    |
| NR11 | 0xFF11   | 0xFF22    |
| NR12 | 0xFF12   | 0xFF21    |
| NR13 | 0xFF13   | 0xFF23    |
| NR14 | 0xFF14   | 0xFF24    |
| -    | -        | -         |
| NR21 | 0xFF16   | 0xFF25    |
| NR22 | 0xFF17   | 0xFF27    |
| NR23 | 0xFF18   | 0xFF28    |
| NR24 | 0xFF19   | 0xFF29    |
| -    | -        | -         |
| NR30 | 0xFF1A   | 0xFF2A    |
| NR31 | 0xFF1B   | 0xFF2B    |
| NR32 | 0xFF1C   | 0xFF2C    |
| NR33 | 0xFF1D   | 0xFF2E    |
| NR34 | 0xFF1E   | 0xFF2D    |
| -    | -        | -         |
| NR41 | 0xFF20   | 0xFF40    |
| NR42 | 0xFF21   | 0xFF42    |
| NR43 | 0xFF22   | 0xFF41    |
| NR44 | 0xFF23   | 0xFF43    |
| -    | -        | -         |
| NR50 | 0xFF24   | 0xFF44    |
| NR51 | 0xFF25   | 0xFF46    |
| NR52 | 0xFF26   | 0xFF45    |
| -    | -        | -         |

```
        # Alt_name     Reg   Game Boy    Mega Duck Data-change   Addr-change
        . rAUD1SWEEP   NR10     0xFF10      0xFF20
        # rAUD1LEN     NR11     0xFF11      0xFF22               !! Addr +1
        * rAUD1ENV     NR12     0xFF12      0xFF21 * nybble swap !! Addr -1

        . rAUD1LOW     NR13     0xFF13      0xFF23
        . rAUD1HIGH    NR14     0xFF14      0xFF24
        -   -   -
        # rAUD2LEN     NR21     0xFF16      0xFF25               !! Addr -1
        * rAUD2ENV     NR22     0xFF17      0xFF27 * nybble swap

        . rAUD2LOW     NR23     0xFF18      0xFF28
        . rAUD2HIGH    NR24     0xFF19      0xFF29
        -   -   -
        . rAUD3ENA     NR30     0xFF1A      0xFF2A
        . rAUD3LEN     NR31     0xFF1B      0xFF2B
        - rAUD3LEVEL   NR32     0xFF1C      0xFF2C * volume bit swizzle

        # rAUD3LOW     NR33     0xFF1D      0xFF2E               !! Addr +1
        # rAUD3HIGH    NR34     0xFF1E      0xFF2D               !! Addr -1
        -   -   -
        . rAUD4LEN     NR41     0xFF20      0xFF40
        * rAUD4ENV     NR42     0xFF21      0xFF42 * nybble swap !! Addr +1
        * rAUD4POLY    NR43     0xFF22      0xFF41 * nybble swap !! Addr -1

        . rAUD4GO      NR44     0xFF23      0xFF43
        -   -   -
        .              NR50     0xFF24      0xFF44
        # rAUDTERM     NR51     0xFF25      0xFF46               !! Addr +1
        # rAUDENA      NR52     0xFF26      0xFF45               !! Addr +1
```
