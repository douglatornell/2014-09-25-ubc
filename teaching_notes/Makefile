NOTES_PDFS= \
	introduction_notes.pdf \
	Shell_notes.pdf \
	hg_notes.pdf \
	python_notes.pdf

all: $(NOTES_PDFS)

.PHONY: all tidy clean

tidy:
	rm -f *.aux *.log *.nav *.out *.snm *.toc *.vrb

clean: tidy
	rm -f *.pdf

%.pdf: %.tex
	pdflatex $<
