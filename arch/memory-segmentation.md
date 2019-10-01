# Memory Segmentation

There are 3 main [memory models](https://en.wikipedia.org/wiki/Flat_memory_model#Memory_models): __Flat memory model__, __Segmented memory model__ and __Paged memory model__.

## [Type of addresses](http://www.on-time.com/rtos-32-docs/rttarget-32/programming-manual/x86-cpu/protected-mode/virtual-linear-and-physical-addresses.htm)

Logical/Virtual address(known to process) -> Linear address(Mapped to a segment) -> Physical address(Mapped to memory, normally after page table lookup)

## [x86 Memory segmentation](https://en.wikipedia.org/wiki/X86_memory_segmentation)

- Intel 8086. 1978. Any program running on these processors can access any segment with no restrictions.

    Segment Selector is stored in segment register like CS, DS, ES and SS.

    Linear Address(20 bits) = Segment Selector(16 bits) * 0x10 + Offset(16 bits)

    20 bits => 1MB of addressable space.

    Each paragraph is 16 bytes. Each segment is 64 KB long. So a single virtual address can be potentially translated into 4096 segment:offset combinations.

- Intel 80286. 1982. There are "real mode" and "protected mode".

    Segment Selector becomes more than a base address. Segment Selector consists of 13-bit index(to GDP/LDT), 2-bit RPL(Requested Priviledge Level), and 1-bit Table Indicator(TI, GDT -> 0, LDT -> 1)

    13-bit index refers to an entry in GDP/LDT. Each entry in GDP is a 64-bit Segment Descriptor.

    Segment Descriptor in 80286 consists of 24-bit base address, 16-bit segment limit, 8-bit flags and 16-bit reserved.

    If request doesn't have the correct priviledge level or goes out of segment limit, a GP(general protection) fault will be triggered.

- Intel 80386.

    Introduced Paging, two more segment registers(FS and GS).

    Both address bus width and data bus width are 32 bit.

    Segment Descriptor in 80386 and later consists of 32-bit base address, 20-bit segment limit, and many flags:

        Granulairy: limit size: 0 -> byte, 1 -> 4096-byte page

        Default operand size: 0 -> 16-bit, 1 -> 32-bit

        Long mode: 0 -> 16-bit, 1 -> 64-bit

        AVL, P, DPL, C, R, A
