# Taxonomic Clasification and OTU's picking uing PDS

## Classification

**1. Classification**

    mothur > classify.seqs(fasta=Oyster.trim.unique.good.filter.unique.precluster.pick.fasta, count=Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.pick.count_table,reference=trainset16_022016.pds.fasta,taxonomy=trainset16_022016.pds.tax, cutoff=80)


    It took 4 seconds get probabilities.
    Classifying sequences from Oyster.trim.unique.good.filter.unique.precluster.pick.fasta ...
    [WARNING]: GN85KWK04I60JU could not be classified. You can use the remove.lineage command with taxon=unknown; to remove such sequences.
    [WARNING]: GN85KWK04I17Q6 could not be classified. You can use the remove.lineage command with taxon=unknown; to remove such sequences.
    [WARNING]: GN85KWK04I1KJ7 could not be classified. You can use the remove.lineage command with taxon=unknown; to remove such sequences.
    [WARNING]: GN85KWK04IKG8I could not be classified. You can use the remove.lineage command with taxon=unknown; to remove such sequences.
    [WARNING]: GN85KWK04JCTYX could not be classified. You can use the remove.lineage command with taxon=unknown; to remove such sequences.
    [WARNING]: GN85KWK04IVC5J could not be classified. You can use the remove.lineage command with taxon=unknown; to remove such sequences.
    [WARNING]: GN85KWK04ITWG0 could not be classified. You can use the remove.lineage command with taxon=unknown; to remove such sequences.
    [WARNING]: GN85KWK04JZ92X could not be classified. You can use the remove.lineage command with taxon=unknown; to remove such sequences.
    [WARNING]: GN85KWK04IC2FV could not be classified. You can use the remove.lineage command with taxon=unknown; to remove such sequences.
    [WARNING]: GN85KWK04H5NSO could not be classified. You can use the remove.lineage command with taxon=unknown; to remove such sequences.
    It took 90 secs to classify 10318 sequences.


    It took 90 secs to classify 10318 sequences.


    It took 0 secs to create the summary file for 10318 sequences.


    Output File Names: 
    Oyster.trim.unique.good.filter.unique.precluster.pick.pds.wang.taxonomy
    Oyster.trim.unique.good.filter.unique.precluster.pick.pds.wang.tax.summary

**2. remove contaminants**

    mothur > remove.lineage(fasta=Oyster.trim.unique.good.filter.unique.precluster.pick.fasta, count=Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.pick.count_table,taxonomy=Oyster.trim.unique.good.filter.unique.precluster.pick.pds.wang.taxonomy ,taxon=Chloroplast-Mitochondria-unknown-Archaea-Eukaryota-Cyanobacteria)

    [NOTE]: The count file should contain only unique names, so mothur assumes your fasta, list and taxonomy files also contain only uniques.


    /******************************************/
    Running command: remove.seqs(accnos=Oyster.trim.unique.good.filter.unique.precluster.pick.pds.wang.accnos, count=Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.pick.count_table, fasta=Oyster.trim.unique.good.filter.unique.precluster.pick.fasta)

    [NOTE]: The count file should contain only unique names, so mothur assumes your fasta, list and taxonomy files also contain only uniques.

    Removed 4515 sequences from your fasta file.
    Removed 62431 sequences from your count file.

    Output File Names: 
    Oyster.trim.unique.good.filter.unique.precluster.pick.pick.fasta
    Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.pick.pick.count_table

    /******************************************/

    Output File Names:
    Oyster.trim.unique.good.filter.unique.precluster.pick.pds.wang.pick.taxonomy
    Oyster.trim.unique.good.filter.unique.precluster.pick.pds.wang.accnos
    Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.pick.pick.count_table
    Oyster.trim.unique.good.filter.unique.precluster.pick.pick.fasta

And summarizing:

    mothur > summary.tax(taxonomy=current, count=current)
    Using Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.pick.pick.count_table as input file for the count parameter.
    Using Oyster.trim.unique.good.filter.unique.precluster.pick.pds.wang.pick.taxonomy as input file for the taxonomy parameter.

    It took 0 secs to create the summary file for 30404 sequences.


    Output File Names: 
    Oyster.trim.unique.good.filter.unique.precluster.pick.pds.wang.pick.tax.summary

## OTU's picking

**1. Calculating distance matrix**

    mothur > dist.seqs(fasta=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.fasta, cutoff=0.03)

    Using 36 processors.

    Sequence	Time	Num_Dists_Below_Cutoff

    It took 114 secs to find distances for 5803 sequences. 63465 distances below cutoff 0.03.


    Output File Names: 
    Oyster.trim.unique.good.filter.unique.precluster.pick.pick.dist


**2. OTU's clustering**

    mothur > cluster(column=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.dist, count=Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.pick.pick.count_table)

    Using 36 processors.

    You did not set a cutoff, using 0.03.

    Clustering Oyster.trim.unique.good.filter.unique.precluster.pick.pick.dist


    iter	time	label	num_otus	cutoff	tp	tn	fp	fn	sensitivity	specificity	ppv	npv	fdr	accuracy	mcc	f1score

    0.03    0	0	0.03	5803	0.03	0	16771038	0	63465	0	1	0	0.99623	1	0.99623	0	0	
    1	0	0.03	2099	0.03	52175	16762662	8376	11290	0.822107	0.999501	0.86167	0.999327	0.86167	0.998832	0.841072	0.841424	
    2	0	0.03	2047	0.03	54423	16762119	8919	9042	0.857528	0.999468	0.859193	0.999461	0.859193	0.998933	0.857824	0.85836	
    3	0	0.03	2043	0.03	54503	16762091	8947	8962	0.858788	0.999467	0.858991	0.999466	0.858991	0.998936	0.858356	0.85889	
    4	0	0.03	2045	0.03	54533	16762067	8971	8932	0.859261	0.999465	0.858733	0.999467	0.858733	0.998937	0.858463	0.858997	
    5	0	0.03	2044	0.03	54538	16762062	8976	8927	0.85934	0.999465	0.858677	0.999468	0.858677	0.998937	0.858474	0.859008	


    It took 0 seconds to cluster

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
    0.03	2044

    Output File Names: 
    Oyster.trim.unique.good.filter.unique.precluster.pick.pick.opti_mcc.0.03.cons.taxonomy
    Oyster.trim.unique.good.filter.unique.precluster.pick.pick.opti_mcc.0.03.cons.tax.summary

## PHYLOGENETIC TREE

**1. distance matrix**

    mothur > dist.seqs(fasta=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.fasta, output=lt)

    Using 36 processors.

    Sequence	Time	Num_Dists_Below_Cutoff

    It took 121 secs to find distances for 5803 sequences. 16834503 distances below cutoff 1.


    Output File Names: 
    Oyster.trim.unique.good.filter.unique.precluster.pick.pick.phylip.dist

**2. Tree construction**

    mothur > clearcut(phylip=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.phylip.dist)

    Output File Names: 
    Oyster.trim.unique.good.filter.unique.precluster.pick.pick.phylip.tre

 Aditionally we will rename the files to a easily handle naming system
 
    mothur > rename.file(count=Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.pick.pick.count_table, tree=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.phylip.tre, shared=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.opti_mcc.shared, constaxonomy=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.opti_mcc.0.03.cons.taxonomy,prefix=final, deleteold=f)

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
      HB1G contains 1882.
      HB1S contains 945.
      HB2G contains 1098.
      HB2S contains 1026.
      HB3G contains 2487.
      HB3S contains 699.
      LC1G contains 2495.
      LC1S contains 3399.
      LC2G contains 1674.
      LC2S contains 7166.
      LC3G contains 3554.
      LC3S contains 3979.

      Total seqs: 30404.

      Output File Names: 
      final.opti_mcc.count.summary
