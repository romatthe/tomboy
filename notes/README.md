Screen: 66mm or 2.6" screen
CPU: 1MHz 8-bit CPU (though some say 4MHz?)
RAM: 8Kb
VRAM: 8Kb
Resolution: 160x144
Simultaneous colors: 4
Sprites/line: 10

DMG-CPU:
* CPU
* Interrupt controller
* Timer
* Memory
* Boot ROM
* Joypad Input
* Serial Data Transfer
* Sound Controller
* Pixel Processing Unit (PPU)

Used the Sharp LR35902 core
--> Feels like a mix between Intel 8080 and Z80
--> Z80 is strict superset of Intel 8080    
--> However, LR35902 does not support some Intel 8080 features, yet also support some Z80 features
--> In short, stripped down Intel 8080 feature-set plus some added Z80 features, plus some unique to 35902

Registers:

A    F
B    C
D    E
H    L
  SP
  PC
B&C, D&E and H&L can be combined to form 16-bit registeres (for example for pointers)

16-Bit registers: BC, DE, HL, SP
8-Bit registers: a, b, c, d, e, h, l
HL is a special case, the value pointed to by the address in HL can be used in place of any register

Flags:
- Zero
- N ?
- H ?
- Carry

## Interrupt model

The Game Boy jumps to fixed locations in (the beginning of) RAM

0000     rst $00 <-- Reset      |
0008     rst $08                |
0010     rst $10                |
0018     rst $18                | Software
0020     rst $20                | interrupts
0028     rst $28                |
0030     rst $30                |
0038     rst $38                |
0040     irq service routine #0
0048     irq service routine #1
0050     irq service routine #2
0058     irq service routine #3
0060     irq service routine #4

## Zero-Page

Zero page is not the lowest page in RAM, it's actually the topmost page in ram, so $FF00-$FFFF

## System Clocks

* CPU: 4MHz
* RAM: 1MHz
* PPU: 4MHz
* VRAM: 2MHz

That's actually not completely right, it's actually more like:
* CPU: 4,192,304Hz
* RAM: 1,048,576Hz
* PPU: 4,194,304Hz
* VRAM: 2,097,152Hz

## Memory Layout:

$0000: ROM
$8000: VRAM
$A000: External RAM
$C000: Internal RAM
$E000: Mirrors other things
$FE00: OAM RAM (Special purpose video RAM?)
$FEA0: Nothing
$FF00: I/O
$FF80: HRAM

If we look at the ROM we have avaiable, does this means games can only be 32Kb?
No, there is actually no real theoretical limit. Cartridges usually have largers ROM chips plus MBC (Memory Bank Controller) which can switch memory banks

Usually, this works like this:

At $0000, we have the upper 16Kb of ROM
At $4000, we have the 16Kb of ROM that is switched by the MBC

The same is true for external RAM, these can also be swapped in the space for External RAM in the address space.

There's also the Boot ROM at $0000-$00FF, which initializes the gameplay (famous intro screen and chime). This is built into the gameboy.
A game must ship with a copy of the Nintendo logo inside it's ROM. The gameplay then compares that to its own to determine legitimacy.

## ROM Header:

$0100-$0103 : Entry Point (Usually just a jump to go past the rest of the header)
$0104-$0133 : The Nintendo logo
$0134-$0143 : The Title
$013F-$0142 : Manufacturer Code
$0143       : CGB Flag
$0144-$0145 : New licensee code
$0146       : SGB Flag
$0147       : Cartridge type
$0148       : ROM Size
$0149       : RAM Size
$014A       : Destination Code
$014B       : Old Licensee code
$014C       : Mask Rom Version number
$014D       : Header Checksum
$014E-$014F : Global Checksum

## HRAM

See screenshots

## Joypad input

See screenshots

## Timer

See screenshots

## Interrupt controller

See schreenshots

## Sound Controller

See screenshots

## VRAM Memory Map

