#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL"). You may
# only use this file in accordance with the terms of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source. A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright 2011, 2013, EveryCity Ltd. All rights reserved.
# Copyright 2016, Adam Stevko, All rights reserved.
#

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		nasm
COMPONENT_VERSION=	2.13.01
COMPONENT_FMRI=	developer/assembler/nasm
COMPONENT_SUMMARY=	The Netwide Assembler
COMPONENT_CLASSIFICATION=	Development/Other Languages
COMPONENT_PROJECT_URL=	http://www.nasm.us/
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH=	\
  sha256:0cd4327b114e459a84717260fad4238b445d3511cf0341249072204867698e09
COMPONENT_ARCHIVE_URL= \
  http://www.nasm.us/pub/nasm/releasebuilds/$(COMPONENT_VERSION)/$(COMPONENT_ARCHIVE)
COMPONENT_LICENSE=	BSD

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/configure.mk
include $(WS_MAKE_RULES)/ips.mk

IPS_COMPONENT_VERSION=	2.13.1

CFLAGS+="-I$(BUILD_DIR_$(BITS))"

CONFIGURE_BINDIR.64 = $(CONFIGURE_BINDIR.32)

COMPONENT_POST_CONFIGURE_ACTION += (mkdir -p $(BUILD_DIR_64)/lib)

COMPONENT_INSTALL_ENV += INSTALLROOT="$(PROTO_DIR)"

build:		$(BUILD_64)

install:	$(INSTALL_64)

test:	$(NO_TESTS)

# Auto-generated dependencies
REQUIRED_PACKAGES += system/library
