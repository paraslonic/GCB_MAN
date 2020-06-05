==============================================
Standalone version 
==============================================

Command-line tools (basic analysis)
####################################

Roadmap
-------

Standalone version should be used when the user wants to work with a custom set of genomes. 
Command-line scripts are provided to: calculate complexity profile, generate subgraphs, generate a database which can be imported to browser-based GUI application. Scheme of actions and scripts is shown below.

.. image:: img/alone/standalone_scheme_hor_short.png
	:align: center


Prerequisites
-------------

Orthogroup inference
---------------------

Orthogroup inference is the first step in the standalone analysis.
We recomend using our `orthosnake <https://github.com/paraslonic/orthosnake>`_ pipeline for inference of orthogroups, because GCB requires some special formating of the files.


**Orthosnake pipeline**

*INPUT: Fasta-formated files with .fna extension, one file per genome*

*OUTPUT: orthogroups file `Orthogroups.txt` in OrthoFinder format*

Steps: 

	1. Clone or download orthosnake GIT repository: https://github.com/paraslonic/orthosnake
	2. Put fasta-formated genome files in ``fna`` folder of the orthosnake folder. 
	3. Rut snakemake with ``--use-conda`` and other appropriate options

The following code will run analysis of the test dataset (three plasmids)::

   git clone https://github.com/paraslonic/orthosnake.git
   cd orthosnake
   cp test_fna/* fna # copy test fasta files with three plasmids
   snakemake -j 4 --use-conda

Here, we used snakemake with parameters specifying the number of available cores (``-j 4``), and using conda environments (``--use-conda``). During the first start of the pipeline, it will take about ten minutes to install the necessary programs into the conda environments.

If genome files have extension, other than ``.fna`` (e.g., ``*.fasta``) , please rename them. For example, to change the file extension from ``.fasta`` to ``.fna``, run::

	for i in fna/*.fasta; do mv $i fna/$(basename $i .fasta).fna; done

Orthosnake pipeline performs the following steps:

	* Fasta headers are modified, to satisfy the requirement of the Prokka:  
		* symbols other than alphanumericals and `_` are converted to `_`
		* if header is longer than 20 symbols, it is cropped to the first 18 symbols, and dots are added to the end (e.g., ``gi|15829254|ref|NC_002695.1`` becomes ``gi|15829254|ref|NC..``)
	* Annotation with Prokka.
	* Genebank files converted to amino acid fasta files.
	* Orthogroups are inferred with OrthoFinder.

When amino acid fasta files are generated from genebank files, information regarding location and product is included in headers in the following format: genome_name|numerical_id|start|end|product. Please note this if you want to perform orthogroups inference without using orthosnake.

Building a graph and complexity estimation with a single command
-----------------------------------------------------------------
*INPUT: orthogroups file `Orthogroups.txt` in OrthoFinder format*

*OUTPUT: graph-based representation of genomes (sqlite database), complexity values (text)*

To perform the basic analysis, run::

	python3 gg.py -i [orthogroups file] -o [output] --reference [name of the reference genome]

Parameters:

	``-i`` -- path to orthogroups file in OrthoFinder format.

	``-o`` --	path and name prefix for output files

	``--reference`` --	name of the reference genome (its filename without extension), used for complexity estimation. This parameter can be skipped, in this case, the complexity values for all genomes in the set will be estimated (this can take a lot of time). 
	
Optional parameters:

	``--window``  -- size of the window used in the complexity estimation (default is 20). Only the paths inside the window increase the value of complexity.

  	``--genomes_list`` -- a text file containing the names of the genomes that will be used to calculate the complexity. Useful for analysis of parts of genomes, such as phylogenetic tree clades, for their subsequent comparison.

	``--coalign`` -- a binary value (true/false) that determines whether to perform the step of selecting the optimal genomes orientation. It can take a lot of time when using a large number of draft genomes (5 hours for 1000 draft genomes).

Advanced complexity estimation algorithm settings (practically not used):

	``--iterations`` --  number of iterations in algorithm (default is 500)
                        
	``--min_depth`` -- minimum length of deviating path (default is 0)

	``--max_depth`` -- maximum length of deviating path (default is inf)
 



hotspots
complexity one reference or all





Command-line tools (advanced)
#############################

Roadmap
-------
For additional analysis, commands can be used that: 1) generate a complete graph, 2) generate and visualize subgraphs, 3) calculate the complexity.
Subgraph generation allows not to use the local server for exploring small regions of the genome in the form of a graph.
Separate full subgraph generation

.. image:: img/alone/standalone_scheme_hor_short.png
	:align: center

Building a graph
-----------------
*INPUT: orthogroups file `Orthogroups.txt` in OrthoFinder format*

*OUTPUT: graph-based representation of genomes (sif-file and sqlite database)*

Graph structure is stored in a sif-formatted text file and in a sqlite database file. Sif-formated text file is needed for furher command-line analysis steps. Sqlite database is needed for subsequent export to the local gcb server. 

To build a graph, run::

	python3 parse_og.py  -i [path to txt file with orthogroups] -o [path and name prefix for output files]

For example::

	python3 parse_og.py  -i Results/Orthogroups.txt -o graph

Main output files are:

	- :file:`graph.sif` - graph in a sif format.
	- :file:`graph.db` - SQLite database conatining graph.

Additional files for optional user analysis:

	- :file:`graph_context.sif` - number of unique contexts for each gene.
	- :file:`graph_genes.sif` - genes (nodes) from all genomes, with coordinates and Prokka annotations.

In a text ``graph.sif`` file, each line describes one edge, with its source and target nodes, genome id and contig id, to which this edge belongs. SQLite database ``graph.db`` file contains same information, and can be supplemented with complexity values in the course of further analysis.  

Complexity estimation
-------------------------

The next step is the computing of genome complexity. To do this type in terminal:: 

	python3 start_computing.py -i graph.sif -o [path to output folder] --reference [name of reference genome]

Additional parameters:
	\\-\\-window - sliding window size (default 20)
	
	\\-\\-iterations - number of iterations in probabilistic method (default 500)

	\\-\\-genomes_list - path to file with a list of names which will be used to create a graph (default all strains from *.sif will be used)

	\\-\\-min_depth, \\-\\-max_depth - minimum and maximum depth of generated paths in the graph (default from 0 to inf)

	\\-\\-save_db - path to the database, created by orthfinder_parse.py (default data will not be saved to db, only to txt). It’s necessary to use this parameter if you want to use this complexity profile in the stand-alone browser-based GCB application.


Output files for each contig in the reference genome:

	:file:`all_bridges_contig_n.txt` - this file contains information about the number of deviating paths between each pair of nodes in the reference genome



PODVAL
-------------------

Then gene annotation with prokka  tool of each genome is performed. Genbank files then converted to fasta formatted amino acid protein sequences with a custom python3 script. This script inserts special information about genes in fasta headers, namely: genome file name, numeric id, product name, contig, start, end (for example, ``>GCF_000007445|4|Threonine_synthase|NC_004431.1|4445|5731``). Then these files are used to infer orthology groups with OrthoFinder tool. The resulting file with orthology groups (OG) contains information about each OG in the following format: ``<og id>: <gene1> <gene2> …``

For example::

	OG0008594: GCF_001618325|2406|Small_toxic_polypeptide_LdrD|NZ_CP015069.1|2607133|2607240 GCF_001663475|366|Small_toxic_polypeptide_LdrD|NZ_CP015159.1|380042|380149







