.PHONY: all clean
ALL = test.bin test.dis
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

clean::
	$(RM) $(ALL) *\.o *\.elf
