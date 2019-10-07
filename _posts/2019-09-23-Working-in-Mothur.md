
# MOTHUR 2: TRIMMING

**OBJECTIVE** prepare and trim the chipmunk_fastq dataset provided in class using Mothur

**Recapitulating:** In our folder are raw sequence data of *the chipmunk dataset*, our previously generated *stability* file. Our job is to quality control the reads and analyze them. 

## PROCCESSING THE DATA: WORKING WITH MOTHUR
**1. Loading mothur**

        Bash$ load module mothur 1/42.3
        Bash $ mothur 
        mothur > make.contigs(file=stability.files,processors=4)
Or
        
        mothur> make.contigs(file=stability.txt,processors=4)

The stability files with its content, the scrap files do not have information, meaning that there are not sequences that has been trimmed in this first step.

**2. Reading the first 10 lines of the created files**
        
        mothur> system(head -n 10 stability.contigs.groups)

  note: we can do the same for all the different created files.


**3. Summarizing**
         
         mothur > summary.seqs(fasta=stability.trim.contigs.fasta )
        
**4. Trimming the data**
        
        mothur> screen.seqs(fasta=stability.trim.contigs.fasta, group=stability.contigs.groups, maxambig=0, maxlength=275)
        

**5. Summarizing the stability.contigs.good.group (the file to be used from now on)**
        
        mothur>summary.seqs(fasta=stability.trim.contigs.good.fasta)
