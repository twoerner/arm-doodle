.PHONY: all clean
ALL = test.dis flash.bin
CFLAGS = -mcpu=arm926ej-s -g -Wall -Wextra
PREFIX = arm-none-linux-gnueabi-
CC = $(PREFIX)gcc
AS = $(PREFIX)as
LD = $(PREFIX)ld
OBJDUMP = $(PREFIX)objdump
OBJCOPY = $(PREFIX)objcopy

all: $(ALL)

test.bin: test.elf
	$(OBJCOPY) -O binary $< $@

test.elf: test.ld startup.o test.o
	$(LD) -T test.ld test.o startup.o -o $@

startup.o: startup.s
test.o: test.c

test.dis: test.elf
	$(OBJDUMP) -d $^ > $@

flash.bin: u-boot.bin test.uimg
	cat u-boot.bin test.uimg > flash.bin
	@printf "bootm 0x%X\n" $(shell expr `stat -c%s u-boot.bin` + 65536)

test.uimg: test.bin
	$(UBOOT)/tools/mkimage -A arm -C none -O linux -T kernel -d $< -a 0x00100000 -e 0x00100000 $@

clean::
	$(RM) $(ALL) *\.o *\.elf
	$(RM) flash.bin test.bin test.uimg
