# ARMv8 Pipeline Simulator

A portfolio-ready C++ project implementing a pedagogical 5-stage pipelined CPU simulator for a subset of the ARMv8-A integer instruction set. The simulator models **fetch → decode → execute → memory → writeback**, includes instruction trace logging, uses **CMake**, and ships with a **GoogleTest** suite and Linux CI.

## What this project does

- Simulates a 5-stage pipeline with explicit IF/ID, ID/EX, EX/MEM, and MEM/WB latches
- Supports a focused AArch64-style integer subset with **40+ decoded instructions**
- Implements branch flushing and a simple **load-use hazard stall**
- Logs pipeline activity, flags, and register state every cycle for debugging
- Uses **CMake + FetchContent** for GoogleTest and **GitHub Actions** for CI on Linux

## Scope

This is a **text-assembly simulator**, not a raw binary decoder and not a full ARMv8 implementation. That makes it realistic for a portfolio repo while still demonstrating core architecture knowledge, pipeline behaviour, control flow, memory access, and testing discipline.

## Instruction subset

Implemented opcodes:

- Data movement: `MOV`, `MOVZ`, `MVN`, `ADR`
- Arithmetic: `ADD`, `ADDI`, `ADDS`, `ADDSI`, `SUB`, `SUBI`, `SUBS`, `SUBSI`, `MUL`, `SDIV`, `UDIV`, `NEG`
- Logical/bitwise: `AND`, `ANDI`, `ORR`, `ORRI`, `EOR`, `EORI`, `TST`
- Shifts: `LSL`, `LSR`, `ASR`
- Flag-setting comparisons: `CMP`, `CMN`
- Memory: `LDR`, `STR`, `LDUR`, `STUR`
- Control flow: `B`, `BEQ`, `BNE`, `BGT`, `BGE`, `BLT`, `BLE`, `CBZ`, `CBNZ`, `NOP`, `HALT`

## Build

```bash
cmake -S . -B build -DARMSIM_BUILD_TESTS=ON
cmake --build build --parallel
ctest --test-dir build --output-on-failure
```

## Run the demo

```bash
./build/armv8_sim programs/demo_sum.asm --trace demo.trace
```

## Example assembly

```asm
MOVZ X0, #0
MOVZ X1, #5
MOVZ X2, #1

loop:
ADD X0, X0, X2
ADDI X2, X2, #1
SUBI X1, X1, #1
CBNZ X1, loop
HALT
```

## Suggested GitHub repo description

> 5-stage ARMv8-style pipeline simulator in C++ with CMake, GoogleTest, trace logging, hazard stalling, and Linux CI.

## Suggested CV line

**ARMv8 Instruction Set Simulator** | C++, CMake, GoogleTest, Linux | 2026  
Implemented a 5-stage pipelined CPU simulator modelling fetch, decode, execute, memory, and writeback for a subset of the ARMv8 integer ISA; added trace logging, hazard handling, unit tests, and Linux CI.
