SHELL    = /bin/bash
LATEX    = xelatex
BIBTEX   = bibtex
DVIPS    = dvips


BASENAME = syllabus

default: latex

latex:
	xelatex  ${BASENAME} &&  \
	xelatex  ${BASENAME}
	if [ $(shell grep -c citation syllabus.aux) -gt 0 ] ; then bibtex syllabus; else echo "Skipping bibliography - no citations." ; fi
	if [ $(shell grep -c citation syllabus.aux) -gt 0 ] ; then bibtex syllabus; else echo "Skipping bibliography - no citations." ; fi
	xelatex  ${BASENAME} &&  \
	xelatex  ${BASENAME} &&  \
	xelatex  ${BASENAME}
final: latex
	/usr/bin/gs -o ${BASENAME}-final.pdf -dPDFSETTINGS=/prepress -sDEVICE=pdfwrite ${BASENAME}.pdf


#
# standard Latex targets
#

%.dvi:	%.tex
	$(LATEX) $<

%.bbl:	%.tex *.bib
	$(LATEX) $*
	$(BIBTEX) $*

%.ps:	%.dvi
	$(DVIPS) $< -o $@

%.pdf:	%.tex
	$(PDFLATEX) $<

.PHONY: clean

clean:
	rm -f *.aux *.log *.bbl *.blg *.brf *.cb *.ind *.idx *.ilg  \
	      *.inx *.dvi *.toc *.ptc *.out *.synctex.gz *~ ~* spellTmp

realclean: clean
	rm -f syllabus.pdf
