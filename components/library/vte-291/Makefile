#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL)". You may
# only use this file in accordance with the terms of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source. A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright 2016 Alexander Pyhalov
#

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		vte
COMPONENT_VERSION=	0.42.5
COMPONENT_PROJECT_URL=	http://www.gnome.org
COMPONENT_SUMMARY=	Terminal emulation widget for GTK+
COMPONENT_FMRI=		library/desktop/vte-291
COMPONENT_CLASSIFICATION=	Desktop (GNOME)/Libraries
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.xz
COMPONENT_ARCHIVE_HASH=	\
    sha256:53cc15c5315d73b69f7848e07a5c512cd40b7caf0323e3d0e0d75d7ae65deee7
COMPONENT_ARCHIVE_URL=	http://ftp.gnome.org/pub/GNOME/sources/$(COMPONENT_NAME)/0.42/$(COMPONENT_ARCHIVE)
COMPONENT_LICENSE=	LGPLv2.1
COMPONENT_LICENSE_FILE=	COPYING

include $(WS_TOP)/make-rules/prep.mk
include $(WS_TOP)/make-rules/configure.mk
include $(WS_TOP)/make-rules/ips.mk

PATH=/usr/gnu/bin:/usr/bin

# Force use of gnutls-3 pkgconfig during 2.x->3.x transition
GNUTLS_PKG_CONFIG_PATH_32 = /usr/lib/pkgconfig/gnutls-3
GNUTLS_PKG_CONFIG_PATH_64 = /usr/lib/$(MACH64)/pkgconfig/gnutls-3
PKG_CONFIG_PATH = $(GNUTLS_PKG_CONFIG_PATH_$(BITS)):$(PKG_CONFIG_PATH.$(BITS))

LD_OPTIONS.32 += -L/usr/lib/gnutls-3 -R/usr/lib/gnutls-3
LD_OPTIONS.64 += -L/usr/lib/$(MACH64)/gnutls-3 -R/usr/lib/$(MACH64)/gnutls-3
LD_OPTIONS += $(LD_OPTIONS.$(BITS))

COMPONENT_PREP_ACTION =        ( cd $(@D)  && \
					libtoolize --force &&\
					gtkdocize &&\
					aclocal -I . &&\
					autoconf &&\
					autoheader &&\
					automake -c -f -a )

CONFIGURE_OPTIONS+=	--sysconfdir=/etc
CONFIGURE_OPTIONS+=	--libexecdir=$(CONFIGURE_LIBDIR.$(BITS))
CONFIGURE_OPTIONS+=	--localstatedir=/var/lib
CONFIGURE_OPTIONS+=	--disable-Bsymbolic
CONFIGURE_OPTIONS+=	--disable-vala

# gobject introspection
COMPONENT_BUILD_ENV +=	CC="$(CC)"
COMPONENT_BUILD_ENV +=	CFLAGS="$(CFLAGS)"

# Fixes tests run
unexport SHELLOPTS
COMPONENT_TEST_ENV += LD_OPTIONS="$(LD_OPTIONS)"
COMPONENT_TEST_MASTER = $(COMPONENT_TEST_RESULTS_DIR)/results-all.master
COMPONENT_TEST_TRANSFORMS += \
	'-n ' \
	'-e "/TOTAL:/p" ' \
	'-e "/SKIP:/p" ' \
	'-e "/PASS:/p" ' \
	'-e "/FAIL:/p" ' \
	'-e "/ERROR:/p" '

# common targets

$(INSTALL_32):	$(INSTALL_64)

build:		$(BUILD_32_and_64)

install:	$(INSTALL_32_and_64)

test:		$(TEST_32_and_64)

REQUIRED_PACKAGES += library/desktop/atk
REQUIRED_PACKAGES += library/desktop/cairo
REQUIRED_PACKAGES += library/desktop/gtk3
REQUIRED_PACKAGES += library/desktop/pango
REQUIRED_PACKAGES += library/glib2
REQUIRED_PACKAGES += library/gnutls-3
REQUIRED_PACKAGES += library/zlib
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/g++-6-runtime
REQUIRED_PACKAGES += system/library/math
