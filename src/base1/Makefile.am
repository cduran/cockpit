# Mustache is distributed for compat reasons

basedir = $(pkgdatadir)/base1
nodist_base_DATA = \
	dist/base1/cockpit.min.css.gz \
	dist/base1/mustache.min.js.gz \
	dist/base1/jquery.min.js.gz \
	dist/base1/cockpit.min.js.gz \
	$(NULL)
base_DATA = \
	dist/base1/manifest.json \
	$(NULL)

basedebugdir = $(debugdir)$(basedir)
basedebug_DATA = \
	dist/base1/cockpit.min.css.map \
	dist/base1/patternfly.css.map \
	dist/base1/mustache.min.js.map \
	dist/base1/jquery.min.js.map \
	dist/base1/cockpit.min.js.map \
	$(NULL)

AM_TESTS_ENVIRONMENT = export G_DEBUG=fatal-criticals,fatal-warnings ; export XDG_CACHE_HOME=$$(mktemp -d) ; export XDG_RUNTIME_DIR=$$XDG_CACHE_HOME ;

dist/base1/cockpit.min.css: src/base1/cockpit.css
	$(AM_V_GEN) $(MKDIR_P) $(dir $@) && \
	$(srcdir)/tools/missing $(CLEAN_CSS) --keep-line-breaks --output=$@ --inline none --source-map --source-map-inline-sources $^
dist/base1/jquery.js:
	$(AM_V_GEN) $(MKDIR_P) $(dir $@) && \
	cat $(srcdir)/node_modules/jquery/dist/jquery.js $(srcdir)/node_modules/bootstrap/dist/js/bootstrap.js $(srcdir)/node_modules/patternfly/dist/js/patternfly.js > $@.tmp && $(MV) $@.tmp $@
dist/base1/jquery.min.js: dist/base1/jquery.js
	$(MIN_JS_RULE)
dist/base1/cockpit.js: src/base1/cockpit.js
	$(ESLINT_RULE)
	$(COPY_RULE)
dist/base1/cockpit.min.js: dist/base1/cockpit.js
	$(MIN_JS_RULE)
dist/base1/mustache.js: src/base1/deprecated.js
	$(V_COPY) $(MKDIR_P) $(dir $@) && \
	cat $(srcdir)/src/base1/deprecated.js $(srcdir)/node_modules/mustache/mustache.js > $@.tmp && $(MV) $@.tmp $@
dist/base1/mustache.min.js: dist/base1/mustache.js
	$(MIN_JS_RULE)
dist/base1/manifest.json: src/base1/manifest.json
	$(COPY_RULE)


dist/base1/cockpit.min.js.map: dist/base1/cockpit.min.js

dist/base1/jquery.min.js.map: dist/base1/jquery.min.js

dist/base1/mustache.min.js.map: dist/base1/mustache.min.js

dist/base1/cockpit.min.css.map: dist/base1/cockpit.min.css

# PatternFly 3 with hacked CSS to look like PF4 plus the PF4 base
dist/base1/patternfly.css.map: dist/base1/patternfly.css
dist/base1/patternfly.css: src/base1/patternfly-cockpit.scss
	$(AM_V_GEN) $(MKDIR_P) $(dir $@) && \
        $(SASS) $< $@ --source-map \
			--source-map-urls absolute \
			--style compressed \
			--load-path=$(srcdir)/node_modules \
			--load-path=$(srcdir)/node_modules/patternfly/dist/sass \
			--load-path=$(srcdir)/node_modules/bootstrap-sass/assets/stylesheets \
			--load-path=$(srcdir)/node_modules/font-awesome-sass/assets/stylesheets && \
	sed -i -f $(srcdir)/tools/patternfly.sed $@

dist/base1/fonts/fontawesome.woff:
	$(V_COPY) $(MKDIR_P) $(dir $@) && \
	cp $(srcdir)/node_modules/patternfly/dist/fonts/fontawesome-webfont.woff $@.tmp && $(MV) $@.tmp $@
dist/base1/fonts/glyphicons.woff:
	$(V_COPY) $(MKDIR_P) $(dir $@) && \
	cp $(srcdir)/node_modules/patternfly/dist/fonts/glyphicons-halflings-regular.woff $@.tmp && $(MV) $@.tmp $@
dist/base1/fonts/patternfly.woff:
	$(V_COPY) $(MKDIR_P) $(dir $@) && \
	cp $(srcdir)/node_modules/patternfly/dist/fonts/PatternFlyIcons-webfont.woff $@.tmp && $(MV) $@.tmp $@

basefontsdir = $(pkgdatadir)/base1/fonts
basefonts_DATA = \
	dist/base1/fonts/fontawesome.woff \
	dist/base1/fonts/patternfly.woff \
	dist/base1/fonts/glyphicons.woff \
	$(NULL)

# Tests run with QUnit

base_QUNIT_TESTS = \
	dist/base1/test-base64.html \
	dist/base1/test-utf8.html \
	dist/base1/test-events.html \
	dist/base1/test-chan.html \
	dist/base1/test-dbus.html \
	dist/base1/test-dbus-address.html \
	dist/base1/test-echo.html \
	dist/base1/test-spawn.html \
	dist/base1/test-spawn-proc.html \
	dist/base1/test-http.html \
	dist/base1/test-external.html \
	dist/base1/test-location.html \
	dist/base1/test-locale.html \
	dist/base1/test-format.html \
	dist/base1/test-file.html \
	dist/base1/test-metrics.html \
	dist/base1/test-user.html \
	dist/base1/test-machines.html \
	dist/base1/test-permissions.html \
	dist/base1/test-series.html \
	dist/base1/test-cache.html \
	dist/base1/test-websocket.html \
	dist/base1/test-browser-storage.html \
	dist/base1/test-promise.html \
	dist/base1/test-protocol.html \
	$(NULL)

base_QUNIT_DEPS = \
	dist/base1/qunit.css \
	dist/base1/qunit.js \
	dist/base1/test-dbus-common.js \
	src/base1/qunit-template.html \
	src/base1/test-dbus-common.js \
	$(NULL)

dist/base1/qunit.js:
	$(V_COPY) $(MKDIR_P) $(dir $@) && \
	cat $(srcdir)/node_modules/qunit/qunit/qunit.js \
	    $(srcdir)/node_modules/qunit-tap/lib/qunit-tap.js \
            $(srcdir)/pkg/lib/qunit-config.js > $@.tmp && $(MV) $@.tmp $@

dist/base1/qunit.css:
	$(V_COPY) $(MKDIR_P) $(dir $@) && \
	cp $(srcdir)/node_modules/qunit/qunit/qunit.css $@.tmp && $(MV) $@.tmp $@

dist/base1/test-dbus-common.js: src/base1/test-dbus-common.js
	$(ESLINT_RULE)
	$(COPY_RULE)

$(base_QUNIT_TESTS): dist/base1/test-%.html: src/base1/test-%.js $(base_QUNIT_DEPS)
	$(ESLINT_RULE)
	$(AM_V_GEN) $(MKDIR_P) $(dir $@) && \
	cp -L $< $@.tmp.js && $(MV) $@.tmp.js $(dir $@)/$(notdir $<) && \
	$(SED_TEST_TEMPLATE) $(srcdir)/src/base1/qunit-template.html > $@.tmp && $(MV) $@.tmp $@

# Simple tests run without QUnit

base_SIMPLE_TESTS = \
	dist/base1/test-no-jquery.html \
	dist/base1/test-framed-cache.html \
	dist/base1/test-framed.html \
	dist/base1/test-dbus-framed.html \
	$(NULL)

base_SIMPLE_DEPS = \
	dist/base1/simple-tap.js \
	src/base1/simple-template.html \
	src/base1/simple-tap.js \
	$(NULL)

dist/base1/simple-tap.js: src/base1/simple-tap.js
	$(ESLINT_RULE)
	$(COPY_RULE)

$(base_SIMPLE_TESTS): dist/base1/test-%.html: src/base1/test-%.js $(base_SIMPLE_DEPS)
	$(ESLINT_RULE)
	$(AM_V_GEN) $(MKDIR_P) $(dir $@) && \
	cp -L $< $@.tmp.js && $(MV) $@.tmp.js $(dir $@)/$(notdir $<) && \
	$(SED_TEST_TEMPLATE) $(srcdir)/src/base1/simple-template.html > $@.tmp && $(MV) $@.tmp $@

dist/base1/test-%.js: dist/base1/test-%.html
	@true

# A html-webpack-plugin workalike for tests not built by webpack

SED_TEST_TEMPLATE = sed -e 's,[@]TEST[@],$(notdir $<),g'

base_TESTS = $(base_QUNIT_TESTS) $(base_SIMPLE_TESTS)
base_TESTS_DEPS = $(base_QUNIT_DEPS) $(base_SIMPLE_DEPS)
base_TESTS_JAVASCRIPT = $(base_TESTS:.html=.js)
base_TESTS_SOURCE = $(subst dist/,src/,$(base_TESTS_JAVASCRIPT))

TESTS += $(base_TESTS)
noinst_SCRIPTS += $(base_TESTS)

EXTRA_DIST += \
	dist/base1/cockpit.js \
	dist/base1/cockpit.min.css \
	dist/base1/cockpit.min.css.map \
	dist/base1/cockpit.min.js \
	dist/base1/cockpit.min.js.map \
	dist/base1/jquery.js \
	dist/base1/jquery.min.js \
	dist/base1/jquery.min.js.map \
	dist/base1/mustache.js \
	dist/base1/mustache.min.js \
	dist/base1/mustache.min.js.map \
	dist/base1/patternfly.css \
	dist/base1/patternfly.css.map \
	dist/base1/simple-tap.js \
	src/base1/cockpit.css \
	src/base1/cockpit.js \
	src/base1/deprecated.js \
	src/base1/manifest.json \
	src/base1/patternfly-cockpit.scss \
	src/base1/simple-tap.js \
	src/base1/test-dbus-common.js \
	$(base_DATA) \
	$(basefonts_DATA) \
	$(base_TESTS) \
	$(base_TESTS_DEPS) \
	$(base_TESTS_SOURCE) \
	$(base_TESTS_JAVASCRIPT) \
	$(NULL)

MAINTAINERCLEANFILES += \
	dist/base1/cockpit.js \
	dist/base1/cockpit.min.css \
	dist/base1/cockpit.min.css.gz \
	dist/base1/cockpit.min.css.map \
	dist/base1/cockpit.min.js \
	dist/base1/cockpit.min.js.gz \
	dist/base1/cockpit.min.js.map \
	dist/base1/fonts/fontawesome.woff \
	dist/base1/fonts/glyphicons.woff \
	dist/base1/fonts/patternfly.woff \
	dist/base1/jquery.js \
	dist/base1/jquery.min.js \
	dist/base1/jquery.min.js.gz \
	dist/base1/jquery.min.js.map \
	dist/base1/manifest.json \
	dist/base1/mustache.js \
	dist/base1/mustache.min.js \
	dist/base1/mustache.min.js.gz \
	dist/base1/mustache.min.js.map \
	dist/base1/patternfly.css \
	dist/base1/patternfly.css.map \
	dist/base1/qunit.css \
	dist/base1/qunit.js \
	dist/base1/simple-tap.js \
	dist/base1/test-dbus-common.js \
	$(base_TESTS) \
	$(base_TESTS_JAVASCRIPT) \
	$(NULL)
