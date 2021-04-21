.. GCB_MAN documentation master file, created by
   sphinx-quickstart on Thu Apr  2 12:42:08 2020.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Genome Complexity Browser 
===================================

Welcome to the Genome Complexity Browser (GCB) documentation. 

GCB is created to analyse variability in hundreds of prokaryote or viral genomes simultaniously.

GCB performs:

	- Visualization of gene neighborhoods in a graph-based format.
	- Quantification of local genome variability. 

.. figure:: img/scheme_of_things.png
   :align: center


The graph-based visualization may facilitate answering questions:

	- Is a gene (operon) located in the same location in all genomes? If not, then what alternative genes are present?
	- Which parts of a gene set (operon) are conserved and which are variable? 
	- Which genomes contain some particular combination of genes?

	
Local genome variability profile may be used to identify:

	- Hotspots of horizontal gene transfer or other local gene rearrangement events. 
	- Cold spots, regions of the genome with virtually no changes in the considered set of genomes.

The GCB is available as a `web server <https://gcb.rcpcm.org>`_ and as a standalone application. 
Web server contains precalculated data for 143 prokaryote species. Standalone version allows to analyze a custom set of genomes (basic command-line skills will be needed). 

You can find screen recordings of GCB `here <https://www.youtube.com/playlist?list=PLba8uyARLwj1SK6iME73Biu-KE2NzcZR9>`_ (Youtube).

GCB paper is published in:

Manolov, A., Konanov, D., Fedorov, D., Osmolovsky, I., Vereshchagin, R., & Ilina, E. (2020). Genome Complexity Browser: Visualization and quantification of genome variability. PLOS Computational Biology, 16(10), e1008222.
`https://doi.org/10.1371/journal.pcbi.1008222 <https://doi.org/10.1371/journal.pcbi.1008222>`_

.. toctree::
	:maxdepth: 3
	:caption: Contents:

	general
	interface
	standalone
	FAQ
	contacts

* :ref:`search`
