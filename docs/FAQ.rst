==========================
Frequently Asked Questions
==========================

What are those circles and lines in the graph form?

How gene name is selected?

Does all variants that present in considered set of genomes are represented in the graph visualization form? 

- Not always. GCB by default skips paralogues genes, but they can still be analysed by switching ``Draw paralogues`` toggle on top panel.  

Where should I take coordinates of genes of interest?
- from genome annotations (i.e. Genebank or RefSeq database) by searching for particular gene.
- DOOR database [Mao, Xizeng, et al., Nucleic acids research, 2014] (currently available `here <http://161.117.81.224/DOOR3/>`_ ) can be used to find information about operons of specific organism.
- from papers, in which genome coordinates are specified.

How can I obtain graph image in vector format for publication?
- Export it to JSON and then open it in a Cytoscape or other graph editing software.

What if genome of interest is absent at gcb.rcpcm.org?

Can I use PC for the standalone analyisis or do I need a computational cluster?

How many genomes may be analyzed in a standalone version?


Can I adress someone to help me with my organisms?

- You can write to the `google group <https://groups.google.com/forum/#!forum/genome-complexiity-browser>`_. We will be hapy to help you.

Why should I run several python scripts insted of one in a standalone version?
- you may choose different references. Only complexity values for the selected reference are added to database. Usually we have one or several genomes of particular interest or of good quality which may become references. Computation of complexity values for each genome in a set to 