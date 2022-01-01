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

We compare the performance of VPsearch with two standard tools for sequence
lookup: Blast+, as a standard tool that is optimized for inexact but fast
sequence lookup via the matching sequence pair heuristic, and ggsearch36, part
of the FASTA suite, which relies on exact alignment to achieve higher accuracy
at the cost of greatly increased lookup times. We show that VPsearch manages to
combine the good aspects of both tools, while avoiding the drawbacks.

![Sequence lookup time for 232 sequences as a function of the size of the
    database. For small databases (less than 10,000 sequences), VPsearch
    performs comparably to Blast+ and ggsearch36. For realistic databases
    (consisting of more than 50,000 sequences), the VPsearch lookup times
    scales logarithmically as the size of the database
    increases.\label{fig:execution-time}](execution-time.pdf){ width=70% }

For our case study, we look up 232 query sequences from the Mothur SOP dataset
[@2013-kozich-DevelopmentDualIndexSequencing] in the Silva database
[@2013-quast-SILVARibosomalRNA] of 16S sequences. The database was processed by
excising the v4 region and removing duplicate sequences, resulting in a
database of 230,013 sequences (each approximately 250 base pairs in length)
with known taxonomies.

On the full Silva database, VPsearch is clearly the fastest (20s total lookup
time), compared to Blast+ (157s) and ggsearch (561.3s). For Blast+ and
ggsearch36, the total lookup time scales linearly with the size of the
database, whereas for VPsearch the scaling is logarithmical (in other words,
making the database 10 times larger adds a constant factor to the total lookup
time). We therefore believe that VPsearch will continue to be an accurate yet
performant lookup tool, even as sizes of genomic databases continue to
increase.

# Acknowledgements

We would like to thank Jun Isayama and Yuko Kiridoshi for stimulating
discussions, and Homin Park for help in setting up the computational
infrastructure.

# References
