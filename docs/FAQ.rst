==========================
Frequently Asked Questions
==========================

What is this curvulin in the Complexity panel?
----------------------------------------------

- It is a local genome variability profile, which we call complexity profile. The higher the values, the more often changes occurs in this region of genome. By change we mean: gene insertions/deletions/translocations. Large-scale changes (e.g., large inversions) have little effect on complexity value; large scale means larger than the *window* parameter. Complexity profiles calculated with window values 20, 50, 100 are available at gcb.rcpcm.org, to obtain complexity profiles with other windows sizes you need to use stand-alone version.

Why do you call it complexity, not variability?
---------------------------------------------------

- For two reasons. Firstly, only fixed variants are observed, so we measure not variability *per se*, but combination of genome variability and fitness cost of the genome changes. Secondly, not only the quantity, but also the pattern of the changes contributes to the complexity value. The more overlapping changes occur, the greater their contribution.

What are those circles and lines in the Graph panel?
-----------------------------------------------------

- Circles correspond to the genes, or more precisely, to the orthogroups, inferred from the set of genomes. Lines (graph edges) connects genes, which are adjacent in at least one of the genomes (the larger the number of genomes these genes are located next to each other, the thicker the line).

How node name is selected?
-----------------------------------------------------

- By majority rule. We consider how many times the name of a gene occurs in the names of genes within the same orthogroup, and we choose the most common one.

Does all variants that present in considered set of genomes are represented in the graph visualization form? 
-------------------------------------------------------------------------------------------------------------------

- Not always. GCB by default skips paralogues genes, but they can still be analysed by switching ``Draw paralogues`` toggle in the left slide bar.  

Where should I take coordinates of genes of interest?
-------------------------------------------------------------------------------------------------------------------

- from genome annotations (i.e. Genebank or RefSeq database) by searching for particular gene.
- from DOOR database of operons [Mao, Xizeng, et al., Nucleic acids research, 2014] (currently available `here <http://161.117.81.224/DOOR3/>`_ ).
- from papers, in which genome coordinates are specified.

How can I obtain graph image in vector format for publication?
-------------------------------------------------------------------------------------------------------------------

- Export graph to JSON (left panel->File->Graph->Download JSON), and then import it in a Cytoscape (File->Import->Network from File), or other graph editing software.

What if genome of interest is absent at gcb.rcpcm.org?
-------------------------------------------------------------------------------------------------------------------

- You should use standalone application in this case. Command-line tools are available `here <https://github.com/DNKonanov/geneGraph>`_, local webserver is available `here <https://github.com/DNKonanov/GCB>`_. 

Can I run standalone version on Windows?
----------------------------------------

- Most likely yes, via `Windows Subsystem for Linux <https://docs.microsoft.com/en-us/windows/wsl/>`_, but we only tested GCB on Linux (Ubuntu, CentOS).

What genome sets can be used in a standalone version?
--------------------------------------------------

- We recomend using phylogenetically narrow groups of genomes as input to the GCB analysis (species, and even better - clades of the phylogenetic tree consisting of several tens of genomes). In this case local variability of genomes is not confused by large-scale changes in the genome (e.g., inversions). If you have a genome of interest, it’s a good idea to take in addition to it 50-100 closest genomes.

Can I use PC for the standalone analyisis or do I need a computational cluster?
-------------------------------------------------------------------------------------------------------------------

- In case of bacterial (not viral) genomes, it is recommended to run orthology inference on computational cluster. However, you may try it, and if orthogroups inference will be completed, then it is OK to continue the analysis. Local server application can be run on a standart PC.

How many genomes may be analyzed in a standalone version?
-------------------------------------------------------------------------------------------------------------------

- It depends on computational resources you have. If you have a computational cluster, then hundreds of genomes will be OK in most cases. If you have problems running analysis for your project feel free to contact us, we will try to help you (e.g., run orthology inference on our side).

Can I adress someone to help me with my organisms?
-------------------------------------------------------------------------------------------------------------------

- Please, write to the `google group <https://groups.google.com/forum/#!forum/genome-complexiity-browser>`_.
