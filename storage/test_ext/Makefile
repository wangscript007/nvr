CURDIR = $(shell pwd)
ROOTDIR = ../..
CURWORKDIR = $(CURDIR)/$(ROOTDIR)
include $(ROOTDIR)/Rules.make

SrcDir = src/
ObjDir = obj/
Src = $(wildcard $(SrcDir)*.c)
SrcFile = $(notdir $(Src))
ObjFile = $(patsubst %.c,%.o,$(SrcFile))
Obj = $(addprefix $(ObjDir),$(ObjFile))
CC := $(CROSS_PREFIX)gcc
AR := $(CROSS_PREFIX)ar

CFLAGS := $(CFLAGS_EXTRA) -I$(STORAGE_DIR)/inc
LDFLAGS := $(LDFLAGS_EXTRA) -lstorage_ext -lstorage -lnet -lavformat -lavcodec -lavutil


OUTPUT	:= storage_ext_test

all:main

main:$(Obj)
	$(CC) -o $(OUTPUT) $^ $(LDFLAGS)

.depend:$(Src)
	@$(CC) $(CFLAGS) -MM $(Src) > $@
sinclude .depend

$(ObjDir)%.o:$(SrcDir)%.c
	$(CC) -c $(CFLAGS) $< -o $@

.PHONY: clean install

clean:
	-rm -f $(OUTPUT)
	rm -f $(ObjDir)*.o
	-rm -f .depend

install:
	install $(OUTPUT) $(TARGET_APP_DIR)
