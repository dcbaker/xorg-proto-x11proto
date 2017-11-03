SUBDIRS=specs

xprotodir = $(includedir)/X11
xproto_HEADERS = \
	include/X11/ap_keysym.h \
	include/X11/DECkeysym.h \
	include/X11/HPkeysym.h \
	include/X11/keysymdef.h \
	include/X11/keysym.h \
	include/X11/Sunkeysym.h \
	include/X11/Xalloca.h \
	include/X11/Xarch.h \
	include/X11/Xatom.h \
	include/X11/Xdefs.h \
	include/X11/XF86keysym.h \
	include/X11/Xfuncs.h \
	include/X11/X.h \
	include/X11/Xmd.h \
	include/X11/Xosdefs.h \
	include/X11/Xos.h \
	include/X11/Xos_r.h \
	include/X11/Xproto.h \
	include/X11/Xprotostr.h \
	include/X11/Xthreads.h \
	include/X11/Xw32defs.h \
	include/X11/XWDFile.h \
	include/X11/Xwindows.h \
	include/X11/Xwinsock.h

nodist_xproto_HEADERS = \
	Xfuncproto.h \
	Xpoll.h

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = xproto.pc


MAINTAINERCLEANFILES = ChangeLog INSTALL

.PHONY: ChangeLog INSTALL

INSTALL:
	$(INSTALL_CMD)

ChangeLog:
	$(CHANGELOG_CMD)

dist-hook: ChangeLog INSTALL

