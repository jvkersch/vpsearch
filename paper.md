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
BLAST [@1990-blast] in terms of lookup speed and accuracy. Some of these, such
as the FASTA tool suite [@2016-pearson-FindingProteinNucleotide], provide rapid
protein or nucleotide similarity search based on sequence content
alone. Others, such as the RDP classifier [@2007-wang-NaiveBayesianClassifier]
for microbiome analysis, take taxonomic information or other domain-specific
information into account to improve classification sensitivity or to provide
additional confidence measures. For whole-genome sequences, data structures for
approximate similarity search have been adopted to improve sequence lookup
speed [@2019-marcais-SketchingSublinearData].

# Statement of need

We present VPsearch, a light-weight Python package and command-line tool to
organize nucleotide sequences into a so-called _vantage point tree_
[@1991-uhlmann-SatisfyingGeneralProximity;
1993-yianilos-DataStructuresAlgorithms]. This data structure allows for
similarity searches that use a number of lookups proportional to the logarithm
of the size of the database (rather than scanning through the database in
linear fashion), and hence greatly speeds up similarity search queries. In the
case study below we show that for short sequences (such as the 16S rRNA gene
used in bacterial classification) VPsearch outperforms both BLAST (7x speedup)
and ggsearch36 from the FASTA suite (27x speedup) without any loss in accuracy.

The VPsearch tool is implemented in Python, using Cython for
performance-critical sections.  It outputs similarity search results in the
"BLAST-6" tabular format also used by BLAST, Diamond, the FASTA tool suite and
others, so that VPsearch can be used as a drop-in replacement for any of these
tools. VPsearch is able to return the $k$ most similar sequences for a given
query, not just the most similar match, and is fully multithreaded.

# Case study

We compared the performance of VPsearch with two standard tools for sequence
lookup: Blast+, as a standard tool that is optimized for inexact but fast
sequence lookup via the matching sequence pair heuristic, and ggsearch36, part
of the FASTA suite, which relies on exact alignment to achieve higher accuracy
at the cost of greatly increased lookup times. We show that VPsearch manages to
combine the good aspects of both tools, while avoiding the drawbacks.


![XYZ\label{fig:execution-time}](execution-time.pdf)



# Figures

Figures can be included like this:
![Caption for example figure.\label{fig:example}](figure.png)
and referenced from text using \autoref{fig:example}.

Figure sizes can be customized by adding an optional second parameter:
![Caption for example figure.](figure.png){ width=20% }

# Acknowledgements

We would like to thank Jun Isayama and Yuko Kiridoshi for stimulating
discussions, and Homin Park for help in setting up the computational
infrastructure.

# References
