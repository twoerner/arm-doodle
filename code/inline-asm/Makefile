.PHONY: all clean
ALL = asm_test asm_test.dis
CFLAGS = -mcpu=cortex-a8 -marm -static -O2 -Wall -Wextra
CC = arm-none-linux-gnueabi-gcc

all: $(ALL)
asm_test: asm_test.c
asm_test.dis: asm_test
	arm-none-linux-gnueabi-objdump -d $^ > $@

clean::
	$(RM) $(ALL)
