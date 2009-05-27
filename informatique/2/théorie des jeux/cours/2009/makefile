all: pdf html ps

pdf: latex
	pdflatex cours.latex
ps: latex
	pslatex cours.latex
html: cours.rst
	rst2html cours.rst
slide: cours.rst
	rst2s5 cours.rst
latex: cours.rst
	rst2latex cours.rst > cours.latex