AC_PREREQ(2.59)
AC_INIT([libexif command line interface], [0.6.22], [libexif-devel@lists.sourceforge.net], [exif])
AC_CONFIG_SRCDIR([exif/main.c])
AC_CONFIG_HEADERS([config.h])
AC_CONFIG_MACRO_DIR([auto-m4])
AM_INIT_AUTOMAKE([-Wall gnu 1.9 dist-bzip2 check-news])

# Use the silent-rules feature when possible.
m4_ifndef([AM_SILENT_RULES], [m4_define([AM_SILENT_RULES],[])])
AM_SILENT_RULES([yes])

GP_CHECK_SHELL_ENVIRONMENT
GP_CONFIG_MSG([Build])
GP_CONFIG_MSG([Source code location],[${srcdir}])

AC_PROG_CC
AC_C_CONST
AC_C_INLINE
AM_PROG_AR
AM_PROG_LIBTOOL
AM_CPPFLAGS="$CPPFLAGS -I\$(top_srcdir) -I\$(top_builddir)"
GP_CONFIG_MSG([Compiler],[${CC}])
AM_PROG_CC_C_O

AC_CHECK_FUNCS([isatty fileno])

# ---------------------------------------------------------------------------
# i18n support
# ---------------------------------------------------------------------------
GP_GETTEXT_HACK([${PACKAGE}],[Lutz Mueller and others])
ALL_LINGUAS="ast cs da de eo es fi fr fur gl hr id is it ja ko lv ms nl pl pt pt_BR ro ru sk sr sv tr uk vi zh_CN"
AM_GNU_GETTEXT_VERSION([0.14.1])
AM_GNU_GETTEXT([external])
AM_PO_SUBDIRS()
AM_ICONV()
GP_GETTEXT_FLAGS()


# ---------------------------------------------------------------------------
# locale.h: locale.h provides setlocale. It seems that some systems don't
#           have it (at least if configured --without-nls).
# ---------------------------------------------------------------------------
AC_CHECK_HEADERS([locale.h])
AC_CHECK_HEADER([iconv.h], [
	AC_DEFINE(HAVE_ICONV,1,[whether iconv is available])])

dnl Versions of GNU gettext >= 0.10.36 automatically convert messages into
dnl the correct locale encoding, but with older versions and maybe non-GNU
dnl versions the app needs to do that itself.
AC_ARG_ENABLE(gettext-iconv,
	      [  --enable-gettext-iconv  convert character encodings (only needed when gettext doesn't do it itself)],
	      [ AC_DEFINE(ENABLE_GETTEXT_ICONV,1,[whether to run iconv on gettext output]) ])

AC_CHECK_FUNCS(mblen)

# ---------------------------------------------------------------------------
# libraries needed
# ---------------------------------------------------------------------------
dnl Need 0.6.18 for exif_loader_get_buf
GP_CHECK_LIBRARY([LIBEXIF],[libexif],[>= 0.6.18])

# ---------------------------------------------------------------------------
# popt.h: Simplifies handling of command-line options enormously.
# ---------------------------------------------------------------------------
GP_CHECK_LIBRARY([POPT],[popt],[>= 1.12])


# ---------------------------------------------------------------------------
# Check for misc headers
# ---------------------------------------------------------------------------
AC_CHECK_HEADERS([unistd.h])


# ---------------------------------------------------------------------------
# Warnings: If we have GCC, be paranoid.
# ---------------------------------------------------------------------------
if test "x$GCC" = "xyes"; then
    AM_CPPFLAGS="$AM_CPPFLAGS -Wall -Wchar-subscripts -Wmissing-declarations -Wmissing-prototypes -Wnested-externs -Wpointer-arith"
    AM_LDFLAGS="$AM_LDFLAGS -g -Wall"
fi

AC_SUBST([AM_CPPFLAGS])dnl
AC_SUBST([AM_LDFLAGS])dnl


# ---------------------------------------------------------------------------
# Output files
# ---------------------------------------------------------------------------
AC_CONFIG_FILES([
  po/Makefile.in
  Makefile
  m4m/Makefile
  exif.spec
  libjpeg/Makefile
  exif/Makefile
  test/Makefile
  test/check-vars.sh
])
AC_OUTPUT

GP_CONFIG_OUTPUT()dnl
