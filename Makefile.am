sbin_PROGRAMS = mapper

mapper_SOURCES = libmapper/app.c
mapper_LDFLAGS = $(SYSTEMD_LIBS)
mapper_CFLAGS = $(SYSTEMD_CFLAGS)
mapper_LDADD = libmapper.la

libmapperdir = ${libdir}
libmapper_LTLIBRARIES = libmapper.la
libmapper_la_SOURCES = libmapper/mapper.c
libmapper_la_LDFLAGS = $(SYSTEMD_LIBS) -version-info 1:0:0 -shared
libmapper_la_CFLAGS = $(SYSTEMD_CFLAGS)

include_HEADERS = libmapper/mapper.h

if HAVE_PYTHON

all-local:
	$(AM_V_at)$(PYTHON) ${top_builddir}/setup.py build

clean-local:
	rm -rfv ${top_builddir}/build

install-exec-hook:
	$(AM_V_at)$(PYTHON) ${top_builddir}/setup.py install \
	--prefix=$(DESTDIR)${prefix} \
	--install-data=$(DESTDIR)${datadir} \
	--install-lib=$(DESTDIR)$(PYTHONDIR) \
	--install-scripts=$(DESTDIR)${sbindir} \
	--record=${top_builddir}/python_install.log

uninstall-hook:
	cat ${top_builddir}/python_install.log \
	| $(AWK) '{print "$(DESTDIR)"$$1}' | xargs rm -fv

endif

SUBDIRS = fail-monitor
