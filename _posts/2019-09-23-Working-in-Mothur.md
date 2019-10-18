
# MOTHUR 2: TRIMMING

**Objective:** 
- Start the first steps of data preparation of the chipmunk_fastq dataset provided in class using Mothur.

**Recapitulating:** In our folder are raw sequence data of *the chipmunk dataset*, our previously generated *stability* file. Our job is to quality control the reads and analyze them. 

## PROCCESSING THE DATA: WORKING WITH MOTHUR
**1. Loading mothur**

        Bash$ load module mothur 1/42.3
        Bash $ mothur 
        
**2. Grouping the reads**

Once we have the stability files, we are going to group all forward and reverse reads belonging to a sample into one contig and in the process of matching if there is disagreements in the base being call on each of the reads the algoritm will decide base on the quality to keep one or other base or called N.

        mothur > make.contigs(file=stability.files,processors=4)
        
Or, if we created stability file with notepad:
        
        mothur> make.contigs(file=stability.txt,processors=4)
        
For this command our Input / Output will be: 

<ul>
                <li>stability.trim.contigs.fasta</li>
                <li>stability.trim.contigs.qual</li>
                <li>stability.scrap.contigs.fasta</li>
                <li>stability.scrap.contigs.qual</li>
                <li>stability.contigs.report</li>
                <li>stability.contigs.groups</li>
 </ul>


   **SIDE NOTE: Reading the first 10 lines of the created files**

   each file created can be read using:
        
        mothur> system(head -n 10 name of file)
 
    for example:

        mothur> system(head -n 10 stability.contigs.groups)
        
the stability.trim.contigs.fasta and stability.trim.contigs.qual contain the information of the contigs that passed the quality constraints, while the "scrap" files contains data that did not pass the quality constraints, stability.contigs.group have the information linking samples and contigs and finally the stability.contigs.report contains information about the contigs like the number of N called bases.

**3. Summarizing the data** 

To know how many sequences we lost and how many we kept after obtaining contigs
       
         mothur > summary.seqs(fasta=stability.trim.contigs.fasta )
   
OUTPUT:
           <ul>
           <li>stability.trim.contigs.summary</li> 
           </ul>

       
**4. Trimming the data**

In this step everything that is bigger than 275 and reads with ambiguous bases will be removed
        
        mothur> screen.seqs(fasta=stability.trim.contigs.fasta, group=stability.contigs.groups, maxambig=0, maxlength=275)
   
  OUTPUT:
          <ul>
          <li>stability.contigs.pick.groups</li>
          <li>stability.trim.contigs.good.fasta</li>
          <li>stability.trim.contigs.bad.accnos</li>
          <li>stability.contigs.good.groups</li>
          </ul>
     

**5. Summarizing the stability.contigs.good.group (the file to be used from now on)**
In this step we check how many reads passed the screening in step 4
        
        mothur>summary.seqs(fasta=stability.trim.contigs.good.fasta)

[Back to home :house: ](https://github.com/mhchavez/SMCA-notebook1/wiki)

