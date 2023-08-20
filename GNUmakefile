THISDIR := GAelectrodynamics
THISBOOK := GAelectrodynamics

BIBLIOGRAPHY_PATH := classicthesis_mine
HAVE_OWN_CONTENTS := 1
HAVE_OWN_TITLEPAGE := 1
MY_CLASSICTHESIS_FRONTBACK_FILES += ../latex/classicthesis_mine/FrontBackmatter/Index.tex
MY_CLASSICTHESIS_FRONTBACK_FILES += ../latex/classicthesis_mine/FrontBackmatter/ContentsAndFigures.tex
BOOKTEMPLATE := ../latex/classicthesis_mine/ClassicThesis2.tex

include make.revision
include ../latex/make.bookvars

#ONCEFLAGS := -justonce

SOURCE_DIRS += working

# comment this out for online pdf version (uncomment for KDP)
#PRINT_VERSION := 1

#SUBFIGDIR := bw
#ifndef SUBFIGDIR
#SUBFIGDIR := color
#endif

ifdef KINDLE_VERSION
PARAMS += --kindle
endif

ifdef PRINT_VERSION
SUBFIGDIR := bw
else
SUBFIGDIR := color
endif

ifndef PRINT_VERSION
PARAMS += --no-print
endif
PARAMS += -subfig $(SUBFIGDIR)
DISTEXTRA := $(SUBFIGDIR)
ifdef PRINT_VERSION
DISTEXTRA := $(DISTEXTRA).kdp
endif

FIGURES += ../figures/$(THISBOOK)/$(SUBFIGDIR)
FIGURES += ../figures/$(THISBOOK)
SOURCE_DIRS += $(FIGURES)

PRIMARY_SOURCES := $(shell grep input chapters.tex | sed 's/%.*//;s/.*{//;s/}.*//;')
PRIMARY_SOURCES += FrontBackmatter/preface.tex

#GENERATED_SOURCES += matlab.tex
GENERATED_SOURCES += mathematica.tex
#GENERATED_SOURCES += julia.tex
GENERATED_SOURCES += backmatter.tex

EPS_FILES := $(foreach dir,$(FIGURES),$(wildcard $(dir)/*.eps))
PDFS_FROM_EPS := $(subst eps,pdf,$(EPS_FILES))
#$(error PDFS_FROM_EPS $(PDFS_FROM_EPS))

THISBOOK_DEPS += $(PDFS_FROM_EPS)
#THISBOOK_DEPS += macros_mathematica.sty

CLEAN_TARGETS += *.sp FrontBackmatter/*.sp

DO_SPELL_CHECK := $(shell cat spellcheckem.txt)

KINDLE := gaee-kindle

include ../latex/make.rules

$(THISBOOK).pdf :: parameters.sty
#all :: $(THISBOOK).pdf
#all :: ellipticalWaves.pdf
#all :: junk.pdf
#all :: maxwells.pdf
integration.pdf :: $(shell cat spellcheckem.txt)
maxwells.pdf :: $(shell cat spellcheckem.txt)
ece2500report.pdf :: $(shell cat spellcheckem.txt) reportPreamble.tex

report : ece2500report.pdf
mx : maxwells.pdf
ii : integration.pdf
gp : geometricproduct.pdf
#lp : lineAndPlane.pdf
lp : subspaceDistance.pdf

eps:
	@echo $(EPS_FILES)

pdfeps:
	@echo $(PDFS_FROM_EPS)

eps2pdf: $(PDFS_FROM_EPS)

# FIXME: this should be an automatic dependency, but currently isn't.
#$(THISBOOK).pdf :: mmacells.sty

#$(THISBOOK).pdf :: classicthesis.sty $(EXTERNAL_DEPENDENCIES)
$(THISBOOK).pdf :: $(EXTERNAL_DEPENDENCIES)

.PHONY: spellcheck
spellcheck: $(patsubst %.tex,%.sp,$(filter-out $(DONT_SPELL_CHECK),$(DO_SPELL_CHECK)))

dropbox: $(HOME)/Dropbox/Review/$(THISBOOK).$(VER).pdf

$(HOME)/Dropbox/Review/$(THISBOOK).$(VER).pdf : $(THISBOOK).$(VER).pdf
	cp $(THISBOOK).pdf ~/Dropbox/Review/$(THISBOOK).$(VER).pdf
	git log --decorate > ~/Dropbox/Review/Changelog.txt

#alex:
#	cp $(THISBOOK).pdf ~/Dropbox/4Alex/$(THISBOOK).$(VER).pdf
#	#cp ece2500report.pdf ~/Dropbox/4Alex/ece2500report.$(VER).pdf
#	git log --decorate > ~/Dropbox/4Alex/Changelog.txt

%.sp : %.tex
	spellcheck $^
	touch $@

#classicthesis.sty: ../latex/classicthesis/classicthesis.sty
#	cp ../latex/classicthesis/classicthesis.sty .

#.PHONY: copy
#copy : $(HOME)/Dropbox/$(THISDIR)/$(THISBOOK).pdf
#
#$(HOME)/Dropbox/$(THISDIR)/$(THISBOOK).pdf : $(THISBOOK).pdf
#	cp $^ $@

mmacells/mmacells.sty:
	git clone https://github.com/jkuczm/mmacells

bib:
	rm -f Bibliography.bib myrefs.bib
	make Bibliography.bib myrefs.bib

mmacells.sty: mmacells/mmacells.sty
	cp $^ $@

# hack for: HAVE_OWN_TITLEPAGE
clean :: kclean
	git checkout FrontBackmatter/Titlepage.tex

kclean ::
	#rm -f *.html # clobbers Changelog.html
	rm -f *.idx *.4ct *.aux *.xref *.4tc *.dvi *.log *.ncx *.lg *.idv *.tmp *.css *.epub
	rm -f *.bbl *.blg *.brf *.fdb_latexmk *.fls *.ilg *.ind *.lof *.out *.synctex.gz *.toc
	rm -f *.aux */*.aux
	rm -f $(KINDLE)*.html
	rm -f $(KINDLE)*svg content.opf
	rm -rf $(KINDLE)-epub $(KINDLE)-mobi
	rm -rf $(KINDLE)-conversionLog.csv
	git checkout README.md

kindle:
	#tex4ebook -s -f mobi -e build.mk4 $(KINDLE).tex
	#tex4ebook -s $(KINDLE).tex
	tex4ebook -s -f mobi $(KINDLE).tex
	#tex4ebook -s -e build.mk4 $(KINDLE).tex
	#tex4ebook -s -e build_factor.mk4 $(KINDLE).tex
	#tex4ebook -s $(KINDLE).tex
	#tex4ebook -s -f mobi -e kbuild.mk4 $(KINDLE).tex

backmatter.tex: ../latex/classicthesis_mine/backmatter2.tex
	rm -f $@
	ln -s ../latex/classicthesis_mine/backmatter2.tex backmatter.tex
