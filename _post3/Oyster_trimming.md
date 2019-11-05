     bash-4.2$ srun --pty -p mcbstudent --qos=mcbstudent --mem=2G bash
     bash-4.2$ pwd
      /home/CAM/mcb5896/usr11
     bash-4.2$ ls

      chipmunk_fastq  mothur.1567784410.logfile  mothur.1571417701.logfile
      fastqcStuff     mothur.1567875472.logfile  SRR100123.fastq
      Metagenomics    mothur.1570745423.logfile  transferThisText.txt
      Miseq_batch     mothur.1571018318.logfile
      MiSeq_SOP       mothur.1571401653.logfile

    bash-4.2$ mkdir Oyster_Project
    bash-4.2$ cd Oyster_Project/
    bash-4.2$ ls
    
    HB1G.fna  HB2G.fna  HB3G.fna  LC1G.fna  LC2G.fna  oligos.txt
    HB1S.fna  HB2S.fna  HB3S.fna  LC1S.fna  LC2S.fna
    bash-4.2$
    
    bash-4.2$ cat 608**.fna > Oyster2.fna
bash-4.2$ ls
608900.fna  608902.fna  608904.fna  608906.fna  608908.fna  608910.fna  Oyster2.fna
608901.fna  608903.fna  608905.fna  608907.fna  608909.fna  608911.fna  Oyster.fna
bash-4.2$

Evaluating the obtained data:

mothur > summary.seqs(fasta=Oyster2.fna)

Using 36 processors.

                Start   End     NBases  Ambigs  Polymer NumSeqs
Minimum:        1       35      35      0       2       1
2.5%-tile:      1       85      85      0       4       2853
25%-tile:       1       308     308     0       4       28527
Median:         1       320     320     0       4       57053
75%-tile:       1       321     321     0       5       85579
97.5%-tile:     1       323     323     1       6       111253
Maximum:        1       633     633     13      19      114105
Mean:   1       295     295     0       4
# of Seqs:      114105

It took 2 secs to summarize 114105 sequences.

Output File Names:
Oyster2.summary

Note: the Original paper mentioned an original 237,842 raw reads, but non all of them were actually public at the database
