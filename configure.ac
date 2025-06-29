dnl Process this file with autoconf to produce a configure script.

dnl Copyright (C) 2004-2025 Free Software Foundation, Inc.

dnl This file is free software; as a special exception the author gives
dnl unlimited permission to copy and/or distribute it, with or without
dnl modifications, as long as this notice is preserved.
dnl
dnl This program is distributed in the hope that it will be useful, but
dnl WITHOUT ANY WARRANTY, to the extent permitted by law; without even the
dnl implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

AC_INIT([ttdb],
	[m4_esyscmd([build-aux/git-version-gen .tarball-version])],
	[ivan.guerreschi.dev@gmail.com], [],
	[https://www.github.com/nullzeiger/timetablesdb])

dnl Must come before AM_INIT_AUTOMAKE.
AC_CONFIG_AUX_DIR([build-aux])
AM_INIT_AUTOMAKE([1.11.1 readme-alpha subdir-objects])

dnl Minimum Autoconf version required.
AC_PREREQ([2.69])

dnl Where to generate output; srcdir location.
AC_CONFIG_HEADERS([config.h:config.in])dnl Keep filename to 8.3 for MS-DOS.
AC_CONFIG_SRCDIR([src/hello.c])

dnl Checks for programs.
dnl We need a C compiler.
AC_PROG_CC

dnl Since we use gnulib: gl_EARLY must be called as soon as possible after
dnl the C compiler is checked.  The others could be later, but we just
dnl keep everything together.
gl_EARLY
gl_INIT

dnl Are we building from git checked-out sources, or a tarball ?
dnl This is used in "Makefile.am" to avoid re-generating the manpage
dnl when building from tarballs.
AM_CONDITIONAL([BUILD_FROM_GIT], [test -d "$srcdir/.git"])
AM_CONDITIONAL([GIT_CROSS_COMPILING],
               [test -d "$srcdir/.git" && test $cross_compiling = yes])

dnl GNU help2man creates man pages from --help output; in many cases, this
dnl is sufficient, and obviates the need to maintain man pages separately.
dnl However, this means invoking executables, which we generally cannot do
dnl when cross-compiling, so we test to avoid that (the variable
dnl "cross_compiling" is set by AC_PROG_CC).
AS_IF([test $cross_compiling = no], [
  AM_MISSING_PROG([HELP2MAN], [help2man])
], [
  HELP2MAN=:
])

dnl Ensure VLAs are not used.
AC_DEFINE([GNULIB_NO_VLA], [1], [Define to 1 to disable use of VLAs])

dnl i18n support from GNU gettext.
AM_GNU_GETTEXT_VERSION([0.19.2])
AM_GNU_GETTEXT([external])

AC_CONFIG_FILES([Makefile
	lib/Makefile
	src/Makefile
	po/Makefile.in])

AC_OUTPUT
