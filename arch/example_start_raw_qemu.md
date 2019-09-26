# Start Raw Qemu Example

## Assembly Example(main.s)

```s
.code16 # specify the processor to run in 16-bit mode
    mov $msg, %si # move msg address to SI(Source Index register)
    mov $0x0e, %ah # store 0xe to AH register. It's used for video service. 0xe is "teletype output".
loop:
    lodsb # LODS instruction move value(B byte, W word, D double word) at addr pointed by SI to destination(AL, AX, EAX)
    or %al, %al # have a chance to set zero flag.
    jz halt # jz is conditional jump. Jump only if ZF(zero flag) is set.
    int $0x10 # INT 0x10 is the BIOS interrupt call to video service. AH is set to "teleport output"
    jmp loop
halt:
    hlt
msg:
    .asciz "hello world" # asciz is ascii with a zero at the end
```

## Common interrupt table

[table in Wikipedia](https://en.wikipedia.org/wiki/BIOS_interrupt_call#Interrupt_table)

## Linker script example(link.ld)

```ld
SECTIONS
{
    /* The BIOS loads the code from the disk to this location.
     * We must tell that to the linker so that it can properly
     * calculate the addresses of symbols we might jump to.
     */
    /* . represents location counter */
    /* . sets the location counter to 0x7c00 */
    . = 0x7c00;
    /* sets the text output text section */
    .text :
    {
        __start = .;
        /* sets all input sections to this location */
        *(.text)
        /* Place the magic boot bytes at the end of the first 512 sector. */
        . = 0x1FE;
        /* write 0xAA55 as two bytes */
        SHORT(0xAA55)
    }
}
```

Linker Script [documentation](https://sourceware.org/binutils/docs/ld/Simple-Example.html#Simple-Example)

## Build & Link

`as -g -o main.o main.S` generates an object file that is 1700+ bytes in size.

`ld --oformat binary -o main.img -T link.ld main.o` generates an image that is 512 bytes in size. It is perfectly fit for the boot section.

`qemu-system-x86_64 -hda main.img` will run and display the message in BIOS

### My Question

How come linker links 1700+ bytes input to become 512 bytes output

My current understanding is that `main.o`(1700+ bytes) is in ELF format with text, data and etc sections. The code section is small. But ELF overhead is big. link striped away ELF overhead. Could be wrong.
