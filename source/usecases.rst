=============================
Use cases
=============================

Determine gene context of operon of interest
----------------------------------------------

Consider we are interested in a particular operon and want to know something about its representation in a particular group of organisms. Let's take lactose operon of Escherichia coli as example.

First we need to determine its genome position, i.e. in `EcoCyc <https://www.google.com/url?q=https://biocyc.org/ECOLI/NEW-IMAGE?type%3DOPERON%26object%3DTU00036&sa=D&ust=1585816672295000>`_ database. Positions of start and end genes of the operon are 361249-366305 in  *K-12 substr. MG1655* genome. First we select Escherichia coli as ``Organism`` (dataset containing 300 genomes) and K-12 as ``Reference``. Only one contig is present (finished genome, no plasmids), so we do not need to change http://tux.ripcm.com:8081/build/html/standalone.html``Contig`` value.


