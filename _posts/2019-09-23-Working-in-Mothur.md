
# MOTHUR 2: TRIMMING

**OBJECTIVE** prepare and trim the chipmunk_fastq dataset provided in class using Mothur

**Recapitulating:** In our folder are raw sequence data of *the chipmunk dataset*, our previously generated *stability* file. Our job is to quality control the reads and analyze them. 

## PROCCESSING THE DATA: WORKING WITH MOTHUR
**1. Loading mothur**

        Bash$ load module mothur 1/42.3
        Bash $ mothur 
**2. Grouping the reads**
Once we have the stability files, we are going to group all forward and reverse reads belonging to a sample into one.

        mothur > make.contigs(file=stability.files,processors=4)
        
Or, if we created stability file with notepad:
        
        mothur> make.contigs(file=stability.txt,processors=4)
        
For this command our Input / Output will be: 

<table border-left="15">
<tr>
     <td bgcolor="#AED6F1" align="center"><strong>INPUT</strong>
     </td>
     <td bgcolor="#AED6F1" align="center"><strong>OUTPUT</strong>
     </td>
</tr>
<tr>
     <td bgcolor="#EBF5FB"> 
           <ul>
                   <li> stability.file</li>
     </td>
     <td bgcolor="#EBF5FB">
          <ul>
                 <li> stability.trim.contigs.fasta</li>
                 <li> stability.trim.contigs.qual</li>
                <li>stability.scrap.contigs.fasta</li>
                <li>stability.scrap.contigs.qual</li>
                <li>stability.contigs.report</li>
                <li>stability.contigs.groups</li>
           </ul>
     </td>
          </tr>



**2. Reading the first 10 lines of the created files**
        
        mothur> system(head -n 10 stability.contigs.groups)

  note: we can do the same for all the different created files.


**3. Summarizing**
         
         mothur > summary.seqs(fasta=stability.trim.contigs.fasta )
        
**4. Trimming the data**
        
        mothur> screen.seqs(fasta=stability.trim.contigs.fasta, group=stability.contigs.groups, maxambig=0, maxlength=275)
        

**5. Summarizing the stability.contigs.good.group (the file to be used from now on)**
        
        mothur>summary.seqs(fasta=stability.trim.contigs.good.fasta)
