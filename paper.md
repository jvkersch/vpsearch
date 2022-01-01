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
#bibliography: paper.bib

---

# Summary

The forces on stars, galaxies, and dark matter under external gravitational
fields lead to the dynamical evolution of structures in the universe. The orbits
of these bodies are therefore key to understanding the formation, history, and
future state of galaxies. The field of "galactic dynamics," which aims to model
the gravitating components of galaxies to study their structure and evolution,
is now well-established, commonly taught, and frequently used in astronomy.
Aside from toy problems and demonstrations, the majority of problems require
efficient numerical tools, many of which require the same base code (e.g., for
performing numerical orbit integration).


Similarity search, \emph{i.e.} finding an approximate match from a database of
known nucleotide sequences given an unknown query sequence, is a central task
in the taxonomic determination and functional understanding of newly sequenced
organisms. As databases of known, curated sequences and the number of unknown
sequences continue to grow exponentially, tools that can organize genomic data
at scale and make it efficiently accessible are of fundamental importance.

Over the years, a number of tools for similarity search have improved upon
BLAST in terms of lookup speed and accuracy. Some of these, such as the FASTA
tool suite (\cite{2016-pearson-FindingProteinNucleotide}), provide rapid
protein or nucleotide similarity search based on sequence content
alone. Others, such as the RDP classifier
(\cite{2007-wang-NaiveBayesianClassifier}) for microbiome analysis, take
taxonomic information or other domain-specific information into account to
improve classification sensitivity or to provide additional confidence
measures. For whole-genome sequences, data structures for approximate
similarity search have been adopted to improve sequence lookup speed
(\cite{2019-marcais-SketchingSublinearData}).


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

We acknowledge contributions from Brigitta Sipocz, Syrtis Major, and Semyeong
Oh, and support from Kathryn Johnston during the genesis of this project.

# References
Example paper.bib file:

@article{Pearson:2017,
  	url = {http://adsabs.harvard.edu/abs/2017arXiv170304627P},
  	Archiveprefix = {arXiv},
  	Author = {{Pearson}, S. and {Price-Whelan}, A.~M. and {Johnston}, K.~V.},
  	Eprint = {1703.04627},
  	Journal = {ArXiv e-prints},
  	Keywords = {Astrophysics - Astrophysics of Galaxies},
  	Month = mar,
  	Title = {{Gaps in Globular Cluster Streams: Pal 5 and the Galactic Bar}},
  	Year = 2017
}

@book{Binney:2008,
  	url = {http://adsabs.harvard.edu/abs/2008gady.book.....B},
  	Author = {{Binney}, J. and {Tremaine}, S.},
  	Booktitle = {Galactic Dynamics: Second Edition, by James Binney and Scott Tremaine.~ISBN 978-0-691-13026-2 (HB).~Published by Princeton University Press, Princeton, NJ USA, 2008.},
  	Publisher = {Princeton University Press},
  	Title = {{Galactic Dynamics: Second Edition}},
  	Year = 2008
}

@article{gaia,
    author = {{Gaia Collaboration}},
    title = "{The Gaia mission}",
    journal = {Astronomy and Astrophysics},
    archivePrefix = "arXiv",
    eprint = {1609.04153},
    primaryClass = "astro-ph.IM",
    keywords = {space vehicles: instruments, Galaxy: structure, astrometry, parallaxes, proper motions, telescopes},
    year = 2016,
    month = nov,
    volume = 595,
    doi = {10.1051/0004-6361/201629272},
    url = {http://adsabs.harvard.edu/abs/2016A%26A...595A...1G},
}

@article{astropy,
    author = {{Astropy Collaboration}},
    title = "{Astropy: A community Python package for astronomy}",
    journal = {Astronomy and Astrophysics},
    archivePrefix = "arXiv",
    eprint = {1307.6212},
    primaryClass = "astro-ph.IM",
    keywords = {methods: data analysis, methods: miscellaneous, virtual observatory tools},
    year = 2013,
    month = oct,
    volume = 558,
    doi = {10.1051/0004-6361/201322068},
    url = {http://adsabs.harvard.edu/abs/2013A%26A...558A..33A}
}

@misc{fidgit,
  author = {A. M. Smith and K. Thaney and M. Hahnel},
  title = {Fidgit: An ungodly union of GitHub and Figshare},
  year = {2020},
  publisher = {GitHub},
  journal = {GitHub repository},
  url = {https://github.com/arfon/fidgit}
}
