include default.mk

FEATURE_FILES = $(sort $(wildcard ../ruby/features/*.feature))
FEATURE_NDJSONS = $(patsubst ../ruby/features/%.feature,acceptance/%.ndjson,$(FEATURE_FILES))

.DELETE_ON_ERROR:

.tested: $(FEATURE_NDJSONS) acceptance/all.ndjson

acceptance/all.ndjson: $(FEATURE_FILES)
	mkdir -p $$(dirname $@)
	pushd ../ruby && \
		../javascript/node_modules/fake-cucumber/bin/fake-cucumber \
		--format ndjson \
		--results pattern \
		$(patsubst ../ruby/%,%,$^) > \
		../javascript/$@ && \
		popd

acceptance/test_%.ndjson: ../ruby/features/test_%.feature
	mkdir -p $$(dirname $@)
	pushd ../ruby && \
		../javascript/node_modules/fake-cucumber/bin/fake-cucumber \
		--format ndjson \
		--results pattern \
		$(patsubst ../ruby/%,%,$^) > \
		../javascript/$@ && \
		popd
