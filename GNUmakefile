THISDIR := GAelectrodynamics
THISBOOK := GAelectrodynamics

include ../latex/make.bookvars

# Override my default:
#MY_CLASSICTHESIS_FRONTBACK_FILES := $(filter-out ../classicthesis_mine/FrontBackmatter/Dedication.tex,$(MY_CLASSICTHESIS_FRONTBACK_FILES))

#ONCEFLAGS := -justonce

SOURCE_DIRS += working
FIGURES := ../$(THISBOOK)-figures
SOURCE_DIRS += $(FIGURES)

PRIMARY_SOURCES := $(shell grep input chapters.tex | sed 's/%.*//;s/.*{//;s/}.*//;')
PRIMARY_SOURCES += FrontBackmatter/preface.tex

#GENERATED_SOURCES += matlab.tex 
#GENERATED_SOURCES += mathematica.tex 
#GENERATED_SOURCES += julia.tex 

EPS_FILES := $(wildcard $(FIGURES)/*.eps)
PDFS_FROM_EPS := $(subst eps,pdf,$(EPS_FILES))
#$(error PDFS_FROM_EPS $(PDFS_FROM_EPS))

THISBOOK_DEPS += $(PDFS_FROM_EPS)
#THISBOOK_DEPS += macros_mathematica.sty

CLEAN_TARGETS += *.sp FrontBackmatter/*.sp

DO_SPELL_CHECK := $(shell cat spellcheckem.txt)

include ../latex/make.rules

#all :: $(THISBOOK).pdf
#all :: ellipticalWaves.pdf
#all :: junk.pdf
#all :: maxwells.pdf
maxwells.pdf :: $(shell cat spellcheckem.txt)
#maxwells.pdf :: ../frequencydomain/frequencydomainMaxwells.tex

#greens.pdf :: gradientGreensFunctionEuclidean.tex

$(THISBOOK).pdf :: $(EXTERNAL_DEPENDENCIES)

VER := $(shell grep Version .revinfo/lastCommitBook.tex | sed 's/Version //')

.PHONY: spellcheck
spellcheck: $(patsubst %.tex,%.sp,$(filter-out $(DONT_SPELL_CHECK),$(DO_SPELL_CHECK)))

# enable doublespace before making:
dropbox:
	cp GAelectrodynamics.pdf ~/Dropbox/ECE2500Y/GAelectrodynamics.V$(VER).pdf
	cp Changelog.txt ~/Dropbox/ECE2500Y/
	#cp maxwells.pdf ~/Dropbox/ECE2500Y/multivector.pdf

%.sp : %.tex
	spellcheck $^
	touch $@

.PHONY: copy
copy : $(HOME)/Dropbox/$(THISDIR)/$(THISBOOK).pdf

$(HOME)/Dropbox/$(THISDIR)/$(THISBOOK).pdf : $(THISBOOK).pdf
	cp $^ $@
