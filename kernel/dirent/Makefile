#
# Makefile for the direntry-library functions
#

LIB	=../Libc.a
#AR	=gar
#AS	=gas
#LD	=gld
AR	=ar
AS	=as
LD	=ld
LDFLAGS	=-s -x
CC	=gcc
INC	=-nostdinc -I../include
CFLAGS	=-Wall -O -fstrength-reduce -fomit-frame-pointer \
	-finline-functions $(INC)
CPP	=$(CC) -E $(INC)

.c.s:
	$(CC) $(CFLAGS) \
	-S -o $*.s $<
.s.o:
	$(CC) -c -o $*.o $<
.c.o:
	$(CC) $(CFLAGS) \
	-c -o $*.o $<

OBJS  =	closedir.o opendir.o readdir.o rewinddir.o

all: library

library: $(OBJS)
	$(AR) uvc $(LIB) $(OBJS)
	sync

clean:
	$(RM) -f core *.o *.a tmp_make
	for i in *.c;do $(RM) -f `basename $$i .c`.s;done

dep:
	sed '/\#\#\# Dependencies/q' < Makefile > tmp_make
	(for i in *.c;do echo -n `echo $$i | sed 's,\.c,\.s,'`" "; \
		$(CPP) -M $$i;done) >> tmp_make
	cp tmp_make Makefile

### Dependencies:
