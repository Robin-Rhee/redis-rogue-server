#set environment variable RM_INCLUDE_DIR to the location of redisexp.h
ifndef RM_INCLUDE_DIR
	RM_INCLUDE_DIR=../
endif

ifndef RMUTIL_LIBDIR
	RMUTIL_LIBDIR=../rmutil
endif

# find the OS
uname_S := $(shell sh -c 'uname -s 2>/dev/null || echo not')

# Compile flags for linux / osx
ifeq ($(uname_S),Linux)
	SHOBJ_CFLAGS ?=  -fno-common -g -ggdb
	SHOBJ_LDFLAGS ?= -shared -Bsymbolic
else
	SHOBJ_CFLAGS ?= -dynamic -fno-common -g -ggdb
	SHOBJ_LDFLAGS ?= -bundle -undefined dynamic_lookup
endif
CFLAGS = -I$(RM_INCLUDE_DIR) -Wall -g -fPIC -lc -lm -std=gnu99  
CC=gcc

all: rmutil exp.so

rmutil: FORCE
	$(MAKE) -C $(RMUTIL_LIBDIR)

#exp.so: exp.o
#	$(LD) -o $@ exp.o $(SHOBJ_LDFLAGS) $(LIBS) -L$(RMUTIL_LIBDIR) -lrmutil -lc 

exp.so: exp.c
	$(CC) -o $@ $< $(CFLAGS) $(SHOBJ_LDFLAGS) -L$(RMUTIL_LIBDIR) -lrmutil -lc
	mv exp.so ~/redis-rogue-server

clean:
	rm -rf *.xo *.so *.o

FORCE:
