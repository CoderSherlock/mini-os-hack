#
# ARM architecture specific makefiles.
#

TOPLEVEL_DIR = $(CURDIR)/../..
OBJ_DIR=$(CURDIR)
include ../../Config.mk

# include arch.mk has to be before minios.mk!

include arch.mk
include ../../minios.mk

include $(MINIOS_ROOT)/config/MiniOS.mk


# Sources here are all *.c (without $(MINIOS_TARGET_ARCH).S)
# This is handled in $(HEAD_ARCH_OBJ)
ARCH_SRCS := $(wildcard *.c)

# The objects built from the sources.
ARCH_OBJS := $(patsubst %.c,$(OBJ_DIR)/%.o,$(ARCH_SRCS))

ifeq ($(MINIOS_TARGET_ARCH),arm32)
ARCH_OBJS += $(OBJ_DIR)/hypercalls32.o
else
ARCH_OBJS += $(OBJ_DIR)/hypercalls64.o
endif

all: $(OBJ_DIR)/$(ARCH_LIB)

# $(HEAD_ARCH_OBJ) is only built here, needed on linking
# in ../../Makefile.
$(OBJ_DIR)/$(ARCH_LIB): $(ARCH_OBJS) $(OBJ_DIR)/$(HEAD_ARCH_OBJ)
	$(AR) rv $(OBJ_DIR)/$(ARCH_LIB) $(ARCH_OBJS)

clean:
	rm -f $(OBJ_DIR)/$(ARCH_LIB) $(ARCH_OBJS) $(OBJ_DIR)/$(HEAD_ARCH_OBJ)

