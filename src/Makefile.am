AM_CPPFLAGS = -DLOCALEDIR=\"$(localedir)\" -I$(top_builddir)/lib -I$(top_srcdir)/lib

bin_PROGRAMS = 	ttdbcli
ttdbcli_SOURCES = ttdb_cli.c

ttdb-cli_LDADD = $(top_builddir)/lib/libgnu.a @LIBINTL@ 
