# This Makefile will compile a .c file called 'filename.c' with SDCC into a 8051 .ihx file called 'filename.ihx'.
# Then FlashMagic will erase block 0, and flash 'filename.ihx' onto the ArduOne connected to COM-port number 'COM'.

# The variables below can be edited, but be sure not to add any spaces before or after the declerations.

# COM-port number:
COM=6
# The name of the .c file to be compiled and flashed:
filename=main
sdcc_path='C:\Program Files\SDCC\bin\sdcc.exe'
fm_path='C:\Program Files (x86)\Flash Magic\fm.exe'
# In cases where del doesn't work, change 'del' to 'rm' or 'erase' or 'Remove-Item'
remove_cmd=rm

all: compile erase flash

compile: $(filename).c
	if not exist objs mkdir objs
	$(sdcc_path) -mmcs51 $(filename).c -o objs/

erase:
	$(fm_path) 'DEVICE(89C51RD2Hxx, 11.0592, 0) COM($(COM),9600) ERASE(0, PROTECTISP)'

flash: $(filename).ihx
	$(fm_path) 'DEVICE(89C51RD2Hxx, 11.0592, 0) COM($(COM),9600) HEXFILE(objs/$(filename).ihx, NOCHECKSUMS, NOFILL, PROTECTISP)'

clean:
	$(remove_cmd) '$(filename).asm' '$(filename).ihx' '$(filename).lk' '$(filename).lst' '$(filename).map' '$(filename).mem' '$(filename).rel' '$(filename).rst' '$(filename).sym'