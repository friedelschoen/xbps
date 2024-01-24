TOPDIR = ../..
-include $(TOPDIR)/config.mk

BIN = fetch.a
INCL = common.h fetch.h ftperr.h httperr.h
OBJS = common.o fetch.o file.o ftp.o http.o
EXTRA_CPPFLAGS += -DFTP_COMBINE_CWDS -DINET6 -DWITH_SSL
ifdef HAVE_VISIBILITY
EXTRA_CFLAGS += -fvisibility=hidden
endif

ftperr.h: ftp.errors
	@printf " [GEN]\t\t$@\n"
	${SILENT}./errlist.sh ftp_errlist FTP $< > $@

httperr.h: http.errors
	@printf " [GEN]\t\t$@\n"
	@./errlist.sh http_errlist HTTP $< > $@

include $(TOPDIR)/mk/lib.mk