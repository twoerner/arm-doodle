.PHONY: all clean
ALL = rootfs
CFLAGS = -mcpu=arm926ej-s -g -Wall -Wextra
PREFIX = arm-unknown-linux-gnueabi-
CC = $(PREFIX)gcc
AS = $(PREFIX)as
LD = $(PREFIX)ld
STRIP = $(PREFIX)strip
OBJDUMP = $(PREFIX)objdump
OBJCOPY = $(PREFIX)objcopy

all: $(ALL)

rootfs: init
	echo $< | cpio -oc > $@

init: test.c
	$(CC) $(CFLAGS) -static $< -o $@
	$(STRIP) $@

clean::
	$(RM) $(ALL) init
