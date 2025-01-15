# MDB Makefile for ELKS using IA16

############# Standard Section for IA16 C ##############
ifndef TOPDIR
$(error ELKS TOPDIR is not defined)
endif

CC = ia16-elf-gcc
LD = ia16-elf-gcc
CLBASE = -melks-libc -mtune=i8086 -mcmodel=small -mno-segment-relocation-stuff
CLBASE += -fno-inline -fno-builtin-printf -fno-builtin-fprintf
WARNINGS = -Wall -Wextra -Wtype-limits -Wno-unused-parameter -Wno-sign-compare
INCLUDES = -I$(TOPDIR)/include -I$(TOPDIR)/libc/include -I$(TOPDIR)/elks/include

# add the sources and the defines to try this...
# (3) Select Options
#
# i)   For GNU_EXEC Support, uncomment:
#
#FOR_GNU		=gnu_sym.o
#DEF_GNU		=-DGNU_SUPPORT
#
# ii)  For tracing of syscalls, uncomment:
#
#FOR_SYSCALLS 	=syscalls.o decode.o ioctl.o
#DEF_SYSCALLS	=-DSYSCALLS_SUPPORT
#
# iii) For no debugging of mdb, uncomment:
#
#DEF_DEBUG	=-DNDEBUG

DEFINES = -D__ELKS__
CFLAGS = -Os $(CLBASE) $(WARNINGS) $(INCLUDES) $(DEFINES) $(LOCALFLAGS)
LDFLAGS = $(CLBASE)
LDLIBS =

OBJS = $(SRCS:.c=.oaj)
%.oaj: %.c
	$(CC) $(CFLAGS) -c -o $*.oaj $<

############# End of Standard Section ##############

BINDIR = ../elks-bin
LOCALFLAGS = -Dunix
LDFLAGS += -maout-stack=4096 -maout-heap=16384
SRCS = mdb.c mdbexp.c kernel.o sym.c trace.c core.c misc.c io.c
PROG = $(BINDIR)/make

all: $(PROG)

$(PROG): $(OBJS)
	$(LD) $(LDFLAGS) -o $@ $^ $(LDLIBS)

clean:
	rm -f $(PROG) *.oaj
