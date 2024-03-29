# Bluefish HTML Editor
# Makefile.in - the Makefile template
# Copyright (C) 2002-2006 Olivier Sessink
#
# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 2 of the License, or
# (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA  02110-1301, USA.


SHELL = /bin/sh


PACKAGE = bluefish
VERSION = 1.0.7

srcdir = src

prefix=/local
exec_prefix=${prefix}
bindir=${exec_prefix}/bin
datadir=${datarootdir}
datarootdir = ${prefix}/share
pkgdatadir=$(datadir)/$(PACKAGE)
pixmapsdir=/local/share/pixmaps

INSTALLMAIN= install-nls
MAKEMAIN= make-nls

iconpath=no

INSTALL = /bin/install -c
INSTALL_DIR = $(INSTALL) -d -m 755 
INSTALL_DATA = $(INSTALL) -m 644

#make -C is a GNU extension, BSD make doesn't have it
#use cd dir ; make all instead
#and [ "bla" == "bla" ] does not work on netBSD
#use [ "bla" = "bla" ] instead

bluefish:all
all: ${MAKEMAIN}
	@cd src/ && $(MAKE) all
	@cd data/ && $(MAKE) all
	@cd man/ && $(MAKE) all

make-nls:
	cd po/ && $(MAKE) all;

clean:
	rm -f core *~
	@cd src/ && $(MAKE) clean
	@cd po/ && $(MAKE) clean
	@cd data/ && $(MAKE) clean
	@cd man/ && $(MAKE) clean

patchclean: clean
	rm -f *.orig *.rej
	@cd src/ && $(MAKE) patchclean  

distclean:
	@cd src/ && $(MAKE) distclean
	@cd po/ && $(MAKE) distclean
	@cd data/ && $(MAKE) distclean
	@cd man/ && $(MAKE) distclean
	rm -f Makefile src/Makefile icons/Makefile config.status config.cache config.log
	rm -rf autom4te.cache/
	rm -f *.orig *.rej

install-icon:
	$(INSTALL_DIR) $(DESTDIR)$(iconpath)
	$(INSTALL_DATA) inline_images/bluefish_icon1.png $(DESTDIR)$(iconpath)/bluefish-icon.png

install-nls:
	cd po/ && $(MAKE) install

install: src/bluefish ${INSTALLMAIN}
	pkgdatadir=${datarootdir}/bluefish/
	$(INSTALL_DIR) $(DESTDIR)$(pkgdatadir)
	$(INSTALL_DATA) images/bluefish_splash.png $(DESTDIR)$(pkgdatadir)
	@cd icons/ && $(MAKE) install
	@cd data/ && $(MAKE) install
	@cd man/ && $(MAKE) install
	@cd src/ && $(MAKE) install

uninstall:
	@cd icons/ && $(MAKE) uninstall
	@cd src/ && $(MAKE) uninstall
	@cd po/ && $(MAKE) uninstall
	@cd data/ && $(MAKE) uninstall
	@cd man/ && $(MAKE) uninstall
	rm -f $(pkgdatadir)/bluefish_splash.png
	rm -f $(iconpath)/bluefish-icon.png
	/bin/rmdir $(DESTDIR)$(pkgdatadir)
