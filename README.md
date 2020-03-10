# Programming in Tabled Prolog (very) DRAFT

This repository contains the LaTeX sources  for   a  book with the above
title written by David S. Warren. Please take care of this notice:

> This is a very early draft made available privately for those who
> might find it of interest. I reserve all rights to this work. -dsw

To compile `book.pdf`, run

    latex book
    bibtex book
    latex book
    latex book
    dvipdf book

(The `pdflatex` command doesn't properly handle the `eps` figures, so
`latex` + `dvipdf` is used instead.)

To remove the generated files: `git clean -fxd`

If you're on Ubuntu or similar Linux system, these packages should
suffice:

    texlive-latex-base
    texlive-fonts-recommended
    texlive-fonts-extra
    texlive-latex-extra
    texlive-bibtex-extra

The `*.fig` files can be opened using `xfig` from package `xfig`; they
can be translated into various formats using package `fig2dev`; the
`*.eps` files can be viewed using `gio open`, `gv`, `evince`, or
`gimp`.

The following files exist only as `.eps`:

    figures/retr.eps
    figures/small-winbtree.eps
    figures/slg_forest.eps
    figures/terry4.eps
    figures/Completion.1.eps
    figures/xsb-logo.eps
    figures/blacken.eps
    figures/join_in_prolog.eps
    figures/call-dep.eps.eps
    figures/Completion.3.eps
    figures/Completion.2.eps
    figures/dep-graph.eps
    figures/CDG.1.eps
    figures/sld-append1.eps
    figures/opt-of-algo.eps
    figures/slide1.eps
    figures/terry5.eps

The other `.eps` files can be created using this command:

    find . -name '*.fig' | sed 's/\.fig$//' | xargs -L1 -I '{}' fig2dev -L eps '{}.fig' '{}.eps'

## Preface

By _Jan Wielemaker_

Tabled logic programming was invented by David and has since been copied
by various Prolog systems and extended in   several directions in XSB to
deal with scalability and soundness.  Sponsored   by  Kyndi and with the
help of David and Theresa Swift a large  part of XSB tabling support has
been ported on top of SWI-Prologs   delimited continuation based tabling
engine created by Benoit Desouter and Tom Schrijvers.

Effective programming using  tabled  Prolog   is  quite  different  from
traditional Prolog programming. For  example,   a  transitive closure in
normal Prolog is typically written as below, possibly extended with loop
detection if it is not known that the graph is _acyclic_.

    reachable(X, X).
    reachable(X, Z) :-
        reachable(X, Y),
        reachable(Y, Z).

While this definition works as expected   with `:- table reachable/2.`
without the need for additional loop detection, the following definition
is much better suited for use with tabling:

    :- table reachable/2.

    reachable(X, Z) :-
        reachable(X, Y).
        reachable(Y, Z).
    reachable(X, X).

The reason for this is  that  both   in  the  modes `reachable(-,-)` and
`reachable(+,-)` only a single table is created  instead one for node in
the graph.

It took me a while to  figure  this   out.  This  text by David contains
insights in how to tabling can be used efficiently.

## Beyond this draft

David has made  this  source  available  with   the  intend  to  get  it
translated into a community maintained (Wiki)   text  on applying tabled
logic programming.   Making the source accessible is the first step.
