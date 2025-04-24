MS RWR Data
=========================================
Graphs to create multi-species and single-species heterogeneous networks for use in Network Enhanced Similarity Search, which were leveraged in the article *Improving the predictive power of random walk with restart models using multi-species gene-gene and gene-disease association data*

These graphs can be input in any order into Network Enhanced Similarity Search, which then automatically compiles all graphs and performs its random walk with restart. 
Please note in the manuscript which graphs were used for multi-species, single species, and global single species protein-protein interaction.

Data
-----

Annotations
''''''''''

Edge lists contain ontology terms and genes.

.. csv-table:: Example edge list
    :header: term, gene

    GO:0005829,	2645
    GO:0008637,	3099
    GO:0005886,	6869

BioGrid
''''''''''

Edge lists contain genes.

.. csv-table:: Example edge list
    :header: ENTREZ_GENE_A, ENTREZ_GENE_B

    6416,	2318
    84665,	88
    90,	2339

Go Graph
''''''''''

Edge lists contains GO annotations

.. csv-table:: Example edge list
    :header: term1, term2

    GO:0042060,	GO:0002246
    GO:0060485,	GO:0007506
    GO:0060485,	GO:0072074

Genesets
''''''''''

Edge lists, denoted as *gw_gs_...tsv*, contains geneset
gene

.. csv-table:: Example edge list
    :header: geneset, gene

    GS1132,	6532
    GS121068,	5890
    GS1229,	56112

Genesets to Ontology
''''''''''

Edge lists, denoted as *gw_gs_.._ont.tsv*, contains genesets
and accompanying ontology terms

.. csv-table:: Example edge list
    :header: geneset, term

    GS1132,	D010551
    GS1229,	D003932
    GS46978,	GO:0005694

Homology Clusters
''''''''''

Edge lists contains homology clusters and accompanying 
genes

.. csv-table:: Example edge list
    :header: cluster, gene

    cluster:3,	34
    cluster:7,	79558
    cluster:9,	20391

KEGG Network
''''''''''

Edge lists contains KEGG gene networks

.. csv-table:: Example edge list
    :header: node1, node2

    130589,	2538
    160287,	5315
    2026,	5224

Usage
-----

.. code:: text

    Usage: ness [OPTIONS] [OUTPUT]

      Use Network Enhanced Similarity Search (NESS), located at this repository: `NESS`_.
      To integrate all heterogeneous datasets and calculate
      diffusion metrics over the heterogeneous network using a random
      walk with restart.

.. _NESS: https://github.com/treynr/ness/tree/master

For example, to create a multi-species KEGG network. Note: you will use all edgelists in the
*all_graphs* folder for the multi-species heterogeneous network and use only single species
for each single species network. The below code is just a small example, but please follow
the repository's directions for all flags for each graph input.

.. code:: text

    $ ness -e kegg_network_hsa.tsv -e kegg_network_mmu.tsv -e kegg_network_rno.tsv --graph results.tsv

For conducting the random walk with restart over the network with a restart probability of 0.25 and 
distributing the walk over all cores

.. code:: text

    $ ness -e heterogenous_graph.tsv -r 0.25 -d results.tsv

For conducting graph permutation analyses with a walk restart probability of 0.25

.. code:: text

    $ ness -e heterogenous_graph.tsv -r 0.25 -d -p 1000 results.tsv

For conducting seeded walks, which limits to only a list of seed nodes, otherwise
all node results are given.

.. code:: text

    $ ness -e heterogenous_graph.tsv -r 0.25 -d -p 1000 --seed-file sud_genes/AUDgenes.txt results.tsv


