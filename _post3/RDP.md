# Taxonomic Clasification and OTU's picking

## Classification

**1. Classification**

mothur > classify.seqs(fasta=Oyster.trim.unique.good.filter.unique.precluster.pick.fasta, count=Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.pick.count_table,reference=trainset16_022016.rdp.fasta,taxonomy=trainset16_022016.rdp.tax, cutoff=80)

Using 36 processors.
Reading template taxonomy...     DONE.
Reading template probabilities...     DONE.
It took 5 seconds get probabilities.
Classifying sequences from Oyster.trim.unique.good.filter.unique.precluster.pick.fasta ...
[WARNING]: GN85KWK04I60JU could not be classified. You can use the remove.lineage command with taxon=unknown; to remove such sequences.
[WARNING]: GN85KWK04I17Q6 could not be classified. You can use the remove.lineage command with taxon=unknown; to remove such sequences.
[WARNING]: GN85KWK04I1KJ7 could not be classified. You can use the remove.lineage command with taxon=unknown; to remove such sequences.
[WARNING]: GN85KWK04IKG8I could not be classified. You can use the remove.lineage command with taxon=unknown; to remove such sequences.
[WARNING]: GN85KWK04JCTYX could not be classified. You can use the remove.lineage command with taxon=unknown; to remove such sequences.
[WARNING]: GN85KWK04ITWG0 could not be classified. You can use the remove.lineage command with taxon=unknown; to remove such sequences.
[WARNING]: GN85KWK04JZ92X could not be classified. You can use the remove.lineage command with taxon=unknown; to remove such sequences.
[WARNING]: GN85KWK04IC2FV could not be classified. You can use the remove.lineage command with taxon=unknown; to remove such sequences.
[WARNING]: GN85KWK04IWP7D could not be classified. You can use the remove.lineage command with taxon=unknown; to remove such sequences.
[WARNING]: GN85KWK04IISZG could not be classified. You can use the remove.lineage command with taxon=unknown; to remove such sequences.
It took 93 secs to classify 10318 sequences.


Output File Names: 
Oyster.trim.unique.good.filter.unique.precluster.pick.rdp.wang.taxonomy
Oyster.trim.unique.good.filter.unique.precluster.pick.rdp.wang.tax.summary

**2. remove contaminants**

mothur > remove.lineage(fasta=Oyster.trim.unique.good.filter.unique.precluster.pick.fasta, count=Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.pick.count_table,taxonomy=Oyster.trim.unique.good.filter.unique.precluster.pick.pds.wang.taxonomy ,taxon=Chloroplast-Mitochondria-unknown-Archaea-Eukaryota-Cyanobacteria)

[NOTE]: The count file should contain only unique names, so mothur assumes your fasta, list and taxonomy files also contain only uniques.


/******************************************/
Running command: remove.seqs(accnos=Oyster.trim.unique.good.filter.unique.precluster.pick.pds.wang.accnos, count=Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.pick.count_table, fasta=Oyster.trim.unique.good.filter.unique.precluster.pick.fasta)

[NOTE]: The count file should contain only unique names, so mothur assumes your fasta, list and taxonomy files also contain only uniques.

Removed 4540 sequences from your fasta file.
Removed 62438 sequences from your count file.

Output File Names: 
Oyster.trim.unique.good.filter.unique.precluster.pick.pick.fasta
Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.pick.pick.count_table

/******************************************/

Output File Names:
Oyster.trim.unique.good.filter.unique.precluster.pick.pds.wang.pick.taxonomy
Oyster.trim.unique.good.filter.unique.precluster.pick.pds.wang.accnos
Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.pick.pick.count_table
Oyster.trim.unique.good.filter.unique.precluster.pick.pick.fasta


mothur > summary.tax(taxonomy=current, count=current)
Using Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.pick.pick.count_table as input file for the count parameter.
Using Oyster.trim.unique.good.filter.unique.precluster.pick.pds.wang.pick.taxonomy as input file for the taxonomy parameter.

It took 0 secs to create the summary file for 30397 sequences.


Output File Names: 
Oyster.trim.unique.good.filter.unique.precluster.pick.pds.wang.pick.tax.summary

## OTU's picking

**1. Calculating distance matrix**

mothur > dist.seqs(fasta=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.fasta, cutoff=0.03)

Using 36 processors.

Sequence	Time	Num_Dists_Below_Cutoff

It took 112 secs to find distances for 5778 sequences. 62981 distances below cutoff 0.03.


Output File Names: 
Oyster.trim.unique.good.filter.unique.precluster.pick.pick.dist

**2. OTU's clustering**

mothur > cluster(column=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.dist, count=Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.pick.pick.count_table)

Using 36 processors.

You did not set a cutoff, using 0.03.

Clustering Oyster.trim.unique.good.filter.unique.precluster.pick.pick.dist


iter	time	label	num_otus	cutoff	tp	tn	fp	fn	sensitivity	specificity	ppv	npv	fdr	accuracy	mcc	f1score

0.03
0	0	0.03	5778	0.03	0	16626772	0	62981	0	1	0	0.996226	1	0.996226	0	0	
1	0	0.03	2101	0.03	52776	16618357	8415	10205	0.837967	0.999494	0.86248	0.999386	0.86248	0.998884	0.849576	0.850047	
2	0	0.03	2041	0.03	54183	16617708	9064	8798	0.860307	0.999455	0.856689	0.999471	0.856689	0.99893	0.857959	0.858494	
3	0	0.03	2048	0.03	54176	16617780	8992	8805	0.860196	0.999459	0.857649	0.99947	0.857649	0.998934	0.858387	0.858921	
4	0	0.03	2047	0.03	54207	16617751	9021	8774	0.860688	0.999457	0.857326	0.999472	0.857326	0.998934	0.85847	0.859004	


It took 1 seconds to cluster

Output File Names: 
Oyster.trim.unique.good.filter.unique.precluster.pick.pick.opti_mcc.list
Oyster.trim.unique.good.filter.unique.precluster.pick.pick.opti_mcc.steps
Oyster.trim.unique.good.filter.unique.precluster.pick.pick.opti_mcc.sensspec

**3. OTU's composition per sample**

mothur > make.shared(list=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.opti_mcc.list, count=Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.pick.pick.count_table, label=0.03)
0.03

Output File Names: 
Oyster.trim.unique.good.filter.unique.precluster.pick.pick.opti_mcc.shared

**4. OTU's taxonomic classification**

mothur > classify.otu(list=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.opti_mcc.list, count=Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.pick.pick.count_table, taxonomy=Oyster.trim.unique.good.filter.unique.precluster.pick.pds.wang.pick.taxonomy, label=0.03)
0.03	2047

Output File Names: 
Oyster.trim.unique.good.filter.unique.precluster.pick.pick.opti_mcc.0.03.cons.taxonomy
Oyster.trim.unique.good.filter.unique.precluster.pick.pick.opti_mcc.0.03.cons.tax.summary

## PHYLOGENETIC TREE**

**1. distance matrix**

mothur > dist.seqs(fasta=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.fasta, output=lt)

Using 36 processors.

Sequence	Time	Num_Dists_Below_Cutoff

It took 121 secs to find distances for 5778 sequences. 16689753 distances below cutoff 1.


Output File Names: 
Oyster.trim.unique.good.filter.unique.precluster.pick.pick.phylip.dist

**2. Tree construction**


mothur > clearcut(phylip=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.phylip.dist)

Output File Names: 
Oyster.trim.unique.good.filter.unique.precluster.pick.pick.phylip.tre


mothur > rename.file(count=Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.pick.pick.count_table, tree=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.phylip.tre, shared=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.opti_mcc.shared, constaxonomy=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.opti_mcc.0.03.cons.taxonomy,prefix=final, deleteold=f)
/******************************************/
Running command: system(cp Oyster.trim.unique.good.filter.unique.precluster.pick.pick.phylip.tre final.tre)

/******************************************/
/******************************************/
Running command: system(cp Oyster.trim.unique.good.filter.unique.precluster.pick.pick.opti_mcc.shared final.opti_mcc.shared)

/******************************************/
/******************************************/
Running command: system(cp Oyster.trim.unique.good.filter.unique.precluster.pick.pick.opti_mcc.0.03.cons.taxonomy final.cons.taxonomy)

/******************************************/
/******************************************/
Running command: system(cp Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.pick.pick.count_table final.count_table)

/******************************************/

Current files saved by mothur:
accnos=Oyster.trim.unique.good.filter.unique.precluster.pick.pds.wang.accnos
column=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.dist
fasta=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.fasta
list=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.opti_mcc.list
phylip=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.phylip.dist
shared=final.opti_mcc.shared
taxonomy=Oyster.trim.unique.good.filter.unique.precluster.pick.pds.wang.pick.taxonomy
constaxonomy=final.cons.taxonomy
tree=final.tre
count=final.count_table
processors=36

**3. Counting**

        mothur > count.groups(shared=final.opti_mcc.shared)
        HB1G contains 1891.
        HB1S contains 952.
        HB2G contains 1101.
        HB2S contains 1027.
        HB3G contains 2483.
        HB3S contains 698.
        LC1G contains 2487.
        LC1S contains 3400.
        LC2G contains 1668.
        LC2S contains 7165.
        LC3G contains 3549.
        LC3S contains 3976.

        Total seqs: 30397.

        Output File Names: 
        final.opti_mcc.count.summary

