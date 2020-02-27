# Programming in Tabled Prolog (very) DRAFT

This repository contains the LaTeX sources  for   a  book with the above
title written by David S. Warren. Please take care of the notice

> This is a very early draft made available privately for those who
> might find it of interest. I reserve all rights to this work. -dsw

To compile `book.pdf`, run

    pdflatex book
    bibtex book
    pdflatex book
    pdflatex book

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

```
reachable(X, X).
reachable(X, Z) :-
    reachable(X, Y),
    reachable(Y, Z).
```

While this definition works as expected   with ``:- table reachable/2.``
without the need for additional loop detection, the following definition
is much better suited for use with tabling:

```
:- table reachable/2.

reachable(X, Z) :-
    reachable(X, Y).
    reachable(Y, Z).
reachable(X, X).
```

The reason for this is  that  both   in  the  modes `reachable(-,-)` and
`reachable(+,-)` only a single table is created  instead one for node in
the graph.

It took me a while to  figure  this   out.  This  text by David contains
insights in how to tabling can be used efficiently.

## Beyond this draft

David has made  this  source  available  with   the  intend  to  get  it
translated into a community maintained (Wiki)   text  on applying tabled
logic programming.   Making the source accessible is the first step.
