# Support for Rust on old iron

## By CPU / Architecture

This list is incomplete. Please help complete it!

| Vendor   | Microarchitecture  | LLVM Backend | Rust out-of-tree target  | Rust in-tree target  | Comments/Issues   |
|----------|--------------------|--------------|--------------------------|----------------------|-------------------|
| ARM      | v2                 | No           | No                       | No                   | As used on Acorn Archimedes. Only has 26-bit pointers |
| ARM      | v3                 | No           | No                       | No                   | As used on Acorn RiscPC. Supports 26-bit and 32-bit pointers. |
| ARM      | v4                 | Yes          | Yes                      | Yes                  | As used on early ARM Linux boards and some consoles (e.g. ARM7). 32-bit pointers only. |
| ARM      | v6                 | Yes          | Yes                      | Yes                  | e.g. ARM9, ARM11 |
| DEC      | Alpha 21x64        | No           | No                       | No                   | 64-bit only |
| IBM/Motorola | PowerPC G1/G2/G3/G4| Yes          | Yes                      | Yes (Linux)          | e.g. IBM PPC601 in the IBM RS6000, Motorola MPC603e in the Apple Power Macintosh, Motorola PowerPC 750 in the Apple iBook G3, IBM Gekko in the Nintendo GameCube, IBM Broadway in the Nintendo Wii, Motorola PowerPC 7400 in the Apple iBook G4 |
| IBM      | PowerPC G5         | Yes          | Yes                      | Yes (Linux)          | e.g. IBM PowerPC 970 in the Apple Mac G5, IBM Cell in the PlayStation 3 |
| Intel    | 80286              | No           | No                       | No                   | As used on IBM PC AT. CPU compatible with 8086. Rust doesn't have segmented memory support |
| Intel    | 80386+             | Yes          | Yes                      | Yes                  | CPU compatible with 80286 and 8086. Need to get into protected mode. Phil Opperman's blog OS manages this. |
| Intel    | 8080               | No           | No                       | No                   | Zilog Z80 also runs Intel 8080 code |
| Intel    | 8088/86            | No           | No                       | No                   | As used on IBM PC and XT. Rust doesn't have segmented memory support |
| MIPS     | MIPS I/II/III/IV   | Yes          | Yes                      | Yes (Linux)          | e.g. MIPS R3000 in the Sony PlayStation, MIPS R4000 in the SGI Indy, NEC VR4300 in the Nintendo 64, Sony Emotion Engine in the Sony Playstation 2 |
| MOS      | 6502               | No           | No                       | No                   | e.g. Commodore PET/VIC-20/C64, Apple I/II |
| Motorola | 6800               | No           | No                       | No                   | e.g. MITS Altair 680 |
| Motorola | 68000              | No           | No                       | No                   | e.g. Commodore Amiga, Atari ST, Apple Macintosh, SEGA Genesis, etc |
| Motorola | 6809               | No           | No                       | No                   | Replaced the 6800. Has two stack pointers. e.g. Tandy TRS-80 |
| Sun      | SPARC V8 (SuperSPARC) | Yes       | Yes                      | Yes (Linux)          | 32-bit. e.g. Sun SuperSPARC II in the Sun SPARCstation 20 |
| Sun      | SPARC V9 (UltraSPARC) | Yes       | Yes                      | Yes (Linux, Solaris, BSD) | 64-bit. e.g. Sun UltraSPARC IIi in the Sun Ultra 10 |
| Zilog    | Z80                | No           | No                       | No                   | e.g. Sinclair ZX80/81/Spectrum, Amstrad CPC, MSX |

## By Operating System

This list is incomplete. Please help complete it!

| Vendor   | OS                 | Microarchitecture | Rust Support | Rustup std library  |
|----------|--------------------|-------------------|--------------|---------------------|
| Microsoft| DOS                | x86               | No           | No                  |
| Microsoft| Windows 9x         | x86               | No           | No                  |
| Microsoft| Windows NT 3.x/4   | x86/PowerPC/MIPS/Alpha | No      | No                  |
| Microsoft| Windows 2000       | x86               | No           | No                  |
| Microsoft| Windows XP         | x86               | No           | No                  |
| Apple    | System 1 .. System 7 | 68000           | No           | No                  |
| Apple    | Mac OS 8/9         | Power PC          | No           | No                  |
| Apple    | Mac OS X 10.0 .. 10.4 | Power PC       | No           | No                  |
| Sun      | Solaris            | x86               | Yes          | Yes                 |
| Sun      | Solaris            | SPARC V9          | Yes          | No                  |
| Sun      | Solaris            | SPARC V8 and earlier | No        | No                  |
| NetBSD   | NetBSD             | x86               | Yes          | No                  |
| NetBSD   | NetBSD             | PowerPC           | Yes          | No                  |
| NetBSD   | NetBSD             | PowerPC G5        | Yes          | No                  |
| NetBSD   | NetBSD             | SPARC             | Yes          | No                  |




