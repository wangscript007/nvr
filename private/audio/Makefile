CURDIR = $(shell pwd)
ROOTDIR = ../..
CURWORKDIR = $(CURDIR)/$(ROOTDIR)
include $(ROOTDIR)/Rules.make

SrcDir = src/
ObjDir = obj/
IncludeDir = ./inc
Src = $(wildcard $(SrcDir)*.c)
SrcFile = $(notdir $(Src))
ObjFile = $(patsubst %.c,%.o,$(SrcFile))
Obj = $(addprefix $(ObjDir),$(ObjFile))
CC := $(CROSS_PREFIX)gcc
AR := $(CROSS_PREFIX)ar

CFLAGS := $(CFLAGS_EXTRA) -I./inc
LDFLAGS := $(LDFLAGS_EXTRA) -lasound

OUTPUT	:= libcapture_play_audio.so

all:main
main:$(Obj)
	$(CC) $(LDFLAGS) -shared -o $(OUTPUT) $^

.depend:$(Src)
	@$(CC) $(CFLAGS) -MM $(Src) > $@
sinclude .depend

$(ObjDir)%.o:$(SrcDir)%.c
	$(CC) $(CFLAGS) -c -I$(IncludeDir) -fPIC  $< -o $@

.PHONY: clean install
clean:
	-rm -f $(OUTPUT)
	rm -f $(ObjDir)*.o
	-rm -f .depend

install:
	install $(OUTPUT) $(PRI_LIB_DIR)
	ln -sf $(CURDIR)/inc/audio_params.h $(PRI_INC_DIR)/audio_params.h
