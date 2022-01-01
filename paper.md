---
title: 'VPsearch: fast exact sequence similarity search for genomic sequences'
tags:
  - python
  - genomics
  - bioinformatics
authors:
  - name: Joris Vankerschaver
    orcid: 0000-0002-5813-5659
    affiliation: "1, 2"
  - name: Steven J. Kern
    affiliation: 3
  - name: Robert Kern
    affiliation: 3
affiliations:
 - name: Center for Biosystems and Biotech Data Analysis, Ghent University Global Campus, Republic of Korea
   index: 1
 - name: Department of Applied Mathematics, Computer Science and Statistics, Ghent University, Belgium
   index: 2
 - name: Enthought Inc., 200 W Cesar Chavez, Austin, TX 78701, United States
   index: 3
date: 1 January 2022
bibliography: paper.bib

---

# Summary

Similarity search, finding an approximate match from a database of known
nucleotide sequences given an unknown query sequence, is a central task in the
taxonomic determination and functional understanding of newly sequenced
organisms. As databases of known, curated sequences and the number of unknown
sequences continue to grow exponentially, tools that can organize genomic data
at scale and make it efficiently accessible are of fundamental importance.

Over the years, a number of tools for similarity search have improved upon
BLAST [@1990-blast] in terms of lookup speed and accuracy. Some of these, such as the FASTA
tool suite 


(\cite{2016-pearson-FindingProteinNucleotide}), provide rapid
protein or nucleotide similarity search based on sequence content
alone. Others, such as the RDP classifier
(\cite{2007-wang-NaiveBayesianClassifier}) for microbiome analysis, take
taxonomic information or other domain-specific information into account to
improve classification sensitivity or to provide additional confidence
measures. For whole-genome sequences, data structures for approximate
similarity search have been adopted to improve sequence lookup speed
(\cite{2019-marcais-SketchingSublinearData}).


`[@1990-blast]`

# Statement of need

In this paper we present VPsearch, a light-weight Python package and
command-line tool to organize nucleotide sequences into a so-called
\emph{vantage point tree} (\cite{1991-uhlmann-SatisfyingGeneralProximity},
\cite{1993-yianilos-DataStructuresAlgorithms}). This data structure allows for
similarity searches that use a number of lookups proportional to the logarithm
of the size of the database (rather than scanning through the database in
linear fashion), and hence greatly speeds up similarity search queries. We show
that for short sequences (such as the 16S rRNA gene used in bacterial
classification) VPsearch outperforms both BLAST (7x speedup) and ggsearch36
from the FASTA suite (27x speedup) without any loss in accuracy.

The VPsearch tool is implemented in Python, using Cython for performance-critical sections.
It outputs similarity search results in the ``BLAST-6''
tabular format used by BLAST, Diamond, the FASTA tool suite and others, so that
VPsearch can be used as a drop-in replacement for any of these tools. VPsearch
is able to return the $k$ most similar sequences for a given query, not just
the most similar match, and is fully multithreaded.

# Citations

Citations to entries in paper.bib should be in
[rMarkdown](http://rmarkdown.rstudio.com/authoring_bibliographies_and_citations.html)
format.

If you want to cite a software repository URL (e.g. something on GitHub without a preferred
citation) then you can do it with the example BibTeX entry below for @fidgit.

For a quick reference, the following citation commands can be used:
- `@author:2001`  ->  "Author et al. (2001)"
- `[@author:2001]` -> "(Author et al., 2001)"
- `[@author1:2001; @author2:2001]` -> "(Author1 et al., 2001; Author2 et al., 2002)"

# Figures

Figures can be included like this:
![Caption for example figure.\label{fig:example}](figure.png)
and referenced from text using \autoref{fig:example}.

Figure sizes can be customized by adding an optional second parameter:
![Caption for example figure.](figure.png){ width=20% }

# Acknowledgements


# References


