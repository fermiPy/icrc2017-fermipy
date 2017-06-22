filename=proceedings
outname=fermipy_proceedings
tardir=tmpdir
reply=reply

lat=\def\lat{}
arxiv=\def\arxiv{}
aastex=\def\aastex{}
apj=\def\apj{}

figdir=figures
figures=
tables=
files=$(filename).bbl commands.tex aas_macros.sty authors.tex emulateapj.cls

all: arxiv copy

copy: 
	cp $(filename).pdf $(outname).pdf

touch:
	touch ${filename}.tex

lat : flag = ${lat}${aastex}
lat : main 

aastex : flag = ${aastex}
aastex : main

arxiv : flag = ${arxiv} 
arxiv : main 

apj : flag = ${apj} 
apj : main 

main : 
	pdflatex "${flag}\input{${filename}}"
	bibtex ${filename}||true
	pdflatex "${flag}\input{${filename}}"
	pdflatex "${flag}\input{${filename}}"

tar : flag = ${arxiv}
tar : 
	mkdir -p $(tardir)
	printf '%s\n' "${flag}" > $(tardir)/$(filename).tex
	cat $(filename).tex  >> $(tardir)/$(filename).tex
	cp $(files) $(tardir)	
	cp $(tables) $(tardir)
	cp $(figures) $(tardir)
	cp $(filename).pdf $(tardir)/$(outname).pdf
	cd $(tardir) && tar -czf ../$(outname).tar.gz . && cd ..
	rm -rf $(tardir)

reply :
	pdflatex ${reply}
	bibtex ${reply}
	pdflatex ${reply}
	pdflatex ${reply}

arxiv.tgz : flag = ${arxiv}
arxiv.tgz : tar

clean:
	rm -f *.ps ${filename}.pdf *.log *.aux *.out *.dvi *.bbl *.blg *Notes.bib *.synctex.gz


