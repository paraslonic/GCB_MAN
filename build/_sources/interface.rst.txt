===================================
GUI description
===================================

GUI elements
##############

GCB page consists of three main parts: 1) top panel to select genome and region to work with, 2) complexity plot which shows complexity profile for selected genome and contig, 3) subgraph visualization form.

The **top panel** allows selecting one of the precalculated organisms, reference genome and contig (replicon for finished assemblies). The right side of the panel allows selecting the region of the genome for the subgraph visualization. User can specify the start and end coordinates of the region. OG identifiers (which can be taken from the subgraph visualization) can also be used to define a range. Draw paralogues option changes the default program behavior which is to ignore genes which have paralogues. When this option is switched ON,  orhologization of paralogous genes is applied to draw subgraph and calculate complexity. By default,  paralogous genes are not displayed and not contribute to complexity value.

.. image:: img/face/face1.png
        :align:   center

**Complexity plot** panel shows a visualization of complexity profile and allows a user to visualize custom data (GC content, pathogenicity islands, prophage regions, sequence motifs, etc.). Complexity profile can be downloaded as a text file. User can add custom features file, in which each line should be in the format:  <genome position> <numeric value>

.. image:: img/face/face2.png
        :align:   center

**Subgraph visualization** form contains a number of settings to simplify and customize subgraph. On the bottom, there is information about edges (which genomes contain the corresponding edge) and nodes (gene product).

.. image:: img/face/face3.png
        :align:   center

To explain parameters of visualization let's consider subgraph construction procedure: 1) nodes of the reference genome in selected region (+/- *window* ) are added, this is called base chain; 2) all paths which connect with the base chain are added to subgraph; 3) paths which start and end on the base chain and which have length <= *Depth* remain unchanged; 4) all other paths are cropped to the *Tails* length; 5) edges with number of genomes (weight) lower than *minimal edge* weight are removed from the subgraph.

By clicking on the edge user selects this edge. List of genomes which contain gene pair corresponding to the selected edge is shown on the information panel. Edges which have at least one of the genomes from this list are colored blue.

User can upload colors for the nodes from the current subgraph. Each line of this file should be in the format:<OG id> <hex color code>::

	OG000004 #ff0000
	OG000005 #777777


Step-by-step tutorials
#######################

Complexity analysis
--------------------

Complexity is the measure of local genome variability. It is calculated for a set of genomes, one of which is selected as a reference. The greater the number of local changes in a certain neighborhood, the greater the value of complexity. Locality is set by the parameter ``Window``, the larger it is, the more large-scale changes influences complexity value.

Thus, the three parameters that you need to select to calculate the complexity profile are: 1) set of genomes, 2) reference genome, 3) window size. All of them can be set in the left sliding panel. Window size equals 20 by default, and can be changed to other precalculated values (20, 50 and 100 values are available at gcb.rcpcm.org, any value may be used in a standalone version). At gcb.rcpcm.org we precalculated complexity profiles for over 140 prokaryotic species. Any set of genomes may be used in a stand-alone version.

To obtain the complexity profile for a certain set of genomes (we will consider the set of *Bacillus Subtilus* available at gcb.rcpcm.org, follow these steps:

(1) Open gcb.rcpcm.org in you web-browser.

 Left panel with a number of settings will open automatically. 

(2) Click on the ``Organism`` selector and choose ``Bacillus_subtilis`` item.

(3) Click on the ``Reference`` selector and choose one of the available genomes. Let's choose for example ``GCF_001889385.1_ASM188938v1_genomic (J-5)`` genome.

 Genome name is constructed based on its filename (NCBI RefSeq filenames are used in the web version, genomes were downloaded from NCBI FTP server). In the web version strain name from the RefSeq is added to this name in brackets. 

(4) Click on the ``Reference`` selector.

 The contigs of the selected genome will be shown. For complete (finished) genomes they corresponds to replicones (chromosome(s) and plasmids), for draft genomes they are some fragments of genome. You cannot see the complexity profile for all contigs at the same time, they must be selected in turn.

 In case of ``J-5`` genome, only one contig is present (``NZ_CP018295.1``), which means that it is a complete (finished) genome, with single chromosome and without plasmids. 

(5) Close left sliding panel by clicking on the some point outside it (e.g., on the middle of the page).

 To open this panel once again, click on the icon with three horizontal lines on the left side of the page.

(6) Complexity profile wile appear in the *Complexity Plot* panel.

A number of peaks and flat areas are visible in the complexity profile. Peaks corresponds to the genome regions in which many changes were fixed during evolution.  

(7) To get the numerical values of the complexity profile, open left sliding panel, select the *File* tab at the top of the panel, click ``Download complexity values`` button. 

Screen recording with these steps is available `here <https://youtu.be/q122j3pbcko>`_.



Gene neigborhood analysis
---------------------------

Consider we are interested in a particular operon and we want to know more about its representation in a particular group of organisms. Let's take `lactose operon <https://en.wikipedia.org/wiki/Lac_operon>`_ with its regulator in the Escherichia coli as an example (we will call it lac operon further).

First, we need to determine genome position of genes of interest. We can do it in multiple ways, e.g., from `EcoCyc <https://www.google.com/url?q=https://biocyc.org/ECOLI/NEW-IMAGE?type%3DOPERON%26object%3DTU00036&sa=D&ust=1585816672295000>`_ database or from `NCBI Refseq <https://www.ncbi.nlm.nih.gov/nuccore/NC_000913.3>`_. In our case, according to BioCyc, genome region of interst is located at 361249-366305 in *K-12 substr. MG1655*. First we select Escherichia coli as ``Organism`` in a dataset containing 300 *E. coli* genomes. Then we select K-12 MG1655 as ``Reference``. Only one contig is present (finished genome, no plasmids), so we do not need to change ``Contig`` value.

.. image:: img/tutorial/use1/use1_1.png
        :scale: 80 %

Then we should put the operon's margin coordinates to text fields: ``Start coordinate`` and ``End coordinate``.

.. image:: img/tutorial/use1/use1_2.png
        :scale: 80 %

Now we click ``DRAW GRAPH`` button on the bottom panel and graph representation of the operon appears. 

.. image:: img/tutorial/use1/use1_3.png

Note that edges are of different colors in the graph: black and red. Shown in red are edges from the reference genome, all other edges are black, they correspond to genes neighbourhood variants not present in a reference genome. 

Nodes have different colors too. Nodes of reference genome genes are colored red if they are located inbetween ``Start coordinate - neigbhourhood`` and ``End coordinate + neigbhourhood``; they are colored pink if they are present in a reference genome, but are located outside the mentioned region. Nodes of genes, that are absent in a reference genome, are colored green. Gray rectangle is drawn around nodes located between ``Start coordinate`` and ``End coordinate`` (lac operon genes in this case). 

More clear layout can be obtained manually by left clicking and dragging nodes with mouse.

.. image:: img/tutorial/use1/use4_.png

We can see now that operon is located in a conserved context in most of the genomes (thick edges designated with 1 and 2).
One of the operon’s genes is absent in some set of genomes. By left clicking on that gene we can select it and know its gene product. Gene products are assigned with `Prokka <https://github.com/tseemann/prokka>`__ tool in the web version of GCB. 

.. image:: img/tutorial/use1/select_node.gif

In our case, Galactoside acetyltransferase is missing from the operon in some genomes. What are that genomes? By clicking on the bypassing edge, we will select this edge. Selection of the edge results in two effects: 1) names of genomes corresponding to this edge appears in the ``List of genomes`` section below the graph, 2) other edges, taht contain at least one of the genomes from the selected edge are colored blue. In this way, one can determine possible variants of gene neigbhourhoods, and in which genomes they are present. 

.. image:: img/tutorial/use1/select_edge.gif

For now we have determined, that a number of genomes does not contain Galactoside acetyltransferase. We can also notice nodes connected by a thin edges, which seems to represent other alternative variants of the operon. Let's click on that nodes and on the nodes from the reference, to see their products.  

.. image:: img/tutorial/use1/look_orphans1.gif

We see that their names are the same, but their length differs a lot: 263 b.p. for an outlier gene and 1253 b.p. for a reference gene. Often, and also in this particular case,  it comes from frameshit splitting some genes into parts, some of which may become part of homology groups representing original gene. 

.. image:: img/tutorial/use1/look_orphans1.gif


Finaly to verify our findings let's switch to paralogues orthologization mode. To do it you should toggle ``Draw paralogous`` switcher on the top panel and click ``Draw`` button once more (be careful, your current graph layout will be lost, so consider opening new page). After clicking and dragging nodes it should be looking like this. A little bit scary.

.. image:: img/tutorial/use1/paralogs.png

This more complicated graph comes from not ignoring paralogous genes as it done by default, but instead showing all of them.


Combined analysis
------------------

With GCB, you can find which genes are in the hot spots of genome variability. To do this, first select an organism, strain and replicon (chromosome or plasmids, complete genomes are reccomended to be used as reference). Then, in complexity profile panel, click on some of the hot spots to set the current position (depicted with vertical line in the complexity plot and also in ``Start`` and ``End`` coordinates in the left sliding panel). Before proceding to the graph visualization, we recommend adjusting graph rendering options: set ``Minimal edge value`` to 10 (the more intense the hostpot, the bigger this value should be), ``Window`` to 10-20, depending on the hotspot width.  Now press the ``DRAW GRAH`` button in the upper left corner of the *Complexity* panel. Changing colors will be visible above the graph draw buttons while it is being built, and then graph will apear in the *Grpah* panel. To select several genes, for example, located at the variable region, press the left mouse button and holding it move the cursor to surround the desired genes. Their products will apear in the bottom right part of the **Graph** panel.


Publication-ready graph rendering
---------------------------------

A graph-based representation of genome region can be exported in the form of JPEG image or a JSON file. To do this, fist draw some graph and then go to the left sliding panel, select FILE tab, select GRAPH subtab, click "DOWNLOAD JPEG" or "DOWNLOAD JSON" buttons.
JPEG file stores only a bitmap image, while JSON file contains all infromation regarding the current graph, including its layout. JSON filecan be imported in `Cytoscape <https://cytoscape.org/>`_ for complete visualization control (customize the look of nodes, edges, do manual or one of the automatic layouts). Cytoscape graph renderings can be exported in a number of bitmap and vector formats (e.g., pdf, svg). To import JSON graph file into Cytoscape, select File->Import->Network from File and select file, that was downloaded from GCB. Now you may arange graph nodes and adjust style.


