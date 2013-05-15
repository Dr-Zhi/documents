# set file to the name of the main file without the .tex
target	= CV-Yanling
gabbage	= *~ $(target).{out,log,aux,lot,toc,bbl,blg,xdv,log}
files	= $(shell ls *.*)
tmp     = $(target).test
face	= face.jpg

VIEWER	= Skim
TEX 	= pdflatex
BIBTEX  = bibtex
DVI		= xdvipdfmx

#===============================================

default: pdf

all: tarball show

face:
	convert $(face) -compress jpeg eps2:face.eps

pdf:	
	$(TEX) -no-pdf $(target)
	#$(BIBTEX) $(target)
	$(TEX) $(target)
	-make clean
	#$(DVI) -s 1 $(target).xdv && rm $(target).xdv

$(target).tar.gz : $(files)
	tar -czvf $(target).tar.gz $(files)

tarball: $(target).tar.gz

show: pdf
	$(VIEWER) $(target).pdf &

clean:
	-rm -f $(gabbage)

test:
	cp $(target).tex $(tmp).tex
	#sed 's|^\(.*usepackage.*\)|\1\n\\usepackage{syntonly}\n\\syntaxonly|' \
	#			$(target).tex > $(tmp).tex
	$(TEX) -no-pdf $(tmp).tex || echo " :: TeX compile failed!!" ;
	@echo " :: Syntax test finish."
	-@rm -f $(tmp).*


