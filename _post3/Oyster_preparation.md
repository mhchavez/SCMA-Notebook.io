   
 # OYSTER DATASET TRIMMING AND ALIGMENT
 
 ## DATA PREPARATION 
 
A) We start by creating a new directory and moved into it the samples files:
  
    bash-4.2$ mkdir Oyster_Project
    bash-4.2$ cd Oyster_Project/
    bash-4.2$ ls
    
    HB1G.fna  HB2G.fna  HB3G.fna  LC1G.fna  LC2G.fna  oligos.txt
    HB1S.fna  HB2S.fna  HB3S.fna  LC1S.fna  LC2S.fna
    bash-4.2$
    
B) To be able to work with just one file, I will put all the files into just one
 
    bash-4.2$ cat ****.fna > Oyster.fasta
 
C) Aditionally during the run we will need two files:
 
 <ul>
	<li> names files: which has all the reads names found in the samples.</li>
	<li> group files: which is a list of the reads names linked to what sample it belong </li>
</ul>

To create these files the mothur SOP has many different option, for the name file I run the unique.seqs command with the concatenated file and as a result it gives me a name file. For the group file I run the following command modified with the actual sample names:

	mothur > make.group(fasta=sample1.fasta-sample2.fasta-sample3.fasta, groups=A-B-C)

## DATA PROCESSING PRE-ALIGMENT

**1. Summary seqs:  To evaluate the total number of initial sequences** 
 
     mothur > summary.seqs(fasta=Oyster.fasta)

	Using 36 processors.

			Start	End	NBases	Ambigs	Polymer	NumSeqs
	Minimum:	1	35	35	0	2	1
	2.5%-tile:	1	85	85	0	4	2853
	25%-tile:	1	308	308	0	4	28527
	Median: 	1	320	320	0	4	57053
	75%-tile:	1	321	321	0	5	85579
	97.5%-tile:	1	323	323	1	6	111253
	Maximum:	1	633	633	13	19	114105
	Mean:	1	295	295	0	4
	# of Seqs:	114105

	It took 2 secs to summarize 114105 sequences.

	Output File Names:
	Oyster.summary


Note: the Original paper mentioned an original 237,842 raw reads, but it seems that the available dataset has been trimmed already at some degree.

**2. Trimming**

We can proceed to trim the sequences (I have previously look at the files and determined that only the forward primer is present, therefore we will trim it from all the sequences, allowing for a maximum of 3 bases different from the given sequence in a file named oligostest3.oligos.

	   mothur > trim.seqs(fasta=Oyster.fasta, name=Oyster.names, oligos=oligostest3.oligos, pdiffs=3, bdiffs=3, maxhomop=8, minlength=200, flip=T, processors=2)

	Using 2 processors.
	It took 5 secs to trim 114105 sequences.


	Output File Names: 
	Oyster.trim.fasta
	Oyster.scrap.fasta
	Oyster.trim.names
	Oyster.scrap.names


Then we check how many sequences passed 
	
	mothur > summary.seqs(fasta=Oyster.trim.fasta)

			Start	End	NBases	Ambigs	Polymer	NumSeqs
	Minimum:	1	200	200	0	3	1
	2.5%-tile:	1	231	231	0	4	2477
	25%-tile:	1	297	297	0	4	24761
	Median: 	1	299	299	0	4	49522
	75%-tile:	1	299	299	0	4	74282
	97.5%-tile:	1	301	301	1	6	96566
	Maximum:	1	600	600	6	8	99042
	Mean:	1	291	291	0	4
	# of Seqs:	99042

	It took 2 secs to summarize 99042 sequences.

	Output File Names:
	Oyster.trim.summary

**3. Creating Unique.seqs and summarizing**

	mothur > unique.seqs(fasta=Oyster.trim.fasta)
	[WARNING]: This command can take a namefile and you did not provide one. The current namefile is Oyster.trim.names which seems to match Oyster.trim.fasta.
	99042	48120

	Output File Names: 
	Oyster.trim.names
	Oyster.trim.unique.fasta


	mothur > summary.seqs(fasta=Oyster.trim.unique.fasta, name=Oyster.trim.names)

			Start	End	NBases	Ambigs	Polymer	NumSeqs
	Minimum:	1	200	200	0	3	1
	2.5%-tile:	1	231	231	0	4	2477
	25%-tile:	1	297	297	0	4	24761
	Median: 	1	299	299	0	4	49522
	75%-tile:	1	299	299	0	4	74282
	97.5%-tile:	1	301	301	1	6	96566
	Maximum:	1	600	600	6	8	99042
	Mean:	1	291	291	0	4
	# of unique seqs:	48120
	total # of seqs:	99042

	It took 1 secs to summarize 99042 sequences.

	Output File Names:
	Oyster.trim.unique.summary

**4. Counting sequences**

	mothur > count.seqs(name=Oyster.trim.names, group=Oyster.groups)

	It took 0 secs to create a table for 99042 sequences.

	Total number of sequences: 99042

	Output File Names: 
	Oyster.trim.count_table

to check the first lines of the created table we can used the following command:

	mothur > system(head Oyster.trim.count_table)
	#Compressed Format: groupIndex,abundance. For example 1,6 would mean the read has an abundance of 6 for group 1.
	#1,HB1G	2,HB1S	3,HB2G	4,HB2S	5,HB3G	6,HB3S	7,LC1G	8,LC1S	9,LC2G	10,LC2S	11,LC3G	12,LC3S	
	Representative_Sequence	total	HB1G	HB1S	HB2G	HB2S	HB3G	HB3S	LC1G	LC1S	LC2G	LC2S	LC3G	LC3S
	GN85KWK04I3FVK	1	6,1
	GN85KWK04JAY6U	1043	1,220	2,89	3,267	4,142	5,177	6,117	7,6	9,5	11,19	12,1
	GN85KWK04JTNV9	701	1,68	2,225	3,17	4,192	5,106	6,68	7,3	8,3	9,1	11,12	12,6
	GN85KWK04IAFKI	1	6,1
	GN85KWK04IORM8	822	1,70	2,237	3,82	4,90	5,77	6,94	7,52	8,9	9,25	10,7	11,69	12,10
	GN85KWK04IUU49	1	6,1
	GN85KWK04ICICE	1	6,1

And finally we can summarize the output:

	mothur > summary.seqs(fasta=Oyster.trim.unique.fasta, count=Oyster.trim.count_table)

	Using 36 processors.

			Start	End	NBases	Ambigs	Polymer	NumSeqs
	Minimum:	1	200	200	0	3	1
	2.5%-tile:	1	231	231	0	4	2477
	25%-tile:	1	297	297	0	4	24761
	Median: 	1	299	299	0	4	49522
	75%-tile:	1	299	299	0	4	74282
	97.5%-tile:	1	301	301	1	6	96566
	Maximum:	1	600	600	6	8	99042
	Mean:	1	291	291	0	4
	# of unique seqs:	48120
	total # of seqs:	99042

	It took 2 secs to summarize 99042 sequences.

	Output File Names:
	Oyster.trim.unique.summary
	
## ALIGNEMNT

**1. Silva bacteria dataset preparation**

 we must prepare the silva bacteria dataset to restrinct the aligment to only the V4 region:

	mothur > pcr.seqs(fasta=silva.bacteria.fasta ,start=11894, end=25319,keepdots=F)

	Using 36 processors.
	[NOTE]: no sequences were bad, removing silva.bacteria.bad.accnos

	It took 18 secs to screen 14956 sequences.

	Output File Names: 
	silva.bacteria.pcr.fasta



	mothur > rename.file(input=silva.bacteria.pcr.fasta, new=silva.v4.fasta)

	Current files saved by mothur:
	fasta=silva.bacteria.pcr.fasta
	processors=36

	mothur > summary.seqs(fasta=silva.v4.fasta)

	Using 36 processors.

			Start	End	NBases	Ambigs	Polymer	NumSeqs
	Minimum:	1	13424	270	0	3	1
	2.5%-tile:	1	13425	292	0	4	374
	25%-tile:	1	13425	293	0	4	3740
	Median: 	1	13425	293	0	4	7479
	75%-tile:	1	13425	293	0	5	11218
	97.5%-tile:	1	13425	294	1	6	14583
	Maximum:	3	13425	351	5	9	14956
	Mean:	1	13424	292	0	4
	# of Seqs:	14956

	It took 5 secs to summarize 14956 sequences.

	Output File Names:
	silva.v4.summary

**2. Aligment of samples to dataset**

A) Once prepared the dataset we move onto the aligment of our reads to silva bacteria V4 region


	mothur > align.seqs(fasta=Oyster.trim.unique.fasta, reference=silva.v4.fasta)

	Using 36 processors.

	Reading in the silva.v4.fasta template sequences...	DONE.
	It took 4 to read  14956 sequences.

	Aligning sequences from Oyster.trim.unique.fasta ...
	It took 86 secs to align 48120 sequences.

	[WARNING]: 265 of your sequences generated alignments that eliminated too many bases, a list is provided in Oyster.trim.unique.flip.accnos.
	[NOTE]: 52 of your sequences were reversed to produce a better alignment.

	It took 86 seconds to align 48120 sequences.

	Output File Names: 
	Oyster.trim.unique.align
	Oyster.trim.unique.align.report
	Oyster.trim.unique.flip.accnos

B) And we summarize the aligment outputs

	mothur > summary.seqs(fasta=Oyster.trim.unique.align, count=Oyster.trim.count_table)

	Using 36 processors.

			Start	End	NBases	Ambigs	Polymer	NumSeqs
	Minimum:	1	1231	2	0	1	1
	2.5%-tile:	1	11550	226	0	4	2477
	25%-tile:	1	11550	271	0	4	24761
	Median: 	1	11550	272	0	4	49522
	75%-tile:	1	11550	272	0	4	74282
	97.5%-tile:	3072	11550	274	0	6	96566
	Maximum:	13424	13425	297	5	8	99042
	Mean:	258	11544	268	0	4
	# of unique seqs:	48120
	total # of seqs:	99042

	It took 13 secs to summarize 99042 sequences.

	Output File Names:
	Oyster.trim.unique.summary

**3. Post aligment processing**

	
A) After aligment we have to ensure that the reads start and finish overlapin in the same region, to do it mothur have many different options, in my case I ooptimize the start and end of the reads to the 90%.
	
	mothur > screen.seqs(fasta=Oyster.trim.unique.align, name=Oyster.trim.names, group=Oyster.groups, optimize=start-end, criteria=90)

	Using 36 processors.
	Optimizing start to 1968.
	Optimizing end to 11550.

	It took 16 secs to screen 48120 sequences, removed 5130.

	/******************************************/
	Running command: remove.seqs(accnos=Oyster.trim.unique.bad.accnos.temp, name=Oyster.trim.names, group=Oyster.groups)
	Removed 5906 sequences from your name file.
	Removed 5906 sequences from your group file.

	Output File Names: 
	Oyster.trim.pick.names
	Oyster.pick.groups

	/******************************************/

	Output File Names:
	Oyster.trim.unique.good.align
	Oyster.trim.unique.bad.accnos
	Oyster.good.groups
	Oyster.trim.good.names


	It took 31 secs to screen 48120 sequences.

b) And summarizing the screening:

	mothur > summary.seqs(fasta=Oyster.trim.unique.good.align, name=Oyster.trim.good.names)

	Using 36 processors.

			Start	End	NBases	Ambigs	Polymer	NumSeqs
	Minimum:	1	11550	242	0	3	1
	2.5%-tile:	1	11550	263	0	4	2329
	25%-tile:	1	11550	271	0	4	23285
	Median: 	1	11550	272	0	4	46569
	75%-tile:	1	11550	272	0	4	69853
	97.5%-tile:	1248	11550	274	0	6	90808
	Maximum:	1968	13425	297	5	8	93136
	Mean:	88	11550	271	0	4
	# of unique seqs:	42990
	total # of seqs:	93136

	It took 11 secs to summarize 93136 sequences.

	Output File Names:
	Oyster.trim.unique.good.summary
	
c) Third we have to remove all reads that do not overlap in the same region or are empty

	mothur > filter.seqs(fasta=Oyster.trim.unique.good.align, vertical=T, trump=.)

	Using 36 processors.
	Creating Filter... 
	It took 21 secs to create filter for 42990 sequences.


	Running Filter... 
	It took 11 secs to filter 42990 sequences.



	Length of filtered alignment: 551
	Number of columns removed: 12874
	Length of the original alignment: 13425
	Number of sequences used to construct filter: 42990

	Output File Names: 
	Oyster.filter
	Oyster.trim.unique.good.filter.fasta

d) Finally because the previous manipulation we have to re run the unique seqs command just to make sure we do not have redundant reads.

	mothur > unique.seqs(fasta=Oyster.trim.unique.good.filter.fasta, name=Oyster.trim.good.names)
	42990	25213

	Output File Names: 
	Oyster.trim.unique.good.filter.names
	Oyster.trim.unique.good.filter.unique.fasta

## OTUS picking

**1. Preclustering**

Now that we have our reads trimmed and cleaned we will start putting the into groups, the first step is to cluster those reads that are 2bp different of more abundant sequences

	mothur > pre.cluster(fasta=Oyster.trim.unique.good.filter.unique.fasta, name=Oyster.trim.unique.good.filter.names, group=Oyster.good.groups, diffs=2)

	Using 36 processors.
	Reducing processors to 12.


				NOTE: AT THIS point each sample gets split and analyzed

	It took 15 secs to run pre.cluster.

	Output File Names: 
	Oyster.trim.unique.good.filter.count_table
	Oyster.trim.unique.good.filter.unique.precluster.fasta
	Oyster.trim.unique.good.filter.unique.precluster.count_table
	Oyster.trim.unique.good.filter.unique.precluster.HB1G.map
	Oyster.trim.unique.good.filter.unique.precluster.HB1S.map
	Oyster.trim.unique.good.filter.unique.precluster.HB2G.map
	Oyster.trim.unique.good.filter.unique.precluster.HB2S.map
	Oyster.trim.unique.good.filter.unique.precluster.HB3G.map
	Oyster.trim.unique.good.filter.unique.precluster.HB3S.map
	Oyster.trim.unique.good.filter.unique.precluster.LC1G.map
	Oyster.trim.unique.good.filter.unique.precluster.LC1S.map
	Oyster.trim.unique.good.filter.unique.precluster.LC2G.map
	Oyster.trim.unique.good.filter.unique.precluster.LC2S.map
	Oyster.trim.unique.good.filter.unique.precluster.LC3G.map
	Oyster.trim.unique.good.filter.unique.precluster.LC3S.map

And we summarize the results of precluster command

	mothur > summary.seqs(fasta=Oyster.trim.unique.good.filter.unique.precluster.fasta)

	Using 36 processors.
	[WARNING]: This command can take a namefile and you did not provide one. The current namefile is Oyster.trim.unique.good.filter.names which seems to match Oyster.trim.unique.good.filter.unique.precluster.fasta.

			Start	End	NBases	Ambigs	Polymer	NumSeqs
	Minimum:	1	550	223	0	3	1
	2.5%-tile:	1	551	249	0	4	265
	25%-tile:	1	551	252	0	4	2642
	Median: 	1	551	253	0	4	5284
	75%-tile:	1	551	254	0	5	7926
	97.5%-tile:	1	551	256	1	7	10303
	Maximum:	5	551	270	4	8	10567
	Mean:	1	550	253	0	4
	# of Seqs:	10567

	It took 1 secs to summarize 10567 sequences.

	Output File Names:
	Oyster.trim.unique.good.filter.unique.precluster.summary
	
**2. Removing Chimeras**
A) First we have to found the chimeras

	mothur > chimera.vsearch(fasta=Oyster.trim.unique.good.filter.unique.precluster.fasta, count=Oyster.trim.unique.good.filter.unique.precluster.count_table, dereplicate=t)

	Using 36 processors.
	Using vsearch version v2.13.3.
	Checking sequences from Oyster.trim.unique.good.filter.unique.precluster.fasta ...

	/******************************************/
	Running command: split.groups(groups=HB1G-HB1S-HB2G-HB2S-HB3G-HB3S-LC1G-LC1S-LC2G-LC2S-LC3G-LC3S, fasta=Oyster.trim.unique.good.filter.unique.precluster.fasta, count=Oyster.trim.unique.good.filter.unique.precluster.count_table)

	Output File Names: 
	Oyster.trim.unique.good.filter.unique.precluster.HB1G.fasta
	Oyster.trim.unique.good.filter.unique.precluster.HB1G.count_table
	Oyster.trim.unique.good.filter.unique.precluster.HB1S.fasta
	Oyster.trim.unique.good.filter.unique.precluster.HB1S.count_table
	Oyster.trim.unique.good.filter.unique.precluster.HB2G.fasta
	Oyster.trim.unique.good.filter.unique.precluster.HB2G.count_table
	Oyster.trim.unique.good.filter.unique.precluster.HB2S.fasta
	Oyster.trim.unique.good.filter.unique.precluster.HB2S.count_table
	Oyster.trim.unique.good.filter.unique.precluster.HB3G.fasta
	Oyster.trim.unique.good.filter.unique.precluster.HB3G.count_table
	Oyster.trim.unique.good.filter.unique.precluster.HB3S.fasta
	Oyster.trim.unique.good.filter.unique.precluster.HB3S.count_table
	Oyster.trim.unique.good.filter.unique.precluster.LC1G.fasta
	Oyster.trim.unique.good.filter.unique.precluster.LC1G.count_table
	Oyster.trim.unique.good.filter.unique.precluster.LC1S.fasta
	Oyster.trim.unique.good.filter.unique.precluster.LC1S.count_table
	Oyster.trim.unique.good.filter.unique.precluster.LC2G.fasta
	Oyster.trim.unique.good.filter.unique.precluster.LC2G.count_table
	Oyster.trim.unique.good.filter.unique.precluster.LC2S.fasta
	Oyster.trim.unique.good.filter.unique.precluster.LC2S.count_table
	Oyster.trim.unique.good.filter.unique.precluster.LC3G.fasta
	Oyster.trim.unique.good.filter.unique.precluster.LC3G.count_table
	Oyster.trim.unique.good.filter.unique.precluster.LC3S.fasta
	Oyster.trim.unique.good.filter.unique.precluster.LC3S.count_table

	/******************************************/

	It took 1 secs to check 1373 sequences from group HB1G.

	It took 1 secs to check 832 sequences from group HB1S.

	It took 1 secs to check 1038 sequences from group HB2G.

	It took 0 secs to check 985 sequences from group HB2S.

	It took 2 secs to check 1642 sequences from group HB3G.

	It took 0 secs to check 603 sequences from group HB3S.

	It took 1 secs to check 1421 sequences from group LC1G.

	It took 1 secs to check 739 sequences from group LC1S.

	It took 1 secs to check 866 sequences from group LC2G.

	It took 0 secs to check 581 sequences from group LC2S.

	It took 2 secs to check 1889 sequences from group LC3G.

	It took 0 secs to check 825 sequences from group LC3S.

	Output File Names:
	Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.pick.count_table
	Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.chimeras
	Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.accnos

B) Second, we will remove the identified Chimeras

	mothur > remove.seqs(fasta=Oyster.trim.unique.good.filter.unique.precluster.fasta, accnos=Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.accnos )
	[WARNING]: This command can take a namefile and you did not provide one. The current namefile is Oyster.trim.unique.good.filter.names which seems to match Oyster.trim.unique.good.filter.unique.precluster.fasta.
	Removed 249 sequences from your fasta file.

	Output File Names: 
	Oyster.trim.unique.good.filter.unique.precluster.pick.fasta


	mothur > summary.seqs(fasta=Oyster.trim.unique.good.filter.unique.precluster.pick.fasta, count=Oyster.trim.unique.good.filter.unique.precluster.denovo.vsearch.pick.count_table )

	Using 36 processors.

			Start	End	NBases	Ambigs	Polymer	NumSeqs
	Minimum:	1	550	223	0	3	1
	2.5%-tile:	1	551	251	0	4	2321
	25%-tile:	1	551	253	0	4	23209
	Median: 	1	551	253	0	4	46418
	75%-tile:	1	551	253	0	4	69627
	97.5%-tile:	1	551	254	0	6	90515
	Maximum:	5	551	270	4	8	92835
	Mean:	1	550	252	0	4
	# of unique seqs:	10318
	total # of seqs:	92835

	It took 1 secs to summarize 92835 sequences.

	Output File Names:
	Oyster.trim.unique.good.filter.unique.precluster.pick.summary


The following step consist in classifying the read using a taxonomic database and based on it remove all contaminants. For these step I have used two different train sets the RDP and the PDS. The results for each variation is in a different page.

