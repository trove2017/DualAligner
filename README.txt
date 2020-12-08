DualAligner Application

Seah, Boon-siew
Bhowmick, Sourav S
Dewey, C Forbes

CONTACT:
seah0097@ntu.edu.sg or assourav@ntu.edu.sg

NOTE: This version is for review only. Distributed version to be released later.


Aligning PPI Networks
=====================

1) The following global PPI networks are included: human.net, yeast.net and drome.net for human, yeast and fly respectively

2) Two pairwise BLAST bit-score data are also provided: humanyeast.txt and dromeyeast.txt 

3) 
Run DualAligner with JAVA:
java -jar dualigner.jar -p <pairwisefile> <network1>, <network2> 

Example:
java -jar dualaligner.jar -m 50 -p humanyeast.txt human.net,yeast.net

This aligns human.net to yeast.net with humanyeast.txt as BLAST pairwise score values (NOTE: the order of the networks specified is important and must match the pairwise score file!). 

We recommend running DualAligner with the following JVM parameters, for example:

java -Xmx1024m -Xms32m -jar dualaligner.jar -m 50 -p humanyeast.txt human.net,yeast.net


3) Upon alignment, the results are placed in 
region-to-region:   alignedregions.txt
protein-to-protein: alignedproteins.txt


Processing your own PPI Networks
================================
1) Create or obtain PSI-MI 2.5 XML formatted network PPI files with GO annotations (example: IntAct networks in www.ebi.ac.uk/intact/for sample files). 

2) Parse network with the following:
java -jar dualaligner.jar -r true <network1>,<network2>

Example:
java -jar dualaligner.jar -r true human.xml,yeast.xml

3) The following files will be generated:
human.net
yeast.net
human.fasta
yeast.fasta

4) Use the fasta files to construct pairwise BLAST bit scores. Any existing tools can be used.

5) Run DualAligner with human.net, yeast.net and the new pairwise file. Recall that the order of networks specified must match the pairwise file.


Options
=======

Usage: DualAligner [options] <network1>,<network2>

  -x <value> | --extended <value>
        extended alignment (default = false)
  -m <value> | --maxSize <value>
        maximum region size (default = 50)
  -l <value> | --lambda <value>
        lambda (default = 300.0)
  -p <file> | --inputBLAST <file>
        input BLAST pairwise file (default=pairwise.txt)
  -r <value> | --parse <value>
        parse mode (default=false)
  <network1>,<network2>
        Network name format: FACETS (.net) or PSI-MI 2.5 XML(.xml)

