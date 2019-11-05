   
   
  We start by creating a new directory and moved into it the samples files:
  
    bash-4.2$ mkdir Oyster_Project
    bash-4.2$ cd Oyster_Project/
    bash-4.2$ ls
    
    HB1G.fna  HB2G.fna  HB3G.fna  LC1G.fna  LC2G.fna  oligos.txt
    HB1S.fna  HB2S.fna  HB3S.fna  LC1S.fna  LC2S.fna
    bash-4.2$
    
 To be able to work with just one file, I will put all the files into just one
 
    bash-4.2$ cat ****.fna > Oyster.fna
 
 To evaluate the total number of sequences 
 
     mothur > summary.seqs(fasta=Oyster.fna)


Table 1: 
		 Start	End	NBases	Ambigs	Polymer	NumSeqs
Minimum:	 1	     35	     35	     0	     2	1
2.5%-tile: 1	     85	     85	     0	     4	2853
25%-tile:	 1	     308	     308	     0	     4	28527
Median: 	 1	     320	     320	     0	     4	57053
75%-tile:	 1	     321	     321	     0	     5	85579
97.5%-tile:1	     323	     323	     1	     6	111253
Maximum:	 1	     633	     633	     13	     19	114105
Mean:	 1	     295	     295	     0	     4
# of Seqs:	114105

Output File Names:
Oyster.summary
Note: the Original paper mentioned an original 237,842 raw reads, but non all of them were actually public at the database

Know we can proceed to trim the sequences (I have previously look at the files and determined that only the forward primer is present, therefore we will trim it from all the sequences, allowing for a maximum of 3 bases different from the given sequence in a file named oligostest3.oligos.

     mothur > trim.seqs(fasta=Oyster.fna, oligos=oligostest3.oligos, bdiffs=3, pdiffs=3, tdiffs=3 )

     Using 36 processors.
     
     Output File Names: 
     Oyster.trim.fasta
     Oyster.scrap.fasta

Know to check how many sequences passed 

     mothur > summary.seqs(fasta=Oyster.trim.fasta)


	     	     Start	End	NBases	Ambigs	Polymer	NumSeqs
     Minimum:	     1	     15	     15	     0	     2	1
     2.5%-tile:	1	     72	     72	     0	     4	2729
     25%-tile:	     1	     288	     288	     0	     4	27285
     Median: 	     1	     299	     299	     0	     4	54569
     75%-tile:	     1	     299	     299	     0	     4	81853
     97.5%-tile:	1	     301	     301	     1	     6	106409
     Maximum:	     1	     600	     600	     6	     19	109137
     Mean:	     1	     275	     275	     0	     4
     # of Seqs:	109137

     It took 2 secs to summarize 109137 sequences.

     Output File Names:
     Oyster.trim.summary

and how many were removed

     mothur > summary.seqs(fasta=Oyster.scrap.fasta )



		       Start	End	   NBases	 Ambigs Polymer	NumSeqs
     Minimum:	     1	36	     36	     0	2	     1
     2.5%-tile:     1	60	     60	     0	4	     125
     25%-tile:	     1	163	     163	     0	5	     1243
     Median: 	     1	289	     289	     0	5	     2485
     75%-tile:	     1	322	     322	     0	6	     3727
     97.5%-tile:	1	326	     326	     1	6	     4844
     Maximum:	     1	633	     633	     13	18	     4968
     Mean:	     1	240	     240	     0	5
     # of Seqs:	4968

     It took 1 secs to summarize 4968 sequences.

     Output File Names:
     Oyster.scrap.summary



     mothur > trim.seqs(fasta=Oyster.trim.fasta, maxhomop=8,minlength=100, maxlength=300,  maxambig=0)
     It took 2 secs to trim 109137 sequences.

     Output File Names: 
     Oyster.trim.trim.fasta
     Oyster.trim.scrap.fasta


     mothur > summary.seqs(fasta=Oyster.trim.trim.fasta)

     Using 36 processors.

                  Start	End	NBases Ambigs	Polymer	NumSeqs
     Minimum:	     1	100	100	     0	     3	     1
     2.5%-tile:	1	144	144	     0	     4	     2455
     25%-tile:	     1	290	290	     0	     4	     24545
     Median: 	     1	299	299	     0	     4	     49089
     75%-tile:	     1	299	299	     0	     4	     73633
     97.5%-tile:	1	300	300	     0	     6	     95723
     Maximum:	     1	300	300	     0	     8	     98177
     Mean:	     1	282	282	     0	     4
     # of Seqs:	98177

It took 2 secs to summarize 98177 sequences.

Output File Names:
Oyster.trim.trim.summary


mothur > list.seqs(fasta=Oyster.trim.trim.fasta)

Output File Names: 
Oyster.trim.trim.accnos


mothur > unique.seqs(fasta=Oyster.trim.trim.fasta, list=Oyster.trim.trim.accnos )
list is not a valid parameter.
The valid parameters are: fasta, name, count, format, seed, inputdir, and outputdir.
[ERROR]: did not complete unique.seqs.

mothur > unique.seqs(fasta=Oyster.trim.trim.fasta, name=Oyster.trim.trim.accnos )
[ERROR]: GN85KWK04INVPR is in your fasta file, and not in your namefile, please correct.
[ERROR]: GN85KWK04J1GIY is in your fasta file, and not in your namefile, please correct.
[ERROR]: GN85KWK04ISLWP is in your fasta file, and not in your namefile, please correct.
[ERROR]: GN85KWK04I0ORO is in your fasta file, and not in your namefile, please correct.
[ERROR]: GN85KWK04I6QXQ is in your fasta file, and not in your namefile, please correct.
[ERROR]: GN85KWK04I48FY is in your fasta file, and not in your namefile, please correct.
[ERROR]: GN85KWK04I8L2E is in your fasta file, and not in your namefile, please correct.
[ERROR]: GN85KWK04JD4FU is in your fasta file, and not in your namefile, please correct.
[ERROR]: GN85KWK04JPOYL is in your fasta file, and not in your namefile, please correct.
[ERROR]: GN85KWK04I07JK is in your fasta file, and not in your namefile, please correct.
[ERROR]: GN85KWK04JHJ4I is in your fasta file, and not in your namefile, please correct.

mothur > unique.seqs(fasta=Oyster.trim.trim.fasta)
[WARNING]: This command can take a namefile and you did not provide one. The current namefile is Oyster.trim.trim.accnos which seems to match Oyster.trim.trim.fasta.
98177	47028

Output File Names: 
Oyster.trim.trim.names
Oyster.trim.trim.unique.fasta


mothur > summary.seqs(fasta=Oyster.trim.trim.unique.fasta)

Using 36 processors.
[WARNING]: This command can take a namefile and you did not provide one. The current namefile is Oyster.trim.trim.names which seems to match Oyster.trim.trim.unique.fasta.

		Start	End	NBases	Ambigs	Polymer	NumSeqs
Minimum:	1	100	100	0	3	1
2.5%-tile:	1	134	134	0	4	1176
25%-tile:	1	265	265	0	4	11758
Median: 	1	297	297	0	4	23515
75%-tile:	1	299	299	0	4	35272
97.5%-tile:	1	300	300	0	7	45853
Maximum:	1	300	300	0	8	47028
Mean:	1	271	271	0	4
# of Seqs:	47028

It took 1 secs to summarize 47028 sequences.

Output File Names:
Oyster.trim.trim.unique.summary


mothur > screen.seqs(fasta=Oyster.trim.trim.unique.fasta, maxambig=0)

Using 36 processors.
[WARNING]: This command can take a namefile and you did not provide one. The current namefile is Oyster.trim.trim.names which seems to match Oyster.trim.trim.unique.fasta.

It took 0 secs to screen 47028 sequences, removed 0.

[NOTE]: no sequences were bad, removing Oyster.trim.trim.unique.bad.accnos


Output File Names:
Oyster.trim.trim.unique.good.fasta


It took 1 secs to screen 47028 sequences.

mothur > list.seqs(fasta=Oyster.trim.trim.unique.good.fasta)

Output File Names: 
Oyster.trim.trim.unique.good.accnos



