# Makefile for BeOS Release 4 operating systems

CC = gcc
AR = ar 
AS = nasm
CFLAGS = -c -O3 -Wall -Wno-multichar -D__FLAT__ -D__BEOS__
ARFLAGS = cr
LIBS = -L../lib/Haiku/ -laudio -lroot -lbe -lmedia -lstdc++

OBJS = audio.o wavfile.o xmfile.o s3mfile.o modfile.o mtmfile.o \
	iofile.o modeng.o nondrv.o mixdrv.o be3drv.o be4drv.o bedrv.o

LIB = ../lib/Haiku/libaudio.a

all : mp clean
	@echo done.

mp : mp.o $(LIB)
	$(CC) -o mp mp.o $(LIBS)

$(LIB) : $(OBJS)
	@if [ ! -e `dirname $(LIB)` ]; then mkdir -p `dirname $(LIB)`; fi
	$(AR) $(ARFLAGS) $(LIB) $(OBJS)

.SUFFIXES: .c .cpp .h .obj .S

.c.o:
	$(CC) $(CFLAGS) $<

.S.o:
	$(CC) $(CFLAGS) $<

.cpp.o:
	$(CC) $(CFLAGS) $<

.asm.o:
	$(AS) $<

clean :
	@rm -rf *.o
