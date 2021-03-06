PACKAGE_STRING = "/src/extfs-helpers-listcmd"

AM_CPPFLAGS = $(GLIB_CFLAGS) -I$(top_srcdir)

# This lets mc_parse_ls_l.c override MC's message() without the linker
# complaining about multiple definitions.
AM_LDFLAGS = @TESTS_LDFLAGS@

LIBS = $(top_builddir)/lib/libmc.la

# Programs/scripts to build on 'make check'.
check_PROGRAMS = mc_parse_ls_l
check_SCRIPTS = run

# Tests to run on 'make check'
TESTS = run

# On 'make clean', delete 'run' as well.
CLEANFILES = run

mc_parse_ls_l_SOURCES = \
	mc_parse_ls_l.c

data_files_to_distribute = \
	data/lslR.1.spaces.args \
	data/lslR.1.spaces.input \
	data/lslR.1.spaces.output \
	data/lslR.2.spaces-iso.args \
	data/lslR.2.spaces-iso.input \
	data/lslR.2.spaces-iso.output \
	data/lslR.3.spaces-iso-noslash.args \
	data/lslR.3.spaces-iso-noslash.input \
	data/lslR.3.spaces-iso-noslash.output \
	data/lslR.README \
	data/urar.README \
	data/urar.v4,v3.env_vars \
	data/urar.v4,v3.input \
	data/urar.v4,v3.output \
	data/urar.v5.env_vars \
	data/urar.v5.input \
	data/urar.v5.output \
	data/uzip.README \
	data/uzip.with-zipinfo.env_vars \
	data/uzip.with-zipinfo.input \
	data/uzip.with-zipinfo.output \
	data/uzip.without-zipinfo--mdy.env_vars \
	data/uzip.without-zipinfo--mdy.input \
	data/uzip.without-zipinfo--mdy.output \
	data/uzip.without-zipinfo--ymd.env_vars \
	data/uzip.without-zipinfo--ymd.input \
	data/uzip.without-zipinfo--ymd.output \
	data/uzoo.README \
	data/uzoo.input \
	data/uzoo.output \
	data/dummy

EXTRA_DIST = mc_xcat test_all $(data_files_to_distribute)

run:
	echo '#!/bin/sh' > $@
	echo >> $@
	echo '# This script is an easy way to launch the "test_all" script' >> $@
	echo '# with all the required arguments.' >> $@
	echo '#' >> $@
	echo '# Run this script with "--help" to learn more.' >> $@
	echo >> $@
	echo '# Where to find mc_parse_ls_l and mc_xcat, respectively.' >> $@
	echo 'PATH="$(abs_builddir):$(abs_srcdir):$$PATH"' >> $@
	echo >> $@
# The 'abs_' isn't mandatory. It lets you move this script out of the build tree.
	echo '"$(abs_srcdir)"/test_all "$$@" \' >> $@
	echo '  --data-dir "$(abs_srcdir)/data" \' >> $@
# Before installation, some helpers are in the build tree, some in the src tree.
	echo '  --helpers-dir "$(abs_top_builddir)/src/vfs/extfs/helpers" \' >> $@
	echo '  --helpers-dir "$(abs_top_srcdir)/src/vfs/extfs/helpers"' >> $@
	chmod +x $@
# (We can alternatively create run from a run.in template
# with 'AC_CONFIG_FILES[run, chmod +x run]'.)

#
# Documentation
#

doc: README.html

# (Thanks to VPATH we don't need to write "$(srcdir)/README". doc/hlp/Makefile.am needlessly does this.)
README.html: README
	pandoc --include-in-header=$(srcdir)/README.css.inc -N --old-dashes --toc --standalone -o $@ $<

EXTRA_DIST += README.css.inc
CLEANFILES += README.html
