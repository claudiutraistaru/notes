# QEMU

Quick Emulator

## Full system emulation

Emulate entire physical computer system.

### NOTES

- To emulate a system, use `qemu-system-*`. The wildcard (\*) specify the processor architecture.
- Supported architectures: aarch64, arm, riscv32, riscv64, sparc, sparc64, x64\_64, etc
- Use `-drive option[,option[,option[,...]]]` to define a drive. It can be a block driver node or a guest device. In "blog\_os", "-drive" argument is used like `qemu-system-x86_64 -drive format=raw,file=path/to/binary`.
- Different types of block devices:
  - floppy disk: `-fda`, `-fdb`
  - hard disk: `-hda`, `-hdb`, `-hdc`, `-hdd`
  - CD-ROM: `-cdrom`
  - A new block device: `-blockdev`
