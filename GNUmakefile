THISDIR := GAelectrodynamics
THISBOOK := GAelectrodynamics
#BASEVER := 5e8fb49ccd326da795eff23e7bdbbe4792a328e1
export BOOKSUBVER := 1
export BOOKMAJVER := 0
# This isn't a good way to version.  It depends on the local git reflog history count.
export REVCOUNTSTART := 510

include ../latex/make.bookvars

# Override my default:
#MY_CLASSICTHESIS_FRONTBACK_FILES := $(filter-out ../classicthesis_mine/FrontBackmatter/Dedication.tex,$(MY_CLASSICTHESIS_FRONTBACK_FILES))
MY_CLASSICTHESIS_FRONTBACK_FILES := $(filter-out ../classicthesis_mine/FrontBackmatter/Titlepage.tex,$(MY_CLASSICTHESIS_FRONTBACK_FILES))

#ONCEFLAGS := -justonce

SOURCE_DIRS += working
FIGURES := ../$(THISBOOK)-figures
SOURCE_DIRS += $(FIGURES)

PRIMARY_SOURCES := $(shell grep input chapters.tex | sed 's/%.*//;s/.*{//;s/}.*//;')
PRIMARY_SOURCES += FrontBackmatter/preface.tex

#GENERATED_SOURCES += matlab.tex
GENERATED_SOURCES += mathematica.tex
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
ece2500report.pdf :: $(shell cat spellcheckem.txt) reportPreamble.tex

report : ece2500report.pdf
mx : maxwells.pdf

# FIXME: this should be an automatic dependency, but currently isn't.
#$(THISBOOK).pdf :: mmacells.sty

$(THISBOOK).pdf :: $(EXTERNAL_DEPENDENCIES)

#.revinfo/gitCommitDateAsMyTime.tex:\newcommand{\myTime}{April 2018}\newcommand{\myVersion}{version V0.117\xspace}
VER := $(shell grep Version .revinfo/gitCommitDateAsMyTime.tex | sed 's/.*{//;s/.xspace.*//;')

.PHONY: spellcheck
spellcheck: $(patsubst %.tex,%.sp,$(filter-out $(DONT_SPELL_CHECK),$(DO_SPELL_CHECK)))

# enable doublespace before making:
dropbox:
	cp GAelectrodynamics.pdf ~/Dropbox/ECE2500Y/GAelectrodynamics.$(VER).pdf
	git log --decorate > ~/Dropbox/ECE2500Y/Changelog.txt

dist:
	cp GAelectrodynamics.pdf GAelectrodynamics.$(VER).pdf

alex:
	cp GAelectrodynamics.pdf ~/Dropbox/4Alex/GAelectrodynamics.$(VER).pdf
	#cp ece2500report.pdf ~/Dropbox/4Alex/ece2500report.$(VER).pdf
	git log --decorate > ~/Dropbox/4Alex/Changelog.txt

# a for annotate (releases).
tag:
	git tag -a GAelectrodynamics.$(VER).pdf

%.sp : %.tex
	spellcheck $^
	touch $@

.PHONY: copy
copy : $(HOME)/Dropbox/$(THISDIR)/$(THISBOOK).pdf

$(HOME)/Dropbox/$(THISDIR)/$(THISBOOK).pdf : $(THISBOOK).pdf
	cp $^ $@

mmacells/mmacells.sty:
	git clone https://github.com/jkuczm/mmacells

bib:
	rm -f Bibliography.bib myrefs.bib
	make Bibliography.bib myrefs.bib

mmacells.sty: mmacells/mmacells.sty
	cp $^ $@
