NULL =

CLEANFILES =
DISTCLEANFILES =

EXTRA_DIST =

source_c = \
	cogl-pango-display-list.c   \
	cogl-pango-fontmap.c        \
	cogl-pango-render.c         \
	cogl-pango-glyph-cache.c    \
	cogl-pango-pipeline-cache.c \
	$(NULL)

source_h = cogl-pango.h

source_h_priv = \
	cogl-pango-display-list.h   \
	cogl-pango-private.h        \
	cogl-pango-glyph-cache.h    \
	cogl-pango-pipeline-cache.h \
	$(NULL)

ukwmlibdir = $(libdir)/ukwm
ukwmlib_LTLIBRARIES = libukwm-cogl-pango-@LIBUKWM_API_VERSION@.la

libukwm_cogl_pango_@LIBUKWM_API_VERSION@_la_SOURCES = $(source_c) $(source_h) $(source_h_priv)
libukwm_cogl_pango_@LIBUKWM_API_VERSION@_la_CFLAGS = $(COGL_DEP_CFLAGS) $(COGL_PANGO_DEP_CFLAGS) $(COGL_EXTRA_CFLAGS) $(MAINTAINER_CFLAGS)
libukwm_cogl_pango_@LIBUKWM_API_VERSION@_la_LIBADD = $(top_builddir)/cogl/libukwm-cogl-$(LIBUKWM_API_VERSION).la
libukwm_cogl_pango_@LIBUKWM_API_VERSION@_la_LIBADD += $(COGL_DEP_LIBS) $(COGL_PANGO_DEP_LIBS) $(COGL_EXTRA_LDFLAGS)
libukwm_cogl_pango_@LIBUKWM_API_VERSION@_la_LDFLAGS = \
	-export-dynamic \
	-rpath $(ukwmlibdir) \
	-export-symbols-regex "^cogl_pango_.*" \
	-no-undefined \
	-avoid-version

AM_CPPFLAGS = \
	-DCOGL_COMPILATION		\
	-DG_LOG_DOMAIN=\"CoglPango\"	\
	-I$(top_srcdir)/cogl		\
	-I$(top_builddir)/cogl		\
	-I$(top_srcdir)/cogl/winsys	\
	-I$(top_srcdir)			\
	-I$(top_builddir)

cogl_base_includedir = $(includedir)/ukwm
cogl_pangoheadersdir = $(cogl_base_includedir)/cogl/cogl-pango
cogl_pangoheaders_HEADERS = $(source_h)

pc_files = ukwm-cogl-pango-$(LIBUKWM_API_VERSION).pc

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = $(pc_files)

DISTCLEANFILES += $(pc_files)

EXTRA_DIST += cogl-pango.symbols

-include $(INTROSPECTION_MAKEFILE)

INTROSPECTION_GIRS =

if HAVE_INTROSPECTION
INTROSPECTION_COMPILER_ARGS=--includedir=$(top_builddir)/cogl

CoglPango-@LIBUKWM_API_VERSION@.gir: libukwm-cogl-pango-$(LIBUKWM_API_VERSION).la Makefile

CoglPango_@LIBUKWM_API_VERSION@_gir_NAMESPACE = CoglPango
CoglPango_@LIBUKWM_API_VERSION@_gir_VERSION = @LIBUKWM_API_VERSION@
CoglPango_@LIBUKWM_API_VERSION@_gir_LIBS = $(top_builddir)/cogl/libukwm-cogl-$(LIBUKWM_API_VERSION).la libukwm-cogl-pango-$(LIBUKWM_API_VERSION).la
CoglPango_@LIBUKWM_API_VERSION@_gir_FILES = $(source_h) $(source_c)
CoglPango_@LIBUKWM_API_VERSION@_gir_CFLAGS = $(AM_CPPFLAGS) $(COGL_DEP_CFLAGS) $(COGL_PANGO_DEP_CFLAGS)
CoglPango_@LIBUKWM_API_VERSION@_gir_INCLUDES = Pango-1.0 PangoCairo-1.0
CoglPango_@LIBUKWM_API_VERSION@_gir_EXPORT_PACKAGES = ukwm-cogl-pango-@LIBUKWM_API_VERSION@
CoglPango_@LIBUKWM_API_VERSION@_gir_SCANNERFLAGS = \
	--warn-all \
	--identifier-prefix=CoglPango \
	--symbol-prefix=cogl_pango \
	--c-include='cogl-pango/cogl-pango.h' \
	--include-uninstalled=$(top_builddir)/cogl/Cogl-@LIBUKWM_API_VERSION@.gir

INTROSPECTION_GIRS += CoglPango-@LIBUKWM_API_VERSION@.gir

girdir = $(ukwmlibdir)
gir_DATA = $(INTROSPECTION_GIRS)

typelibdir = $(ukwmlibdir)
typelib_DATA = $(INTROSPECTION_GIRS:.gir=.typelib)

CLEANFILES += $(gir_DATA) $(typelib_DATA)
endif
