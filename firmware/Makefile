# customize the following paths for your computer
ROOT_DIR:=$(shell dirname $(realpath $(lastword $(MAKEFILE_LIST))))
INCLUDE1 = ./usb/include
INCLUDE2 = ./usb/src
INCLUDE3 = ./i2c
CC = xc8

CHIP = 16F1459

CFLAGS = --chip=$(CHIP) -Q -G  --double=24 --float=24
CFLAGS += --opt=default,+asm,-asmfile,+speed,-space,-debug --addrqual=ignore
CFLAGS += --mode=pro -N64 -I. -I$(INCLUDE1) -I$(INCLUDE2) -I$(INCLUDE3) --warn=0 --asmlist --summary=default,-psect,-class,+mem,-hex,-file --output=default,-inhx032 
CFLAGS += --runtime=default,+clear,+init,-keep,-no_startup,+osccal,-resetbits,-download,-stackcall,+clib

all: Makefile
	$(CC) $(CFLAGS) -o./firmware.hex main.c i2c/i2c_software.c usb_descriptors.c usb/src/usb.c
	rm -f *.p1 *.d *.pre *.sym *.cmf *.cof *.hxl *.lst *.obj *.rlf *.sdb
	rm -f funclist

clean:
	rm -f firmware.hex

flash: Makefile
	$(CC) $(CFLAGS) -o./firmware.hex main.c i2c/i2c_software.c usb_descriptors.c usb/src/usb.c
	rm -f *.p1 *.d *.pre *.sym *.cmf *.cof *.hxl *.lst *.obj *.rlf *.sdb
	rm -f funclist
	pk2cmd -P -M -F$(ROOT_DIR)/firmware.hex
