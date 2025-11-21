SC-Lab-5
=========

This folder contains a self-contained minimal package of the Satellite Control project selected files so you can copy/paste into another repo and run Scenario 1 in both C (emulation) and RISC-V (QEMU) modes.

Included files
- wrapper_interactive.c (modificado: ahora fuerza Escenario 1)
- memory_map.c / memory_map.h
- main_riscv.c
- kernel.c
- linker.ld
- Makefile
- start.s, scheduler.s, trap_handler.s
- stacks.c / stacks.h
- pcb.h
- debug_gdb.sh
- Processes/ (assembly processes)
- temperaturas1.txt (los demás archivos de temperaturas no son usados)

Quick instructions

1) Build C emulation (x86_64):

```bash
cd SC-Lab-5
make interactive
```

Run Scenario 1 (the wrapper now forces Scenario 1 and uses `temperaturas1.txt`). The program no longer prompts for scenario or temperature file.

```bash
# Run the interactive binary (it will automatically use Scenario 1 and temperaturas1.txt)
./satelite_interactive
```

2) Build RISC-V image and run under QEMU:

```bash
# build riscv binary (if Makefile includes 'riscv' target)
cd SC-Lab-5
make riscv
# run via provided debug_gdb.sh or your qemu invocation
./debug_gdb.sh
# Or run the riscv ELF directly with qemu-system-riscv32 (if installed)
# qemu-system-riscv32 -nographic -machine virt -kernel satelite.elf -singlestep
```

Notes
- The copied Makefile expects a typical riscv toolchain for building the RISC-V target. If you don't have riscv32-unknown-elf or similar, build only `interactive` (C emulation), which requires only a native gcc.
- `debug_gdb.sh` helps start QEMU with gdbserver and useful breakpoints.

If you want, I can also create a single tarball `SC-Lab-5.tar.gz` you can paste into another repo. Would you like that?