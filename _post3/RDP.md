# Taxonomic Clasification and OTU's picking using RDP trainset

## Classification

**1. Classification**

        mothur > classify.seqs(fasta=Oyster.trim.unique.good.filter.unique.precluster.pick.fasta, count=Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.pick.count_table,reference=trainset16_022016.rdp.fasta,taxonomy=trainset16_022016.rdp.tax, cutoff=80)

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
        It took 117 secs to classify 10318 sequences.


        It took 117 secs to classify 10318 sequences.

        Output File Names: 
        Oyster.trim.unique.good.filter.unique.precluster.pick.rdp.wang.taxonomy
        Oyster.trim.unique.good.filter.unique.precluster.pick.rdp.wang.tax.summary


**2. remove contaminants**

                mothur > remove.lineage(fasta=Oyster.trim.unique.good.filter.unique.precluster.pick.fasta, count=Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.pick.count_table,taxonomy=Oyster.trim.unique.good.filter.unique.precluster.pick.rdp.wang.taxonomy ,taxon=Chloroplast-Mitochondria-unknown-Archaea-Eukaryota-Cyanobacteria)

        [NOTE]: The count file should contain only unique names, so mothur assumes your fasta, list and taxonomy files also contain only uniques.


        /******************************************/
        Running command: remove.seqs(accnos=Oyster.trim.unique.good.filter.unique.precluster.pick.rdp.wang.accnos, count=Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.pick.count_table, fasta=Oyster.trim.unique.good.filter.unique.precluster.pick.fasta)

        [NOTE]: The count file should contain only unique names, so mothur assumes your fasta, list and taxonomy files also contain only uniques.

        Removed 4514 sequences from your fasta file.
        Removed 62430 sequences from your count file.

        Output File Names: 
        Oyster.trim.unique.good.filter.unique.precluster.pick.pick.fasta
        Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.pick.pick.count_table

        /******************************************/

        Output File Names:
        Oyster.trim.unique.good.filter.unique.precluster.pick.rdp.wang.pick.taxonomy
        Oyster.trim.unique.good.filter.unique.precluster.pick.rdp.wang.accnos
        Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.pick.pick.count_table
        Oyster.trim.unique.good.filter.unique.precluster.pick.pick.fasta

Summarizing:

       mothur > summary.tax(taxonomy=current, count=current)
        Using Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.pick.pick.count_table as input file for the count parameter.
        Using Oyster.trim.unique.good.filter.unique.precluster.pick.rdp.wang.pick.taxonomy as input file for the taxonomy parameter.

        It took 0 secs to create the summary file for 30405 sequences.


        Output File Names: 
        Oyster.trim.unique.good.filter.unique.precluster.pick.rdp.wang.pick.tax.summary


## OTU's picking

**1. Calculating distance matrix**

        mothur > dist.seqs(fasta=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.fasta, cutoff=0.03)

        It took 140 secs to find distances for 5804 sequences. 63437 distances below cutoff 0.03.

        Output File Names: 
        Oyster.trim.unique.good.filter.unique.precluster.pick.pick.dist
        
**2. OTU's clustering**

       mothur > cluster(column=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.dist, count=Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.pick.pick.count_table)

        You did not set a cutoff, using 0.03.

        Clustering Oyster.trim.unique.good.filter.unique.precluster.pick.pick.dist

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

        mothur > classify.otu(list=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.opti_mcc.list, count=Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.pick.pick.count_table, taxonomy=Oyster.trim.unique.good.filter.unique.precluster.pick.rdp.wang.pick.taxonomy, label=0.03)
        0.03	2048

        Output File Names: 
        Oyster.trim.unique.good.filter.unique.precluster.pick.pick.opti_mcc.0.03.cons.taxonomy
        Oyster.trim.unique.good.filter.unique.precluster.pick.pick.opti_mcc.0.03.cons.tax.summary

## PHYLOGENETIC TREE**

**1. distance matrix**

        mothur > dist.seqs(fasta=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.fasta, output=lt)

        It took 123 secs to find distances for 5804 sequences. 16840306 distances below cutoff 1.
        
        Output File Names: 
        Oyster.trim.unique.good.filter.unique.precluster.pick.pick.phylip.dist



**2. Tree construction**


        mothur > clearcut(phylip=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.phylip.dist)

        Output File Names: 
        Oyster.trim.unique.good.filter.unique.precluster.pick.pick.phylip.tre


Aditionally we will rename the files to a easily handle naming system
 
        mothur > rename.file(count=Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.pick.pick.count_table, tree=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.phylip.tre, shared=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.opti_mcc.shared, constaxonomy=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.opti_mcc.0.03.cons.taxonomy,prefix=final, deleteold=f)

        Current files saved by mothur:
        fasta=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.fasta
        list=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.opti_mcc.list
        phylip=Oyster.trim.unique.good.filter.unique.precluster.pick.pick.phylip.dist
        shared=final.opti_mcc.shared
        taxonomy=Oyster.trim.unique.good.filter.unique.precluster.pick.rdp.wang.pick.taxonomy
        constaxonomy=final.cons.taxonomy
        tree=final.tre
        count=final.count_table


**3. Counting**

        mothur > count.groups(shared=final.opti_mcc.shared)
        HB1G contains 1883.
        HB1S contains 945.
        HB2G contains 1099.
        HB2S contains 1025.
        HB3G contains 2487.
        HB3S contains 699.
        LC1G contains 2495.
        LC1S contains 3399.
        LC2G contains 1676.
        LC2S contains 7166.
        LC3G contains 3552.
        LC3S contains 3979.

        Total seqs: 30405.

        Output File Names: 
        final.opti_mcc.count.summary

[:house: Back to home](https://github.com/mhchavez/SMCA-notebook1/wiki)
