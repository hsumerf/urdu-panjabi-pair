###############################################################################
## Makefile for Urdu--Punjabi
###############################################################################

VERSION=0.1.0
LANG1=urd
LANG2=pan
VAR1=Guru
VAR2=Arab
LANG2g=$(LANG2)_$(VAR1)
LANG2s=$(LANG2)_$(VAR2)
PREFIX1=$(LANG1)-$(LANG2)
PREFIX1g=$(LANG1)-$(LANG2)_$(VAR1)
PREFIX1s=$(LANG1)-$(LANG2)_$(VAR2)
PREFIX2=$(LANG2)-$(LANG1)
PREFIX2g=$(LANG2)_$(VAR1)-$(LANG1)
PREFIX2s=$(LANG2)_$(VAR2)-$(LANG1)

BASENAME=apertium-$(PREFIX1)

TARGETS_COMMON =		\
	$(PREFIX1g).automorf.bin	\
	$(PREFIX1g).autobil.bin	\
	$(PREFIX1g).autolex.bin	\
	$(PREFIX1g).autogen.bin	\
	$(PREFIX1s).automorf.bin	\
	$(PREFIX1s).autobil.bin	\
	$(PREFIX1s).autolex.bin	\
	$(PREFIX1s).autogen.bin	\
	$(PREFIX1).prob		\
	$(PREFIX1).rlx.bin	\
	$(PREFIX1).t1x.bin	\
	$(PREFIX1).t2x.bin	\
	$(PREFIX1).t3x.bin	\
	$(PREFIX2g).automorf.bin	\
	$(PREFIX2g).prob		\
	$(PREFIX2g).autobil.bin	\
	$(PREFIX2g).autolex.bin	\
	$(PREFIX2s).automorf.bin	\
	$(PREFIX2s).prob		\
	$(PREFIX2s).autobil.bin	\
	$(PREFIX2s).autolex.bin	\
	$(PREFIX2).autogen.bin	\
	$(PREFIX2).rlx.bin	\
	$(PREFIX2).t1x.bin	\
	$(PREFIX2).t2x.bin	\
	$(PREFIX2).t3x.bin


# This include defines goals for install-modes, .deps/.d, autobil.prefixes and .mode files:
@ap_include@

###############################################################################
## Monolingual transducers
###############################################################################

# -------------------
# Urdu analysis:
# -------------------

.deps/$(LANG1).automorf.bin: $(AP_SRC1)/$(LANG1).automorf.bin .deps/.d
	cp $< $@

$(PREFIX1g).automorf.bin: .deps/$(LANG1).automorf.bin $(PREFIX1g).autobil.bin
	lt-trim $^ $@

$(PREFIX1s).automorf.bin: .deps/$(LANG1).automorf.bin $(PREFIX1s).autobil.bin
	lt-trim $^ $@

# -------------------
# Urdu generation:
# ---------------------


$(PREFIX2).autogen.bin: $(AP_SRC1)/$(LANG1).autogen.bin
	cp $< $@

# -------------------
# Punjabi analysis:
# -------------------

.deps/$(LANG2g).automorf.bin: $(AP_SRC2)/$(LANG2g).automorf.bin .deps/.d
	cp $< $@

.deps/$(LANG2s).automorf.bin: $(AP_SRC2)/$(LANG2s).automorf.bin .deps/.d
	cp $< $@

$(PREFIX2g).automorf.bin: .deps/$(LANG2g).automorf.bin $(PREFIX2g).autobil.bin
	lt-trim $^ $@

$(PREFIX2s).automorf.bin: .deps/$(LANG2s).automorf.bin $(PREFIX2s).autobil.bin
	lt-trim $^ $@

# -------------------
# Punjabi generation:
# ---------------------


$(PREFIX1g).autogen.bin: $(AP_SRC2)/$(LANG2g).autogen.bin
	cp $< $@

$(PREFIX1s).autogen.bin: $(AP_SRC2)/$(LANG2s).autogen.bin
	cp $< $@

###############################################################################
## Tagger models
###############################################################################

$(PREFIX1).prob: $(AP_SRC1)/$(LANG1).prob
	cp $< $@

$(PREFIX2g).prob: $(AP_SRC2)/$(LANG2g).prob
	cp $< $@

$(PREFIX2s).prob: $(AP_SRC2)/$(LANG2s).prob
	cp $< $@

###############################################################################
## Disambiguation rules
###############################################################################

$(PREFIX1).rlx.bin: $(AP_SRC1)/apertium-$(LANG1).$(LANG1).rlx
	cg-comp $< $@

$(PREFIX2).rlx.bin: $(AP_SRC2)/apertium-$(LANG2).$(LANG2).rlx
	cg-comp $< $@

###############################################################################
## Bilingual dictionaries
###############################################################################

$(PREFIX1g).autobil.bin: $(BASENAME).$(PREFIX1g).dix
	apertium-validate-dictionary $<
	lt-comp lr $< $@

$(PREFIX1s).autobil.bin: $(BASENAME).$(PREFIX1s).dix
	apertium-validate-dictionary $<
	lt-comp lr $< $@

$(PREFIX2g).autobil.bin: $(BASENAME).$(PREFIX1g).dix
	apertium-validate-dictionary $<
	lt-comp rl $< $@

$(PREFIX2s).autobil.bin: $(BASENAME).$(PREFIX1s).dix
	apertium-validate-dictionary $<
	lt-comp rl $< $@

###############################################################################
## Lexical selection rules
###############################################################################

$(PREFIX1g).autolex.bin: $(BASENAME).$(PREFIX1g).lrx
	lrx-comp $< $@

$(PREFIX1s).autolex.bin: $(BASENAME).$(PREFIX1s).lrx
	lrx-comp $< $@

$(PREFIX2g).autolex.bin: $(BASENAME).$(PREFIX2g).lrx
	lrx-comp $< $@

$(PREFIX2s).autolex.bin: $(BASENAME).$(PREFIX2s).lrx
	lrx-comp $< $@

###############################################################################
## Structural transfer rules
###############################################################################

$(PREFIX1).t1x.bin: $(BASENAME).$(PREFIX1).t1x
	apertium-validate-transfer $<
	apertium-preprocess-transfer $< $@

$(PREFIX1).t2x.bin: $(BASENAME).$(PREFIX1).t2x
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX1).t3x.bin: $(BASENAME).$(PREFIX1).t3x
	apertium-validate-postchunk $<
	apertium-preprocess-transfer $< $@


$(PREFIX2).t1x.bin: $(BASENAME).$(PREFIX2).t1x
	apertium-validate-transfer $<
	apertium-preprocess-transfer $< $@

$(PREFIX2).t2x.bin: $(BASENAME).$(PREFIX2).t2x
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX2).t3x.bin: $(BASENAME).$(PREFIX2).t3x
	apertium-validate-postchunk $<
	apertium-preprocess-transfer $< $@

###############################################################################
## Distribution
###############################################################################

EXTRA_DIST=					\
		$(BASENAME).$(PREFIX1).lrx	\
		$(BASENAME).$(PREFIX1).dix	\
		$(BASENAME).$(PREFIX2).lrx	\
		$(BASENAME).$(PREFIX1).t1x	\
		$(BASENAME).$(PREFIX1).t2x	\
		$(BASENAME).$(PREFIX1).t3x	\
		$(BASENAME).$(PREFIX2).t1x	\
		$(BASENAME).$(PREFIX2).t2x	\
		$(BASENAME).$(PREFIX2).t3x	\
		modes.xml

###############################################################################
## Installation
###############################################################################

apertium_urd_pandir=$(prefix)/share/apertium/$(BASENAME)/

# Files which should be installed to $(prefix)/share/apertium/$(BASENAME)/:
apertium_urd_pan_DATA=	\
	$(TARGETS_COMMON)				\
	$(BASENAME).$(PREFIX1).t1x			\
	$(BASENAME).$(PREFIX1).t2x			\
	$(BASENAME).$(PREFIX1).t3x			\
	$(BASENAME).$(PREFIX2).t1x			\
	$(BASENAME).$(PREFIX2).t2x			\
	$(BASENAME).$(PREFIX2).t3x

# All modes are created by the same goal, listing several will just give problems with make -j2
noinst_DATA=modes/$(PREFIX1).mode \
	.deps/$(LANG1).automorf.bin \
	.deps/$(LANG2).automorf.bin

install-data-local: install-modes

###############################################################################
## Cleanup
###############################################################################

CLEANFILES = $(TARGETS_COMMON)
clean-local:
	-rm -rf .deps modes

###############################################################################
## Test
###############################################################################

test: all
	echo "house" | apertium -d . urd-pan | tee .test-mt
	@echo "house" > .test-ref
	@diff .test-ref .test-mt
	echo "house" | apertium -d . pan-urd | tee .test-mt
	@echo "house" > .test-ref
	@diff .test-ref .test-mt
	@rm .test-ref .test-mt

