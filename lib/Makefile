TOPDIR = ..
-include $(TOPDIR)/config.mk

RANLIB ?= ranlib

LIBXBPS_MAJOR = 5
LIBXBPS_MINOR = 0
LIBXBPS_MICRO = 1
LIBXBPS_SHLIB = libxbps.so.$(LIBXBPS_MAJOR).$(LIBXBPS_MINOR).$(LIBXBPS_MICRO)

LDFLAGS += $(LIBXBPS_LDFLAGS) -shared -Wl,-soname,libxbps.so.$(LIBXBPS_MAJOR)

COMMON_OBJS 	  = common/cb_util.o \
			   		common/download.o \
			   		common/log.o \
				   	common/pubkey2fp.o \
			   		common/repo_sync.o \
			        common/verifysig.o \
				 	common/archive.o \
			        common/conf.o \
					common/initend.o \
					common/pkgdb.o \
 					common/proplib_wrapper.o \
 					common/repo.o \
 					common/rpool.o

COMPAT_OBJS       = compat/humanize_number.o \
 					compat/strcasestr.o \
 					compat/strlcat.o \
 					compat/strlcpy.o \
 					compat/vasprintf.o

EXTERNAL_OBJS     = external/dewey.o \
 					external/fexec.o \
 					external/mkpath.o

FETCH_OBJS        = fetch/common.o \
 					fetch/fetch.o \
 					fetch/file.o \
 					fetch/ftp.o \
 					fetch/http.o
FETCH_GEN         = fetch/ftperr.h \
					fetch/httperr.h
FETCH_CPPFLAGS    = -DFTP_COMBINE_CWDS -DINET6 -DWITH_SSL
ifdef HAVE_VISIBILITY
FETCH_CFLAGS 	 += -fvisibility=hidden
endif

PACKAGE_OBJS      = package/alternatives.o \
 					package/config_files.o \
 					package/configure.o \
 					package/fulldeptree.o \
 					package/msg.o \
					package/orphans.o \
 					package/register.o \
 					package/remove.o \
 					package/script.o \
 					package/state.o \
 					package/unpack.o

PLIST_UTIL_OBJS   = plist_util/fetch.o \
					plist_util/find.o \
 					plist_util/match.o \
 					plist_util/plist.o \
 					plist_util/remove.o

PLIST_OBJS        = portableproplib/prop_array.o \
 					portableproplib/prop_bool.o \
 					portableproplib/prop_dictionary.o \
 					portableproplib/prop_ingest.o \
					portableproplib/prop_object.o \
 					portableproplib/prop_stack.o \
 					portableproplib/prop_string.o \
					portableproplib/prop_array_util.o \
 					portableproplib/prop_number.o \
 					portableproplib/prop_dictionary_util.o \
 					portableproplib/prop_zlib.o \
					portableproplib/prop_data.o \
 					portableproplib/rb.o
PLIST_CFLAGS 	  = -Wno-unused-parameter
ifdef HAVE_VISIBILITY
PLIST_CFLAGS 	 += -fvisibility=hidden
endif

TRANSACTION_OBJS  = transaction/check_conflicts.o \
 					transaction/check_replaces.o \
 					transaction/check_revdeps.o \
 					transaction/check_shlibs.o \
 					transaction/commit.o \
 					transaction/fetch.o \
 					transaction/files.o \
 					transaction/internalize.o \
 					transaction/ops.o \
 					transaction/pkg_deps.o \
 					transaction/prepare.o \
 					transaction/store.o

UTIL_OBJS 		  = util/hash.o \
					util/path.o \
					util/util.o


OBJS 			  = $(COMMON_OBJS) \
	   				$(COMPAT_OBJS) \
	   				$(EXTERNAL_OBJS) \
	   				$(FETCH_OBJS) \
	   				$(PACKAGE_OBJS) \
	   				$(PLIST_UTIL_OBJS) \
	   				$(PLIST_OBJS) \
	   				$(TRANSACTION_OBJS) \
					$(UTIL_OBJS)

GENS 			  = $(COMMON_GENS) \
	   				$(COMPAT_GENS) \
	   				$(EXTERNAL_GENS) \
	   				$(FETCH_GENS) \
	   				$(PACKAGE_GENS) \
	   				$(PLIST_UTIL_GENS) \
	   				$(PLIST_GENS) \
	   				$(TRANSACTION_GENS) \
					$(UTIL_GENS)

.PHONY: all 
all: libxbps.so libxbps.a

fetch/ftperr.h: fetch/ftp.errors
	@printf " [GEN]\t\t$@\n"
	${SILENT}./fetch/errlist.sh ftp_errlist FTP $< > $@

fetch/httperr.h: fetch/fetch/http.errors
	@printf " [GEN]\t\t$@\n"
	@./fetch/errlist.sh http_errlist HTTP $< > $@

$(COMMON_OBJS): %.o: %.c $(COMMON_GENS)
	@printf " [CC]\t\t$@\n"
	${SILENT}$(CC) -o $@ $(CFLAGS) $(CPPFLAGS) $(COMMON_CFLAGS) $(COMMON_CPPFLAGS) -c $<

$(COMPAT_OBJS): %.o: %.c $(COMPAT_GENS)
	@printf " [CC]\t\t$@\n"
	${SILENT}$(CC) -o $@ $(CFLAGS) $(CPPFLAGS) $(COMPAT_CFLAGS) $(COMPAT_CPPFLAGS) -c $<

$(EXTERNAL_OBJS): %.o: %.c $(EXTERNAL_GENS)
	@printf " [CC]\t\t$@\n"
	${SILENT}$(CC) -o $@ $(CFLAGS) $(CPPFLAGS) $(EXTERNAL_CFLAGS) $(EXTERNAL_CPPFLAGS) -c $<

$(FETCH_OBJS): %.o: %.c $(FETCH_GENS)
	@printf " [CC]\t\t$@\n"
	${SILENT}$(CC) -o $@ $(CFLAGS) $(CPPFLAGS) $(FETCH_CFLAGS) $(FETCH_CPPFLAGS) -c $<

$(PACKAGE_OBJS): %.o: %.c $(PACKAGE_GENS)
	@printf " [CC]\t\t$@\n"
	${SILENT}$(CC) -o $@ $(CFLAGS) $(CPPFLAGS) $(PACKAGE_CFLAGS) $(PACKAGE_CPPFLAGS) -c $<

$(PLIST_UTIL_OBJS): %.o: %.c $(PLIST_UTIL_GENS)
	@printf " [CC]\t\t$@\n"
	${SILENT}$(CC) -o $@ $(CFLAGS) $(CPPFLAGS) $(PLIST_UTIL_CFLAGS) $(PLIST_UTIL_CPPFLAGS) -c $<

$(PLIST_OBJS): %.o: %.c $(PLIST_GENS)
	@printf " [CC]\t\t$@\n"
	${SILENT}$(CC) -o $@ $(CFLAGS) $(CPPFLAGS) $(PLIST_CFLAGS) $(PLIST_CPPFLAGS) -c $<

$(TRANSACTION_OBJS): %.o: %.c $(TRANSACTION_GENS)
	@printf " [CC]\t\t$@\n"
	${SILENT}$(CC) -o $@ $(CFLAGS) $(CPPFLAGS) $(TRANSACTION_CFLAGS) $(TRANSACTION_CPPFLAGS) -c $<

$(UTIL_OBJS): %.o: %.c $(UTIL_GENS)
	@printf " [CC]\t\t$@\n"
	${SILENT}$(CC) -o $@ $(CFLAGS) $(CPPFLAGS) $(UTIL_CFLAGS) $(UTIL_CPPFLAGS) -c $<

libxbps.so: $(OBJS) $(GENS)
	@printf " [CCLD]\t\t$@\n"
	${SILENT}$(CC) $(OBJS) $(CFLAGS) $(LDFLAGS) -o $(LIBXBPS_SHLIB)
	@-ln -sf $(LIBXBPS_SHLIB) libxbps.so.$(LIBXBPS_MAJOR)
	@-ln -sf $(LIBXBPS_SHLIB) libxbps.so

libxbps.a: $(OBJS) $(GENS)
	@printf " [AR]\t\t$@\n"
	${SILENT}$(AR) rcs $@ $(OBJS)
	@printf " [RANLIB]\t$@\n"
	${SILENT}$(RANLIB) $@

.PHONY: install
install: all
	install -d $(DESTDIR)$(LIBDIR)
	install -m 644 libxbps.a $(DESTDIR)$(LIBDIR)
	install -m 755 $(LIBXBPS_SHLIB) $(DESTDIR)$(LIBDIR)
	cp -a libxbps.so $(DESTDIR)$(LIBDIR)
	cp -a libxbps.so.$(LIBXBPS_MAJOR) $(DESTDIR)$(LIBDIR)

.PHONY: uninstall
uninstall:
	-rm -f $(DESTDIR)$(LIBDIR)/libxbps.*

.PHONY: clean
clean:
	-rm -f libxbps* $(OBJS) $(GENS)
