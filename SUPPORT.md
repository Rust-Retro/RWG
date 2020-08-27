# Support for Rust on old iron

## By CPU / Architecture

This list is incomplete. Please help complete it!

| Vendor            | Microarchitecture | LLVM Arch       | Rust Target | Rustup Stdlib/Core | Comments                             |
|-------------------|-------------------|-----------------|-------------|--------------------|--------------------------------------|
| ARM               | ARMv2             | No              | No          | No                  | As used on Acorn Archimedes. Only has 26-bit pointers |
| ARM               | ARMv3             | No              | No          | No                  | As used on Acorn RiscPC. Supports 26-bit and 32-bit pointers. |
| ARM               | ArmV4T            | thumbv4t/armv4t | Yes         | No                 | e.g. ARM7TDMI in the Nintendo Game Boy Advance |
| ARM               | ArmV5TE           | armv5te         | Yes         | Yes                | e.g. ARM946E-S based Nintendo NTR in the Nintendo DS |
| ARM               | Armv6-M           | thumbv6m        | Yes         | Yes                | e.g. Cortex-M0 based microcontrollers |
| ARM               | Armv7-M           | thumbv7m        | Yes         | Yes                | e.g. Cortex-M3 based microcontrollers |
| ARM               | ArmV6             | arm/armv6       | Yes         | No                 | e.g. ARM11 based Broadcom BCM2835 in the Raspberry Pi Zero. (The LLVM architecture 'arm' seems to mean ArmV6) |
| ARM               | Armv7E-M          | thumbv7em       | Yes         | Yes                | e.g. Cortex-M4 and -M7 based microcontrollers |
| ARM               | ArmV7-R           | armv7r/armebv7r | Yes         | Yes                | 32-bit Real-time Processors. Used in hard-drives, etc. |
| ARM               | ArmV7-A           | thumbv7a/armv7/armv7a  | Yes  | Yes                | 32-bit Application Processors. e.g. Cortex-A8 based Apple A4 in the first-gen iPad |
| ARM               | Armv8-M.base      | thumbv8m.base   | Yes         | Yes                | e.g. Cortex-M23 based microcontrollers |
| ARM               | Armv8-M.main      | thumbv8m.main   | Yes         | Yes                | e.g. Cortex-M33 based microcontrollers |
| ARM               | Aarch64 (Armv8-A) | aarch64         | Yes         | Yes                | 64-bit Application Processors. e.g. Cortex-A72 based Broadcom BCM2711 SoC in the Raspberry Pi 4 |
| IBM               | S390x             | s390x           | Yes         | Yes                | IBM System/390 mainframes |
| IBM/Motorola      | PowerPC G1/G2/G3/G4| powerpc        | Yes         | Yes                | e.g. IBM PPC601 in the IBM RS6000, Motorola MPC603e in the Apple Power Macintosh, Motorola PowerPC 750 in the Apple iBook G3, IBM Gekko in the Nintendo GameCube, IBM Broadway in the Nintendo Wii, Motorola PowerPC 7400 in the Apple iBook G4 |
| IBM/Motorola      | PowerPC G5        | powerpc64/powerpc64le | Yes   | Yes                | e.g. IBM PowerPC 970 in the Apple Mac G5, IBM Cell in the PlayStation 3 |
| Intel             | Pentium           | i586            | Yes         | Yes                | e.g. Intel Pentium PC, AMD K5 PC, etc |
| Intel             | Pentium Pro       | i686            | Yes         | Yes                | e.g. Intel Pentium Pro PC, AMD K6 PC, etc |
| AMD/Intel         | AMD64             | x86_64          | Yes         | Yes                | Standard modern PC architecture used on all PCs since 2005 ish. |
| Microchip         | AVR               | avr             | Yes         | No                 | Atmel AVR-based microcontrollers, e.g. megaAVR, tinyAVR, etc. |
| MIPS              | MIPS I..V / MIPS32 / MIPS64  | mips/mipsel/mips64/mips64el | Yes | Yes | e.g. MIPS R3000 in the Sony PlayStation, MIPS R4000 in the SGI Indy, NEC VR4300 in the Nintendo 64, Sony Emotion Engine in the Sony Playstation 2 |
| MIPS              | MIPS 6            | mipsisa32r6/mipsisa32r6el/mipsisa64r6/mipsisa64r6el | Yes | No | e.g. Imagination M6250 (circa 2014) |
| nVidia            | PTX               | nvptx64         | Yes         | Yes                | nVidia PTX instruction set for Geforce GPUs |
| Qualcomm          | Hexagon           | hexagon         | Yes         | No                 | Qualcomm Snapdragon DSP |
| RISC-V            | RISC-V 32         | riscv32         | Yes         | Yes                | Range of 32-bit Microcontrollers and Microprocessors |
| RISC-V            | RISC-V 64         | riscv64         | Yes         | Yes                | Range of 64-bit Microcontrollers and Microprocessors |
| Sun/Oracle        | SPARC V8          | sparc           | Yes         | No                 | 32-bit. e.g. Sun SuperSPARC II in the Sun SPARCstation 20 |
| Sun/Oracle        | SPARC V9          | sparc64/sparcv9 | Yes         | Yes                | 64-bit. e.g. Sun UltraSPARC IIi in the Sun Ultra 10. LVM Arch is sparc9 for Solaris, and sparc64 for Linux/OpenBSD. |
| TexasInstruments  | MSP430            | msp430          | Yes         | No                 | Range of 16-bit Microcontrollers |
| DEC               | Alpha 21x64       | No              | No          | No                 | 64-bit only, e.g. the Alpha 21264 in the Digital DS25 workstation |
| Intel             | 80286             | No              | No          | No                 | As used on IBM PC AT. CPU compatible with 8086. Rust doesn't have segmented memory support |
| Intel             | 80386+            | No              | No          | No                 | CPU compatible with 80286 and 8086. Need to get into protected mode. Phil Opperman's blog OS manages this. |
| Intel             | 8080              | No              | No          | No                 | Zilog Z80 also runs Intel 8080 code |
| Intel             | 8086/8088         | No              | No          | No                 | As used on IBM PC and XT. Rust doesn't have segmented memory support |
| MOS               | 6502              | No              | No          | No                 | e.g. Commodore PET/VIC-20/C64, Apple I/II |
| Motorola          | 6800              | No              | No          | No                 | e.g. MITS Altair 680 |
| Motorola          | 6809              | No              | No          | No                 | Replaced the 6800. Has two stack pointers. e.g. Tandy TRS-80 |
| Motorola          | 68000             | No              | No          | No                 | e.g. Commodore Amiga, Atari ST, Apple Macintosh, SEGA Genesis, etc |
| Zilog             | Z80               | No              | No          | No                 | e.g. Sinclair ZX80/81/Spectrum, Amstrad CPC, MSX |


## By Operating System

This list is incomplete. Please help complete it!

| Vendor   | OS                   | Microarchitecture | Rust Support | Rustup std library  |
|----------|----------------------|-------------------|--------------|---------------------|
| Microsoft| DOS                  | x86               | No           | No                  |
| Microsoft| Windows 3.x          | x86               | No           | No                  |
| Microsoft| Windows 9x           | x86               | No           | No                  |
| Microsoft| Windows NT 3.x/4     | x86               | No           | No                  |
| Microsoft| Windows NT 3.x/4     | PowerPC           | No           | No                  |
| Microsoft| Windows NT 3.x/4     | MIPS              | No           | No                  |
| Microsoft| Windows NT 3.x/4     | Alpha             | No           | No                  |
| Microsoft| Windows 2000         | x86               | No           | No                  |
| Microsoft| Windows XP           | x86/x86_64        | No           | No                  |
| Apple    | System 1 .. System 7 | 68k               | No           | No                  |
| Apple    | Mac OS 8/9           | powerpc           | No           | No                  |
| Apple    | Mac OS X 10.0..10.4  | powerpc/powerpc64 | No           | No                  |
| Apple    | Mac OS X 10.5+       | x86/x86_64        | Yes          | Yes                 |
| Commodore| Amiga OS             | 68k               | No           | No                  |
| Acorn    | RISC OS 2            | ARM               | No           | No                  |
| Acorn    | RISC OS 3            | ARM               | No           | No                  |
| Element14| RISC OS 4            | ARM               | No           | No                  |
| Castle   | RISC OS 5            | 32-bit ARM        | No           | No                  |
| Castle   | RISC OS Six          | 32-bit ARM        | No           | No                  |
| Sun      | Solaris              | SPARC V8 and earlier | No        | No                  |
| Sun      | Solaris              | SPARC V9          | Yes          | Yes                 |
| Sun      | Solaris              | x86               | Yes          | Yes                 |
| NetBSD   | NetBSD               | x86               | Yes          | No                  |
| NetBSD   | NetBSD               | x86_64            | Yes          | Yes                 |
| NetBSD   | NetBSD               | powerpc           | Yes          | No                  |
| NetBSD   | NetBSD               | powerpc64         | Yes          | No                  |
| NetBSD   | NetBSD               | SPARC             | Yes          | No                  |
| Digital  | Tru64 UNIX           | Alpha             | No           | No                  |
| IBM      | OS/2                 | x86               | No           | No                  |
| FreeBSD  | FreeBSD              | AArch64           | Yes          | No                  |
| FreeBSD  | FreeBSD              | ArmV6             | Yes          | No                  |
| FreeBSD  | FreeBSD              | ArmV7             | Yes          | No                  |
| FreeBSD  | FreeBSD              | i686              | Yes          | Yes                 |
| FreeBSD  | FreeBSD              | powerpc64         | Yes          | No                  |
| FreeBSD  | FreeBSD              | x86_64            | Yes          | Yes                 |






