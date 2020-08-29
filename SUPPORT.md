# Support for Rust on old iron

## Various levels of Rust CPU / Platform / OS support

### Host

These targets (CPU / Platform / OS combinations) can run `rustc` itself.

### Rustup stdlib / core

You can download a `libstd` or `libcore` for this target using `rustup target
add XXXX-YYY-ZZZ`, then compiler with `cargo --target=XXXX-YYY-ZZZ`.

### Built-in target

Rust knows about your target, and so you can compile for this target by
specifying `cargo +nightly run -Z build-std --target XXXX-YYY-ZZZ`.

### Out-of-tree target

LLVM can emit machine code for your CPU, but you must specify a JSON target
specification with `cargo +nightly run -Z build-std --target xxx.json`.

## Host compilers

These system can run the Rust compiler and Cargo.

Target                            | Notes                                               | Specific CPU targeted                     |
----------------------------------|-----------------------------------------------------|-------------------------------------------|
`aarch64-unknown-freebsd`         | ARM64 FreeBSD                                       | `generic`                                 |
`aarch64-unknown-linux-gnu`       | ARM64 Linux (kernel 4.2, glibc 2.17)                | `generic`                                 |
`aarch64-unknown-openbsd`         | ARM64 OpenBSD                                       | `generic`                                 |
`arm-unknown-linux-gnueabi`       | ARMv6 Linux (kernel 3.2, glibc 2.17)                | `generic, "+strict-align,+v6,+vfp2,-d32"` |
`arm-unknown-linux-gnueabihf`     | ARMv6 Linux, hardfloat (kernel 3.2, glibc 2.17)     | `generic, "+strict-align,+v6,+vfp2,-d32"` |
`armv6-unknown-freebsd`           | ARMv6 FreeBSD                                       | `generic, "+v6,+vfp2,-d32"`               |
`armv7-unknown-freebsd`           | ARMv7 FreeBSD                                       | `generic, "+v7,+vfp3,-d32,+thumb2,-neon"` |
`armv7-unknown-linux-gnueabihf`   | ARMv7 Linux, hardfloat (kernel 3.2, glibc 2.17)     | `generic, "+v7,+vfp3,-d32,+thumb2,-neon"` |
`i686-apple-darwin`               | 32-bit OSX (10.7+, Lion+)                           | `yonah`                                   |
`i686-pc-windows-gnu`             | 32-bit MinGW (Windows 7+)                           | `pentium4`                                |
`i686-pc-windows-msvc`            | 32-bit MSVC (Windows 7+)                            | `pentium4`                                |
`i686-unknown-freebsd`            | 32-bit FreeBSD                                      | `pentium4`                                |
`i686-unknown-haiku`              | 32-bit Haiku                                        | `pentium4`                                |
`i686-unknown-linux-gnu`          | 32-bit Linux (kernel 2.6.32+, glibc 2.11+)          | `pentium4`                                |
`i686-unknown-openbsd`            | 32-bit OpenBSD                                      | `pentium4`                                |
`mips-unknown-linux-gnu`          | MIPS Linux (kernel 4.4, glibc 2.23)                 | `mips32r2`                                |
`mips64-unknown-linux-gnuabi64`   | MIPS64 Linux, n64 ABI (kernel 4.4, glibc 2.23)      | `mips64r2`                                |
`mips64el-unknown-linux-gnuabi64` | MIPS64 (LE) Linux, n64 ABI (kernel 4.4, glibc 2.23) | `mips64r2`                                |
`mipsel-unknown-linux-gnu`        | MIPS (LE) Linux (kernel 4.4, glibc 2.23)            | `mips32r2`                                |
`powerpc-unknown-linux-gnu`       | PowerPC Linux (kernel 2.6.32, glibc 2.11)           | `generic`                                 |
`powerpc64-unknown-freebsd`       | PPC64 FreeBSD (ELFv1 and ELFv2)                     | `ppc64`                                   |
`powerpc64-unknown-linux-gnu`     | PPC64 Linux (kernel 2.6.32, glibc 2.11)             | `ppc64`                                   |
`powerpc64le-unknown-linux-gnu`   | PPC64LE Linux (kernel 3.10, glibc 2.17)             | `ppc64le`                                 |
`riscv64gc-unknown-linux-gnu`     | RISC-V Linux (kernel 4.20, glibc 2.29)              | `generic-rv64`                            |
`s390x-unknown-linux-gnu`         | S390x Linux (kernel 2.6.32, glibc 2.11)             | `z10`                                     |
`sparc64-unknown-netbsd`          | NetBSD/sparc64                                      | `v9`                                      |
`x86_64-apple-darwin`             | 64-bit OSX (10.7+, Lion+)                           | `core2`                                   |
`x86_64-pc-windows-gnu`           | 64-bit MinGW (Windows 7+)                           | `x86_64`                                  |
`x86_64-pc-windows-msvc`          | 64-bit MSVC (Windows 7+)                            | `x86_64`                                  |
`x86_64-unknown-dragonfly`        | 64-bit DragonFlyBSD                                 | `x86_64`                                  |
`x86_64-unknown-freebsd`          | 64-bit FreeBSD                                      | `x86_64`                                  |
`x86_64-unknown-haiku`            | 64-bit Haiku                                        | `x86_64`                                  |
`x86_64-unknown-illumos`          | illumos                                             | `x86_64`                                  |
`x86_64-unknown-linux-gnu`        | 64-bit Linux (kernel 2.6.32+, glibc 2.11+)          | `x86_64`                                  |
`x86_64-unknown-linux-musl`       | 64-bit Linux with MUSL                              | `x86_64`                                  |
`x86_64-unknown-netbsd`           | NetBSD/amd64                                        | `x86_64`                                  |
`x86_64-unknown-openbsd`          | 64-bit OpenBSD                                      | `x86_64`                                  |


## What CPU does each target support?

Here is a complete list of all the LLVM architectures and Processors
supported, along with which built-in Rust targets use that CPU. Note that in
most cases, newer CPUs in a given architecture are backwards compatible (e.g.
an `i686` Pentium Pro will run `i586` Pentium code just fine).

Unfortunately the processors are listed in alphabetical order rather than date order. PRs welcome to fix this!

It is unclear why some targets differ (e.g. `sparcv9-sun-solaris` vs
`sparc-unknown-linux`) when they target the same CPU (a SPARC V9). Also, the
`thumbXX-unknown-none-eabi` targets are really confusing, as Thumb is just an
instruction encoding for Arm supported by a range of CPUs.

| Architecture          | Processor              | Support     |
|-----------------------|------------------------|-------------|
| `aarch64`             | `a64fx`                | Out-of-tree |
|                       | `apple-a10`            | Out-of-tree |
|                       | `apple-a11`            | Out-of-tree |
|                       | `apple-a12`            | `aarch64-apple-darwin` |
|                       | `apple-a13`            | Out-of-tree |
|                       | `apple-a7`             | Out-of-tree |
|                       | `apple-a8`             | Out-of-tree |
|                       | `apple-a9`             | Out-of-tree |
|                       | `apple-latest`         | Out-of-tree |
|                       | `apple-s4`             | Out-of-tree |
|                       | `apple-s5`             | Out-of-tree |
|                       | `carmel`               | Out-of-tree |
|                       | `cortex-a34`           | Out-of-tree |
|                       | `cortex-a35`           | Out-of-tree |
|                       | `cortex-a53`           | Out-of-tree |
|                       | `cortex-a55`           | Out-of-tree |
|                       | `cortex-a57`           | Out-of-tree |
|                       | `cortex-a65`           | Out-of-tree |
|                       | `cortex-a65ae`         | Out-of-tree |
|                       | `cortex-a72`           | Out-of-tree |
|                       | `cortex-a73`           | Out-of-tree |
|                       | `cortex-a75`           | Out-of-tree |
|                       | `cortex-a76`           | Out-of-tree |
|                       | `cortex-a76ae`         | Out-of-tree |
|                       | `cortex-a77`           | Out-of-tree |
|                       | `cortex-a78`           | Out-of-tree |
|                       | `cortex-x1`            | Out-of-tree |
|                       | `cyclone`              | Out-of-tree |
|                       | `exynos-m3`            | Out-of-tree |
|                       | `exynos-m4`            | Out-of-tree |
|                       | `exynos-m5`            | Out-of-tree |
|                       | `falkor`               | Out-of-tree |
|                       | `generic`              | `aarch64-unknown-freebsd` `aarch64-unknown-linux-gnu` `aarch64-unknown-openbsd` |
|                       | `kryo`                 | Out-of-tree |
|                       | `neoverse-e1`          | Out-of-tree |
|                       | `neoverse-n1`          | Out-of-tree |
|                       | `saphira`              | Out-of-tree |
|                       | `thunderx`             | Out-of-tree |
|                       | `thunderx2t99`         | Out-of-tree |
|                       | `thunderx3t110`        | Out-of-tree |
|                       | `thunderxt81`          | Out-of-tree |
|                       | `thunderxt83`          | Out-of-tree |
|                       | `thunderxt88`          | Out-of-tree |
|                       | `tsv110`               | Out-of-tree |
| `arm`                 | `arm1020e`             | Out-of-tree |
|                       | `arm1020t`             | Out-of-tree |
|                       | `arm1022e`             | Out-of-tree |
|                       | `arm10e`               | Out-of-tree |
|                       | `arm10tdmi`            | Out-of-tree |
|                       | `arm1136j-s`           | Out-of-tree |
|                       | `arm1136jf-s`          | Out-of-tree |
|                       | `arm1156t2-s`          | Out-of-tree |
|                       | `arm1156t2f-s`         | Out-of-tree |
|                       | `arm1176j-s`           | Out-of-tree |
|                       | `arm1176jz-s`          | Out-of-tree |
|                       | `arm1176jzf-s`         | Out-of-tree |
|                       | `arm710t`              | Out-of-tree |
|                       | `arm720t`              | Out-of-tree |
|                       | `arm7tdmi`             | Out-of-tree |
|                       | `arm7tdmi-s`           | Out-of-tree |
|                       | `arm8`                 | Out-of-tree |
|                       | `arm810`               | Out-of-tree |
|                       | `arm9`                 | Out-of-tree |
|                       | `arm920`               | Out-of-tree |
|                       | `arm920t`              | Out-of-tree |
|                       | `arm922t`              | Out-of-tree |
|                       | `arm926ej-s`           | Out-of-tree |
|                       | `arm940t`              | Out-of-tree |
|                       | `arm946e-s`            | Out-of-tree |
|                       | `arm966e-s`            | Out-of-tree |
|                       | `arm968e-s`            | Out-of-tree |
|                       | `arm9e`                | Out-of-tree |
|                       | `arm9tdmi`             | Out-of-tree |
|                       | `cortex-a12`           | Out-of-tree |
|                       | `cortex-a15`           | Out-of-tree |
|                       | `cortex-a17`           | Out-of-tree |
|                       | `cortex-a32`           | Out-of-tree |
|                       | `cortex-a35`           | Out-of-tree |
|                       | `cortex-a5`            | Out-of-tree |
|                       | `cortex-a53`           | Out-of-tree |
|                       | `cortex-a55`           | Out-of-tree |
|                       | `cortex-a57`           | Out-of-tree |
|                       | `cortex-a7`            | Out-of-tree |
|                       | `cortex-a72`           | Out-of-tree |
|                       | `cortex-a73`           | Out-of-tree |
|                       | `cortex-a75`           | Out-of-tree |
|                       | `cortex-a76`           | Out-of-tree |
|                       | `cortex-a76ae`         | Out-of-tree |
|                       | `cortex-a77`           | Out-of-tree |
|                       | `cortex-a78`           | Out-of-tree |
|                       | `cortex-a8`            | `armv7-unknown-cloudabi-eabihf` |
|                       | `cortex-a9`            | Out-of-tree |
|                       | `cortex-m0`            | Out-of-tree |
|                       | `cortex-m0plus`        | Out-of-tree |
|                       | `cortex-m1`            | Out-of-tree |
|                       | `cortex-m23`           | Out-of-tree |
|                       | `cortex-m3`            | Out-of-tree |
|                       | `cortex-m33`           | Out-of-tree |
|                       | `cortex-m35p`          | Out-of-tree |
|                       | `cortex-m4`            | Out-of-tree |
|                       | `cortex-m55`           | Out-of-tree |
|                       | `cortex-m7`            | Out-of-tree |
|                       | `cortex-r4`            | Out-of-tree |
|                       | `cortex-r4f`           | Out-of-tree |
|                       | `cortex-r5`            | Out-of-tree |
|                       | `cortex-r52`           | Out-of-tree |
|                       | `cortex-r7`            | Out-of-tree |
|                       | `cortex-r8`            | Out-of-tree |
|                       | `cortex-x1`            | Out-of-tree |
|                       | `cyclone`              | Out-of-tree |
|                       | `ep9312`               | Out-of-tree |
|                       | `exynos-m3`            | Out-of-tree |
|                       | `exynos-m4`            | Out-of-tree |
|                       | `exynos-m5`            | Out-of-tree |
|                       | `generic`              | `arm-unknown-linux-gnueabi` (v6 or higher), `arm-unknown-linux-gnueabihf` (v6 or higher), `armv6-unknown-freebsd` (v6 or higher), `armv7-unknown-freebsd` (v7 or higher), `armv7-unknown-linux-gnueabihf` (v7 or higher) |
|                       | `iwmmxt`               | Out-of-tree |
|                       | `krait`                | Out-of-tree |
|                       | `kryo`                 | Out-of-tree |
|                       | `mpcore`               | Out-of-tree |
|                       | `mpcorenovfp`          | Out-of-tree |
|                       | `neoverse-n1`          | Out-of-tree |
|                       | `sc000`                | Out-of-tree |
|                       | `sc300`                | Out-of-tree |
|                       | `strongarm`            | Out-of-tree |
|                       | `strongarm110`         | Out-of-tree |
|                       | `strongarm1100`        | Out-of-tree |
|                       | `strongarm1110`        | Out-of-tree |
|                       | `swift`                | Out-of-tree |
|                       | `xscale`               | Out-of-tree |
| `avr`                 | `at43usb320`           | Out-of-tree |
|                       | `at43usb355`           | Out-of-tree |
|                       | `at76c711`             | Out-of-tree |
|                       | `at86rf401`            | Out-of-tree |
|                       | `at90c8534`            | Out-of-tree |
|                       | `at90can128`           | Out-of-tree |
|                       | `at90can32`            | Out-of-tree |
|                       | `at90can64`            | Out-of-tree |
|                       | `at90pwm1`             | Out-of-tree |
|                       | `at90pwm161`           | Out-of-tree |
|                       | `at90pwm2`             | Out-of-tree |
|                       | `at90pwm216`           | Out-of-tree |
|                       | `at90pwm2b`            | Out-of-tree |
|                       | `at90pwm3`             | Out-of-tree |
|                       | `at90pwm316`           | Out-of-tree |
|                       | `at90pwm3b`            | Out-of-tree |
|                       | `at90pwm81`            | Out-of-tree |
|                       | `at90s1200`            | Out-of-tree |
|                       | `at90s2313`            | Out-of-tree |
|                       | `at90s2323`            | Out-of-tree |
|                       | `at90s2333`            | Out-of-tree |
|                       | `at90s2343`            | Out-of-tree |
|                       | `at90s4414`            | Out-of-tree |
|                       | `at90s4433`            | Out-of-tree |
|                       | `at90s4434`            | Out-of-tree |
|                       | `at90s8515`            | Out-of-tree |
|                       | `at90s8535`            | Out-of-tree |
|                       | `at90scr100`           | Out-of-tree |
|                       | `at90usb1286`          | Out-of-tree |
|                       | `at90usb1287`          | Out-of-tree |
|                       | `at90usb162`           | Out-of-tree |
|                       | `at90usb646`           | Out-of-tree |
|                       | `at90usb647`           | Out-of-tree |
|                       | `at90usb82`            | Out-of-tree |
|                       | `at94k`                | Out-of-tree |
|                       | `ata5272`              | Out-of-tree |
|                       | `ata5505`              | Out-of-tree |
|                       | `ata5790`              | Out-of-tree |
|                       | `ata5795`              | Out-of-tree |
|                       | `ata6285`              | Out-of-tree |
|                       | `ata6286`              | Out-of-tree |
|                       | `ata6289`              | Out-of-tree |
|                       | `atmega103`            | Out-of-tree |
|                       | `atmega128`            | Out-of-tree |
|                       | `atmega1280`           | Out-of-tree |
|                       | `atmega1281`           | Out-of-tree |
|                       | `atmega1284`           | Out-of-tree |
|                       | `atmega1284p`          | Out-of-tree |
|                       | `atmega1284rfr2`       | Out-of-tree |
|                       | `atmega128a`           | Out-of-tree |
|                       | `atmega128rfa1`        | Out-of-tree |
|                       | `atmega128rfr2`        | Out-of-tree |
|                       | `atmega16`             | Out-of-tree |
|                       | `atmega161`            | Out-of-tree |
|                       | `atmega162`            | Out-of-tree |
|                       | `atmega163`            | Out-of-tree |
|                       | `atmega164a`           | Out-of-tree |
|                       | `atmega164p`           | Out-of-tree |
|                       | `atmega164pa`          | Out-of-tree |
|                       | `atmega165`            | Out-of-tree |
|                       | `atmega165a`           | Out-of-tree |
|                       | `atmega165p`           | Out-of-tree |
|                       | `atmega165pa`          | Out-of-tree |
|                       | `atmega168`            | Out-of-tree |
|                       | `atmega168a`           | Out-of-tree |
|                       | `atmega168p`           | Out-of-tree |
|                       | `atmega168pa`          | Out-of-tree |
|                       | `atmega169`            | Out-of-tree |
|                       | `atmega169a`           | Out-of-tree |
|                       | `atmega169p`           | Out-of-tree |
|                       | `atmega169pa`          | Out-of-tree |
|                       | `atmega16a`            | Out-of-tree |
|                       | `atmega16hva`          | Out-of-tree |
|                       | `atmega16hva2`         | Out-of-tree |
|                       | `atmega16hvb`          | Out-of-tree |
|                       | `atmega16hvbrevb`      | Out-of-tree |
|                       | `atmega16m1`           | Out-of-tree |
|                       | `atmega16u2`           | Out-of-tree |
|                       | `atmega16u4`           | Out-of-tree |
|                       | `atmega2560`           | Out-of-tree |
|                       | `atmega2561`           | Out-of-tree |
|                       | `atmega2564rfr2`       | Out-of-tree |
|                       | `atmega256rfr2`        | Out-of-tree |
|                       | `atmega32`             | Out-of-tree |
|                       | `atmega323`            | Out-of-tree |
|                       | `atmega324a`           | Out-of-tree |
|                       | `atmega324p`           | Out-of-tree |
|                       | `atmega324pa`          | Out-of-tree |
|                       | `atmega325`            | Out-of-tree |
|                       | `atmega3250`           | Out-of-tree |
|                       | `atmega3250a`          | Out-of-tree |
|                       | `atmega3250p`          | Out-of-tree |
|                       | `atmega3250pa`         | Out-of-tree |
|                       | `atmega325a`           | Out-of-tree |
|                       | `atmega325p`           | Out-of-tree |
|                       | `atmega325pa`          | Out-of-tree |
|                       | `atmega328`            | Out-of-tree |
|                       | `atmega328p`           | Out-of-tree |
|                       | `atmega329`            | Out-of-tree |
|                       | `atmega3290`           | Out-of-tree |
|                       | `atmega3290a`          | Out-of-tree |
|                       | `atmega3290p`          | Out-of-tree |
|                       | `atmega3290pa`         | Out-of-tree |
|                       | `atmega329a`           | Out-of-tree |
|                       | `atmega329p`           | Out-of-tree |
|                       | `atmega329pa`          | Out-of-tree |
|                       | `atmega32a`            | Out-of-tree |
|                       | `atmega32c1`           | Out-of-tree |
|                       | `atmega32hvb`          | Out-of-tree |
|                       | `atmega32hvbrevb`      | Out-of-tree |
|                       | `atmega32m1`           | Out-of-tree |
|                       | `atmega32u2`           | Out-of-tree |
|                       | `atmega32u4`           | Out-of-tree |
|                       | `atmega32u6`           | Out-of-tree |
|                       | `atmega406`            | Out-of-tree |
|                       | `atmega48`             | Out-of-tree |
|                       | `atmega48a`            | Out-of-tree |
|                       | `atmega48p`            | Out-of-tree |
|                       | `atmega48pa`           | Out-of-tree |
|                       | `atmega64`             | Out-of-tree |
|                       | `atmega640`            | Out-of-tree |
|                       | `atmega644`            | Out-of-tree |
|                       | `atmega644a`           | Out-of-tree |
|                       | `atmega644p`           | Out-of-tree |
|                       | `atmega644pa`          | Out-of-tree |
|                       | `atmega644rfr2`        | Out-of-tree |
|                       | `atmega645`            | Out-of-tree |
|                       | `atmega6450`           | Out-of-tree |
|                       | `atmega6450a`          | Out-of-tree |
|                       | `atmega6450p`          | Out-of-tree |
|                       | `atmega645a`           | Out-of-tree |
|                       | `atmega645p`           | Out-of-tree |
|                       | `atmega649`            | Out-of-tree |
|                       | `atmega6490`           | Out-of-tree |
|                       | `atmega6490a`          | Out-of-tree |
|                       | `atmega6490p`          | Out-of-tree |
|                       | `atmega649a`           | Out-of-tree |
|                       | `atmega649p`           | Out-of-tree |
|                       | `atmega64a`            | Out-of-tree |
|                       | `atmega64c1`           | Out-of-tree |
|                       | `atmega64hve`          | Out-of-tree |
|                       | `atmega64m1`           | Out-of-tree |
|                       | `atmega64rfr2`         | Out-of-tree |
|                       | `atmega8`              | Out-of-tree |
|                       | `atmega8515`           | Out-of-tree |
|                       | `atmega8535`           | Out-of-tree |
|                       | `atmega88`             | Out-of-tree |
|                       | `atmega88a`            | Out-of-tree |
|                       | `atmega88p`            | Out-of-tree |
|                       | `atmega88pa`           | Out-of-tree |
|                       | `atmega8a`             | Out-of-tree |
|                       | `atmega8hva`           | Out-of-tree |
|                       | `atmega8u2`            | Out-of-tree |
|                       | `attiny10`             | Out-of-tree |
|                       | `attiny102`            | Out-of-tree |
|                       | `attiny104`            | Out-of-tree |
|                       | `attiny11`             | Out-of-tree |
|                       | `attiny12`             | Out-of-tree |
|                       | `attiny13`             | Out-of-tree |
|                       | `attiny13a`            | Out-of-tree |
|                       | `attiny15`             | Out-of-tree |
|                       | `attiny1634`           | Out-of-tree |
|                       | `attiny167`            | Out-of-tree |
|                       | `attiny20`             | Out-of-tree |
|                       | `attiny22`             | Out-of-tree |
|                       | `attiny2313`           | Out-of-tree |
|                       | `attiny2313a`          | Out-of-tree |
|                       | `attiny24`             | Out-of-tree |
|                       | `attiny24a`            | Out-of-tree |
|                       | `attiny25`             | Out-of-tree |
|                       | `attiny26`             | Out-of-tree |
|                       | `attiny261`            | Out-of-tree |
|                       | `attiny261a`           | Out-of-tree |
|                       | `attiny28`             | Out-of-tree |
|                       | `attiny4`              | Out-of-tree |
|                       | `attiny40`             | Out-of-tree |
|                       | `attiny4313`           | Out-of-tree |
|                       | `attiny43u`            | Out-of-tree |
|                       | `attiny44`             | Out-of-tree |
|                       | `attiny44a`            | Out-of-tree |
|                       | `attiny45`             | Out-of-tree |
|                       | `attiny461`            | Out-of-tree |
|                       | `attiny461a`           | Out-of-tree |
|                       | `attiny48`             | Out-of-tree |
|                       | `attiny5`              | Out-of-tree |
|                       | `attiny828`            | Out-of-tree |
|                       | `attiny84`             | Out-of-tree |
|                       | `attiny84a`            | Out-of-tree |
|                       | `attiny85`             | Out-of-tree |
|                       | `attiny861`            | Out-of-tree |
|                       | `attiny861a`           | Out-of-tree |
|                       | `attiny87`             | Out-of-tree |
|                       | `attiny88`             | Out-of-tree |
|                       | `attiny9`              | Out-of-tree |
|                       | `atxmega128a1`         | Out-of-tree |
|                       | `atxmega128a1u`        | Out-of-tree |
|                       | `atxmega128a3`         | Out-of-tree |
|                       | `atxmega128a3u`        | Out-of-tree |
|                       | `atxmega128a4u`        | Out-of-tree |
|                       | `atxmega128b1`         | Out-of-tree |
|                       | `atxmega128b3`         | Out-of-tree |
|                       | `atxmega128c3`         | Out-of-tree |
|                       | `atxmega128d3`         | Out-of-tree |
|                       | `atxmega128d4`         | Out-of-tree |
|                       | `atxmega16a4`          | Out-of-tree |
|                       | `atxmega16a4u`         | Out-of-tree |
|                       | `atxmega16c4`          | Out-of-tree |
|                       | `atxmega16d4`          | Out-of-tree |
|                       | `atxmega16e5`          | Out-of-tree |
|                       | `atxmega192a3`         | Out-of-tree |
|                       | `atxmega192a3u`        | Out-of-tree |
|                       | `atxmega192c3`         | Out-of-tree |
|                       | `atxmega192d3`         | Out-of-tree |
|                       | `atxmega256a3`         | Out-of-tree |
|                       | `atxmega256a3b`        | Out-of-tree |
|                       | `atxmega256a3bu`       | Out-of-tree |
|                       | `atxmega256a3u`        | Out-of-tree |
|                       | `atxmega256c3`         | Out-of-tree |
|                       | `atxmega256d3`         | Out-of-tree |
|                       | `atxmega32a4`          | Out-of-tree |
|                       | `atxmega32a4u`         | Out-of-tree |
|                       | `atxmega32c4`          | Out-of-tree |
|                       | `atxmega32d4`          | Out-of-tree |
|                       | `atxmega32e5`          | Out-of-tree |
|                       | `atxmega32x1`          | Out-of-tree |
|                       | `atxmega384c3`         | Out-of-tree |
|                       | `atxmega384d3`         | Out-of-tree |
|                       | `atxmega64a1`          | Out-of-tree |
|                       | `atxmega64a1u`         | Out-of-tree |
|                       | `atxmega64a3`          | Out-of-tree |
|                       | `atxmega64a3u`         | Out-of-tree |
|                       | `atxmega64a4u`         | Out-of-tree |
|                       | `atxmega64b1`          | Out-of-tree |
|                       | `atxmega64b3`          | Out-of-tree |
|                       | `atxmega64c3`          | Out-of-tree |
|                       | `atxmega64d3`          | Out-of-tree |
|                       | `atxmega64d4`          | Out-of-tree |
|                       | `atxmega8e5`           | Out-of-tree |
|                       | `avr1`                 | Out-of-tree |
|                       | `avr2`                 | Out-of-tree |
|                       | `avr25`                | Out-of-tree |
|                       | `avr3`                 | Out-of-tree |
|                       | `avr31`                | Out-of-tree |
|                       | `avr35`                | Out-of-tree |
|                       | `avr4`                 | Out-of-tree |
|                       | `avr5`                 | Out-of-tree |
|                       | `avr51`                | Out-of-tree |
|                       | `avr6`                 | Out-of-tree |
|                       | `avrtiny`              | Out-of-tree |
|                       | `avrxmega1`            | Out-of-tree |
|                       | `avrxmega2`            | Out-of-tree |
|                       | `avrxmega3`            | Out-of-tree |
|                       | `avrxmega4`            | Out-of-tree |
|                       | `avrxmega5`            | Out-of-tree |
|                       | `avrxmega6`            | Out-of-tree |
|                       | `avrxmega7`            | Out-of-tree |
|                       | `m3000`                | Out-of-tree |
| `hexagon`             | `generic`              | Out-of-tree |
|                       | `hexagonv5`            | Out-of-tree |
|                       | `hexagonv55`           | Out-of-tree |
|                       | `hexagonv60`           | `hexagon-unknown-linux-musl` |
|                       | `hexagonv62`           | Out-of-tree |
|                       | `hexagonv65`           | Out-of-tree |
|                       | `hexagonv66`           | Out-of-tree |
|                       | `hexagonv67`           | Out-of-tree |
|                       | `hexagonv67t`          | Out-of-tree |
| `mips`/`mips64`       | `generic`              | Out-of-tree |
|                       | `mips1`                | Out-of-tree |
|                       | `mips2`                | `mipsel-sony-psp` |
|                       | `mips3`                | Out-of-tree |
|                       | `mips32`               | Out-of-tree |
|                       | `mips32r2`             | `mips-unknown-linux-gnu` `mips-unknown-linux-musl` `mips-unknown-linux-uclibc` `mipsel-unknown-linux-gnu` `mipsel-unknown-linux-musl` `mipsel-unknown-linux-uclibc` |
|                       | `mips32r3`             | Out-of-tree |
|                       | `mips32r5`             | Out-of-tree |
|                       | `mips32r6`             | `mipsisa32r6-unknown-linux-gnu` `mipsisa32r6el-unknown-linux-gnu` |
|                       | `mips4`                | Out-of-tree |
|                       | `mips5`                | Out-of-tree |
|                       | `mips64`               | Out-of-tree |
|                       | `mips64r2`             | `mips64-unknown-linux-gnuabi64` `mips64-unknown-linux-muslabi64` `mips64el-unknown-linux-gnuabi64` `mips64el-unknown-linux-muslabi64` |
|                       | `mips64r3`             | Out-of-tree |
|                       | `mips64r5`             | Out-of-tree |
|                       | `mips64r6`             | `mipsisa64r6-unknown-linux-gnuabi64` `mipsisa64r6el-unknown-linux-gnuabi64` |
|                       | `octeon`               | Out-of-tree |
|                       | `octeon`               | Out-of-tree |
|                       | `p5600`                | Out-of-tree |
| `msp430`              | `generic`              | Out-of-tree |
|                       | `msp430`               | Out-of-tree |
|                       | `msp430x`              | Out-of-tree |
| `nvptx64`             | `sm_20`                | Out-of-tree |
|                       | `sm_21`                | Out-of-tree |
|                       | `sm_30`                | `nvptx64-nvidia-cuda` |
|                       | `sm_32`                | Out-of-tree |
|                       | `sm_35`                | Out-of-tree |
|                       | `sm_37`                | Out-of-tree |
|                       | `sm_50`                | Out-of-tree |
|                       | `sm_52`                | Out-of-tree |
|                       | `sm_53`                | Out-of-tree |
|                       | `sm_60`                | Out-of-tree |
|                       | `sm_61`                | Out-of-tree |
|                       | `sm_62`                | Out-of-tree |
|                       | `sm_70`                | Out-of-tree |
|                       | `sm_72`                | Out-of-tree |
|                       | `sm_75`                | Out-of-tree |
|                       | `sm_80`                | Out-of-tree |
| `powerpc`/`powerpc64` | `440`                  | Out-of-tree |
|                       | `450`                  | Out-of-tree |
|                       | `601`                  | Out-of-tree |
|                       | `602`                  | Out-of-tree |
|                       | `603`                  | Out-of-tree |
|                       | `603e`                 | Out-of-tree |
|                       | `603ev`                | Out-of-tree |
|                       | `604`                  | Out-of-tree |
|                       | `604e`                 | Out-of-tree |
|                       | `620`                  | Out-of-tree |
|                       | `7400`                 | Out-of-tree |
|                       | `7450`                 | Out-of-tree |
|                       | `750`                  | Out-of-tree |
|                       | `970`                  | Out-of-tree |
|                       | `a2`                   | Out-of-tree |
|                       | `a2q`                  | Out-of-tree |
|                       | `e500`                 | Out-of-tree |
|                       | `e500mc`               | Out-of-tree |
|                       | `e5500`                | Out-of-tree |
|                       | `future`               | Out-of-tree |
|                       | `g3`                   | Out-of-tree |
|                       | `g4`                   | Out-of-tree |
|                       | `g4`                   | Out-of-tree |
|                       | `g5`                   | Out-of-tree |
|                       | `generic`              | Out-of-tree |
|                       | `ppc`                  | `powerpc-wrs-vxworks` `powerpc-unknown-linux` `powerpc-unknown-netbsd` |
|                       | `ppc32`                | Out-of-tree |
|                       | `ppc64`                | `powerpc64-unknown-freebsd` `powerpc64-unknown-linux-gnu` `powerpc64-unknown-linux-musl` `powerpc64-wrs-vxworks` |
|                       | `ppc64le`              | `powerpc64le-unknown-linux-gnu` `powerpc64le-unknown-linux-musl` |
|                       | `pwr10`                | Out-of-tree |
|                       | `pwr3`                 | Out-of-tree |
|                       | `pwr4`                 | Out-of-tree |
|                       | `pwr5`                 | Out-of-tree |
|                       | `pwr5x`                | Out-of-tree |
|                       | `pwr6`                 | Out-of-tree |
|                       | `pwr6x`                | Out-of-tree |
|                       | `pwr7`                 | Out-of-tree |
|                       | `pwr8`                 | Out-of-tree |
|                       | `pwr9`                 | Out-of-tree |
| `riscv32` / `riscv64` | `generic-rv32`         | `riscv32i-unknown-none-elf` `riscv32imac-unknown-none-elf` `riscv32imc-unknown-none-elf` |
|                       | `generic-rv64`         | `riscv64gc-unknown-linux-gnu` `riscv64gc-unknown-none-elf` `riscv64imac-unknown-none-elf` |
|                       | `rocket-rv32`          | Out-of-tree |
|                       | `rocket-rv64`          | Out-of-tree |
|                       | `sifive-e31`           | Out-of-tree |
|                       | `sifive-u54`           | Out-of-tree |
| `s390x`               | `arch10`               | Out-of-tree |
|                       | `arch11`               | Out-of-tree |
|                       | `arch12`               | Out-of-tree |
|                       | `arch13`               | Out-of-tree |
|                       | `arch8`                | Out-of-tree |
|                       | `arch9`                | Out-of-tree |
|                       | `generic`              | Out-of-tree |
|                       | `z10`                  | `s390x-unknown-linux-gnu` |
|                       | `z13`                  | Out-of-tree |
|                       | `z14`                  | Out-of-tree |
|                       | `z15`                  | Out-of-tree |
|                       | `z196`                 | Out-of-tree |
|                       | `zEC12`                | Out-of-tree |
| `sparc`/`sparc64`     | `at697e`               | Out-of-tree |
|                       | `at697f`               | Out-of-tree |
|                       | `f934`                 | Out-of-tree |
|                       | `generic`              | Out-of-tree |
|                       | `gr712rc`              | Out-of-tree |
|                       | `gr740`                | Out-of-tree |
|                       | `hypersparc`           | Out-of-tree |
|                       | `leon2`                | Out-of-tree |
|                       | `leon3`                | Out-of-tree |
|                       | `leon4`                | Out-of-tree |
|                       | `ma2080`               | Out-of-tree |
|                       | `ma2085`               | Out-of-tree |
|                       | `ma2100`               | Out-of-tree |
|                       | `ma2150`               | Out-of-tree |
|                       | `ma2155`               | Out-of-tree |
|                       | `ma2450`               | Out-of-tree |
|                       | `ma2455`               | Out-of-tree |
|                       | `ma2480`               | Out-of-tree |
|                       | `ma2485`               | Out-of-tree |
|                       | `ma2x5x`               | Out-of-tree |
|                       | `ma2x8x`               | Out-of-tree |
|                       | `myriad2`              | Out-of-tree |
|                       | `myriad2.1`            | Out-of-tree |
|                       | `myriad2.2`            | Out-of-tree |
|                       | `myriad2.3`            | Out-of-tree |
|                       | `niagara`              | Out-of-tree |
|                       | `niagara2`             | Out-of-tree |
|                       | `niagara3`             | Out-of-tree |
|                       | `niagara4`             | Out-of-tree |
|                       | `sparclet`             | Out-of-tree |
|                       | `sparclite`            | Out-of-tree |
|                       | `sparclite86x`         | Out-of-tree |
|                       | `supersparc`           | Out-of-tree |
|                       | `tsc701`               | Out-of-tree |
|                       | `ultrasparc`           | Out-of-tree |
|                       | `ultrasparc3`          | Out-of-tree |
|                       | `ut699`                | Out-of-tree |
|                       | `v7`                   | Out-of-tree |
|                       | `v8`                   | Out-of-tree |
|                       | `v9`                   | `sparc-unknown-linux-gnu` `sparc64-unknown-linux-gnu` `sparc64-unknown-netbsd` `sparc64-unknown-openbsd` `sparcv9-sun-solaris` |
| `x86`                 | `amdfam10`             | Out-of-tree |
|                       | `athlon`               | Out-of-tree |
|                       | `athlon-4`             | Out-of-tree |
|                       | `athlon-fx`            | Out-of-tree |
|                       | `athlon-mp`            | Out-of-tree |
|                       | `athlon-tbird`         | Out-of-tree |
|                       | `athlon-xp`            | Out-of-tree |
|                       | `athlon64`             | Out-of-tree |
|                       | `athlon64-sse3`        | Out-of-tree |
|                       | `atom`                 | Out-of-tree |
|                       | `barcelona`            | Out-of-tree |
|                       | `bdver1`               | Out-of-tree |
|                       | `bdver2`               | Out-of-tree |
|                       | `bdver3`               | Out-of-tree |
|                       | `bdver4`               | Out-of-tree |
|                       | `bonnell`              | Out-of-tree |
|                       | `broadwell`            | Out-of-tree |
|                       | `btver1`               | Out-of-tree |
|                       | `btver2`               | Out-of-tree |
|                       | `c3`                   | Out-of-tree |
|                       | `c3-2`                 | Out-of-tree |
|                       | `cannonlake`           | Out-of-tree |
|                       | `cascadelake`          | Out-of-tree |
|                       | `cooperlake`           | Out-of-tree |
|                       | `core-avx-i`           | Out-of-tree |
|                       | `core-avx2`            | Out-of-tree |
|                       | `core2`                | `x86_64-apple-darwin` |
|                       | `corei7`               | Out-of-tree |
|                       | `corei7-avx`           | Out-of-tree |
|                       | `generic`              | Out-of-tree |
|                       | `geode`                | Out-of-tree |
|                       | `goldmont`             | Out-of-tree |
|                       | `goldmont-plus`        | Out-of-tree |
|                       | `haswell`              | Out-of-tree |
|                       | `i386`                 | Out-of-tree |
|                       | `i486`                 | Out-of-tree |
|                       | `i586`                 | Out-of-tree |
|                       | `i686`                 | Out-of-tree |
|                       | `icelake-client`       | Out-of-tree |
|                       | `icelake-server`       | Out-of-tree |
|                       | `ivybridge`            | Out-of-tree |
|                       | `k6`                   | Out-of-tree |
|                       | `k6-2`                 | Out-of-tree |
|                       | `k6-3`                 | Out-of-tree |
|                       | `k8`                   | Out-of-tree |
|                       | `k8-sse3`              | Out-of-tree |
|                       | `knl`                  | Out-of-tree |
|                       | `knm`                  | Out-of-tree |
|                       | `lakemont`             | Out-of-tree |
|                       | `nehalem`              | Out-of-tree |
|                       | `nocona`               | Out-of-tree |
|                       | `opteron`              | Out-of-tree |
|                       | `opteron-sse3`         | Out-of-tree |
|                       | `penryn`               | Out-of-tree |
|                       | `pentium`              | `i586-pc-windows-msvc` `i586-unknown-linux-gnu` `i586-unknown-linux-musl` |
|                       | `pentium-m`            | Out-of-tree |
|                       | `pentium-mmx`          | Out-of-tree |
|                       | `pentium2`             | Out-of-tree |
|                       | `pentium3`             | Out-of-tree |
|                       | `pentium3m`            | Out-of-tree |
|                       | `pentium4`             | `i686-pc-windows-gnu` `i686-pc-windows-msvc` `i686-unknown-cloudabi` `i686-unknown-freebsd` `i686-unknown-haiku` `i686-unknown-linux-gnu` `i686-unknown-linux-musl` `i686-unknown-netbsd` `i686-unknown-openbsd` `i686-unknown-uefi` `i686-uwp-windows-gnu` `i686-uwp-windows-msvc` `i686-wrs-vxworks` |
|                       | `pentium4m`            | Out-of-tree |
|                       | `pentiumpro`           | `i686-linux-android` |
|                       | `prescott`             | Out-of-tree |
|                       | `sandybridge`          | Out-of-tree |
|                       | `silvermont`           | Out-of-tree |
|                       | `skx`                  | Out-of-tree |
|                       | `skylake`              | Out-of-tree |
|                       | `skylake-avx512`       | Out-of-tree |
|                       | `slm`                  | Out-of-tree |
|                       | `tigerlake`            | Out-of-tree |
|                       | `tremont`              | Out-of-tree |
|                       | `westmere`             | Out-of-tree |
|                       | `winchip-c6`           | Out-of-tree |
|                       | `winchip2`             | Out-of-tree |
|                       | `x86-64`               | Out-of-tree |
|                       | `yonah`                | `i686-apple-darwin` |
|                       | `znver1`               | Out-of-tree |
|                       | `znver2`               | Out-of-tree |
| `x86_64`              | `amdfam10`             | Out-of-tree |
|                       | `athlon`               | Out-of-tree |
|                       | `athlon-4`             | Out-of-tree |
|                       | `athlon-fx`            | Out-of-tree |
|                       | `athlon-mp`            | Out-of-tree |
|                       | `athlon-tbird`         | Out-of-tree |
|                       | `athlon-xp`            | Out-of-tree |
|                       | `athlon64`             | Out-of-tree |
|                       | `athlon64-sse3`        | Out-of-tree |
|                       | `atom`                 | Out-of-tree |
|                       | `barcelona`            | Out-of-tree |
|                       | `bdver1`               | Out-of-tree |
|                       | `bdver2`               | Out-of-tree |
|                       | `bdver3`               | Out-of-tree |
|                       | `bdver4`               | Out-of-tree |
|                       | `bonnell`              | Out-of-tree |
|                       | `broadwell`            | Out-of-tree |
|                       | `btver1`               | Out-of-tree |
|                       | `btver2`               | Out-of-tree |
|                       | `c3`                   | Out-of-tree |
|                       | `c3-2`                 | Out-of-tree |
|                       | `cannonlake`           | Out-of-tree |
|                       | `cascadelake`          | Out-of-tree |
|                       | `cooperlake`           | Out-of-tree |
|                       | `core-avx-i`           | Out-of-tree |
|                       | `core-avx2`            | Out-of-tree |
|                       | `core2`                | Out-of-tree |
|                       | `corei7`               | Out-of-tree |
|                       | `corei7-avx`           | Out-of-tree |
|                       | `generic`              | Out-of-tree |
|                       | `geode`                | Out-of-tree |
|                       | `goldmont`             | Out-of-tree |
|                       | `goldmont-plus`        | Out-of-tree |
|                       | `haswell`              | Out-of-tree |
|                       | `i386`                 | Out-of-tree |
|                       | `i486`                 | Out-of-tree |
|                       | `i586`                 | Out-of-tree |
|                       | `i686`                 | Out-of-tree |
|                       | `icelake-client`       | Out-of-tree |
|                       | `icelake-server`       | Out-of-tree |
|                       | `ivybridge`            | Out-of-tree |
|                       | `k6`                   | Out-of-tree |
|                       | `k6-2`                 | Out-of-tree |
|                       | `k6-3`                 | Out-of-tree |
|                       | `k8`                   | Out-of-tree |
|                       | `k8-sse3`              | Out-of-tree |
|                       | `knl`                  | Out-of-tree |
|                       | `knm`                  | Out-of-tree |
|                       | `lakemont`             | Out-of-tree |
|                       | `nehalem`              | Out-of-tree |
|                       | `nocona`               | Out-of-tree |
|                       | `opteron`              | Out-of-tree |
|                       | `opteron-sse3`         | Out-of-tree |
|                       | `penryn`               | Out-of-tree |
|                       | `pentium`              | Out-of-tree |
|                       | `pentium-m`            | Out-of-tree |
|                       | `pentium-mmx`          | Out-of-tree |
|                       | `pentium2`             | Out-of-tree |
|                       | `pentium3`             | Out-of-tree |
|                       | `pentium3m`            | Out-of-tree |
|                       | `pentium4`             | Out-of-tree |
|                       | `pentium4m`            | Out-of-tree |
|                       | `pentiumpro`           | Out-of-tree |
|                       | `prescott`             | Out-of-tree |
|                       | `sandybridge`          | Out-of-tree |
|                       | `silvermont`           | Out-of-tree |
|                       | `skx`                  | Out-of-tree |
|                       | `skylake`              | Out-of-tree |
|                       | `skylake-avx512`       | Out-of-tree |
|                       | `slm`                  | Out-of-tree |
|                       | `tigerlake`            | Out-of-tree |
|                       | `tremont`              | Out-of-tree |
|                       | `westmere`             | Out-of-tree |
|                       | `winchip-c6`           | Out-of-tree |
|                       | `winchip2`             | Out-of-tree |
|                       | `x86-64`               | `x86_64-fortanix-unknown-sgx` `x86_64-fuchsia` `x86_64-linux-android` `x86_64-linux-kernel` `x86_64-pc-solaris` `x86_64-pc-windows-gnu` `x86_64-pc-windows-msvc` `x86_64-rumprun-netbsd` `x86_64-sun-solaris` `x86_64-unknown-cloudabi` `x86_64-unknown-dragonfly` `x86_64-unknown-freebsd` `x86_64-unknown-haiku` `x86_64-unknown-hermit` `x86_64-unknown-hermit-kernel` `x86_64-unknown-illumos` `x86_64-unknown-l4re-uclibc` `x86_64-unknown-linux-gnu` `x86_64-unknown-linux-gnux32` `x86_64-unknown-linux-musl` `x86_64-unknown-netbsd` `x86_64-unknown-openbsd` `x86_64-unknown-redox` `x86_64-unknown-uefi` `x86_64-uwp-windows-gnu` `x86_64-uwp-windows-msvc` `x86_64-wrs-vxworks` |
|                       | `yonah`                | Out-of-tree |
|                       | `znver1`               | Out-of-tree |
|                       | `znver2`               | Out-of-tree |

## Unsupported CPU architectures

Here's an list of CPU architectures that don't currently enjoy LLVM support
(at least in the LLVM fork that Rust uses). If you have a machine with one of
these, you are out of luck.

| Vendor            | CPU               | Comments                                                                                              |
|-------------------|-------------------|-------------------------------------------------------------------------------------------------------|
| ARM               | ARM2/ARM250/ARM3  | Armv2 instruction set. Only has 26-bit pointers. e.g. Acorn Archimedes                                |
| ARM               | ARM6/ARM7         | Armv3 instruction set. Supports 26-bit and 32-bit pointers. e.g. Acorn RiscPC, A7500                  |
| DEC               | Alpha 21064 (EV4) | e.g. Digital DECpc AXP 150                                                                            |
| DEC               | Alpha 21164 (EV5) | e.g. Digital AlphaStation 500/266 workstation                                                         |
| DEC               | Alpha 21264 (EV6) | e.g. Digital AlphaStation DS25 workstation                                                            |
| DEC               | Alpha 21364 (EV7) | e.g. Digital AlphaServer ES47                                                                         |
| Intel             | 8080              | e.g. MITS Altair 8800                                                                                 |
| Intel             | 8086/8088         | Rust doesn't have segmented memory support. e.g. IBM PC and XT and clones                             |
| Intel             | 80286             | Compatible with 8086. Rust doesn't have segmented memory support. e.g. IBM PC AT and clones           |
| MOS               | 6502              | e.g. Commodore PET/VIC-20/C64, Apple I/II, Nintendo Entertainment System                              |
| Motorola          | 6800              | e.g. MITS Altair 680                                                                                  |
| Motorola          | 6809              | Replaced the 6800. Has two stack pointers. e.g. Tandy TRS-80                                          |
| Motorola          | 68000             | e.g. Commodore Amiga 500, Atari ST, Apple Macintosh, SEGA Genesis                                     |
| Motorola          | 68010             | e.g. Sun2, HP 9000 Series 300                                                                         |
| Motorola          | 68020             | e.g. Commodore Amiga 1200, Atari ST, Apple Macintosh LC, Sun3                                         |
| Motorola          | 68030             | e.g. Commodore Amiga 3000, Atari TT, Apple Macintosh II, NeXT Cube, Sun-3x                            |
| Motorola          | 68040             | e.g. Commodore Amiga 4000, Apple Macintosh Quadra series                                              |
| Zilog             | Z80               | Enhanced 8080 ISA. e.g. Sinclair ZX80/81/Spectrum, Amstrad CPC/PCW, MSX                               |
| Intel             | Itanium           | IA-64 ISA. e.g. HP Integrity rx4610                                                                   |
| Intel             | Itanium 2         | IA-64 ISA. e.g. HP Integrity rx1600                                                                   |
| Intel             | Itanium 9300      | IA-64 ISA. e.g. HP Integrity rx2800                                                                   |
| Intel             | Itanium 9500      | IA-64 ISA                                                                                             |
| Intel             | Itanium 9700      | Last ever IA-64 ISA chip                                                                              |
| HP                | PA-7x00           | PA-RISC 1.1 ISA. e.g. HP 9000 Series 700 Workstations                                                 |
| HP                | PA-8x00           | PA-RISC 2.0 ISA. e.g. HP 9000 Superdome mainframe                                                     |

## Unsupported OSes

Here's a list of OS / CPU combinations that Rust doesn't currently support. If
you have a machine that runs one of these, you are out of luck.

This list is incomplete. Please help complete it!

| Vendor           | OS                   | Microarchitecture                                             |
|------------------|----------------------|---------------------------------------------------------------|
| Acorn            | RISC OS 2/3.1        | Armv2                                                         |
| Acorn            | RISC OS 3.5+         | Armv3/v4                                                      |
| ROOL             | RISC OS 4/5          | Armv3 .. Armv8                                                |
| Apple            | System 1 .. System 7 | 68k                                                           |
| Apple            | Mac OS 8/9           | PowerPC                                                       |
| Apple            | Mac OS X 10.0..10.4  | PowerPC/PowerPC64                                             |
| Apple            | Mac OS X 10.5+       | x86 x86_64                                                    |
| Be               | BeOS                 | PowerPC x86                                                   |
| Commodore        | Amiga OS             | 68k PowerPC                                                   |
| Digital          | Tru64 UNIX           | Alpha                                                         |
| Digital          | VMS                  | VAX Alpha IA64 x86-64                                         |
| FreeBSD          | FreeBSD              | Lots of CPU architecture not listed above                     |
| IBM              | AIX                  | POWER, ROMP, PowerPC, x86, S/370, S/390                       |
| IBM              | OS/2                 | x86                                                           |
| Linux            | Linux                | Lots of CPU architecture not listed above                     |
| Microsoft        | DOS                  | x86                                                           |
| Microsoft        | Windows 2000         | x86                                                           |
| Microsoft        | Windows 3.x          | x86                                                           |
| Microsoft        | Windows 9x           | x86                                                           |
| Microsoft        | Windows NT 3.x/4     | Alpha MIPS PowerPC x86                                        |
| Microsoft        | Windows XP           | x86/x86_64                                                    |
| Microsoft        | Xenix                | x86                                                           |
| NetBSD           | NetBSD               | AArch64 Alpha Arm HP-PA Itanium 68k MIPS RISC-V SH3 SPARC VAX |
| Next             | NextStep             | 68k x86 PA-RISC SPARC                                         |
| OpenBSD          | OpenBSD              | Lots of CPU architecture not listed above                     |
| Silicon Graphics | IRIX                 | MIPS                                                          |
| Sun              | Solaris              | SPARC V8 x86                                                  |
| Sun              | SunOS                | 68k x86 SPARC                                                 |

## What is the oldest machine I could compile Rust code for?

Let's assume we're allowed to upgrade the OS on this machine to the latest
support (as opposed to what it shipped with).

The Intel Pentium (i586) was supported up to Debian Jessie (Kernel 3.16). The
i586-unknown-linux-musl target *should* support Linux kernel 2.6.39 or higher,
so, I think you could compile a full stdlib Rust program for a **Pentium 60**
(from early 1993) running Debian Jessie using a standard built-in target.

If you are happy to supply a custom JSON format target (and use the nightly
compiler), you can target a [386 running
MS-DOS](https://github.com/Serentty/rusty-dos).

## What is the oldest machine I could run the Rust Compiler on (if I had enough RAM/swap)?

For this, we scan
https://doc.rust-lang.org/nightly/rustc/platform-support.html and look for a
tick in the "Host" column.

The i686-unknown-linux-gnu target works back to Kernel 2.6.32 and glibc 2.11,
so you could find yourself a Pentium Pro (from late 1995) and run Debian
Squeeze on it (which comes with Kernel 2.6.32). But you'll need a lot of RAM
(or a lot of swap and a whole lot more patience).

The `powerpc-unknown-linux-gnu` targets an unspecified PowerPC, so could
potentially work all the back to the 1993 PowerPC 601 in the IBM RS/6000? Can
anyone beat that?
