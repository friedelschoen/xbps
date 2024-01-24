TOPDIR = ../..
-include $(TOPDIR)/config.mk

BIN = portableproplib.a
OBJS += prop_array.o prop_bool.o
OBJS += prop_dictionary.o prop_ingest.o
OBJS += prop_object.o
OBJS += prop_stack.o prop_string.o
OBJS += prop_array_util.o prop_number.o
OBJS += prop_dictionary_util.o prop_zlib.o
OBJS += prop_data.o rb.o

EXTRA_CFLAGS = -Wno-unused-parameter
ifdef HAVE_VISIBILITY
EXTRA_CFLAGS += -fvisibility=hidden
endif

include $(TOPDIR)/mk/lib.mk