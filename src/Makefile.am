## $Id: Makefile.am 1.55 06/05/07 17:37:11+03:00 anttit@tcs.hut.fi $
## Process this file with automake to produce Makefile.in

AM_CFLAGS = -Wall -Wextra -Wpointer-arith -Wreturn-type -pedantic -std=gnu99
AM_CPPFLAGS = -isystem $(top_srcdir)/include
AM_YFLAGS = -d

defpath.h: $(top_builddir)/config.h
	echo "#define DEFAULT_CONFIG_FILE \"$(sysconfdir)/mip6d.conf\"" > $@

pmgr.c: mk-pmgr_c.sh pmgr.c.in policy.h
	sh mk-pmgr_c.sh

pmgr.h: mk-pmgr_h.sh pmgr.h.in policy.h
	sh mk-pmgr_h.sh

BUILT_SOURCES = defpath.h pmgr.c pmgr.h
EXTRA_DIST = mk-pmgr_c.sh mk-pmgr_h.sh pmgr.c.in pmgr.h.in

sbin_PROGRAMS = mip6d

mip6d_SOURCES = pmgr.c pmgr.h defpath.h \
		main.c vars.c mipv6.h \
		conf.c conf.h conf_reload.c \
		gram.y scan.l \
		tqueue.c tqueue.h \
		icmp6.c icmp6.h \
		list.h util.c util.h \
		hash.c hash.h \
		debug.c debug.h \
		dhaad_ha.c dhaad_ha.h \
		dhaad_mn.c dhaad_mn.h \
		ndisc.c ndisc.h \
		mh.c mh.h \
		mn.c mn.h \
		bul.c bul.h \
		bcache.c bcache.h \
		retrout.c retrout.h \
		mpdisc_ha.c mpdisc_ha.h \
		mpdisc_mn.c mpdisc_mn.h \
		tunnelctl.c tunnelctl.h \
		rtnl.c rtnl.h \
		ha.c ha.h \
		cn.c cn.h \
		keygen.c keygen.h \
		movement.c movement.h \
		policy.c policy.h \
		xfrm.c xfrm.h \
		proc_sys.c proc_sys.h \
		prefix.c prefix.h \
		ipsec.c ipsec.h \
		statistics.h

if ENABLE_VT
mip6d_SOURCES += vt.c vt.h
endif

if BUILTIN_CRYPTO
mip6d_SOURCES += crypto.c crypto.h
endif

mip6d_LDADD = 

if MISSING
mip6d_LDADD += -L$(top_builddir)/libmissing -lmissing
endif

if LOCAL_NETLINK
mip6d_LDADD += -L$(top_builddir)/libnetlink -lnetlink
endif

noinst_HEADERS = $(top_srcdir)/include/netinet/icmp6.h \
		 $(top_srcdir)/include/netinet/in.h \
		 $(top_srcdir)/include/netinet/ip6.h \
		 $(top_srcdir)/include/netinet/ip6mh.h \
		 $(top_srcdir)/include/linux/xfrm.h

CLEANFILES = gram.c gram.h \
	     pmgr.c pmgr.h \
	     scan.c

DISTCLEANFILES = $(BUILT_SOURCES)
MAINTAINERCLEANFILES = Makefile.in
