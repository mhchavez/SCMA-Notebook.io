# METAGENOMIC ANALYSIS WITH PHYLOSIFT

Phylosift is a set of tools that allows us to do some phylogenetic analysis of genomes and metagenomes. 

The authors have put toguether a pool of 37 markers genes of proteins to which the reads are compare against and then stablish in terms of phylogeny how the sequence match to the database.

To proceed with the analysis we need two pieces of information:
  <ol>
  <li> list of the reference markers </li>
  <li> taxonomic information associated to the reads that are part of the markers</li>
  </ol>
 
  -> Download : https://figshare.com/articles/PhyloSift_markers_database/5755404
  
  ## command
  
  phylosift all --paired PS_data/HMP_1.fastq.gz PS_data/HMP_2.fastq.gz --disable_updates --output=PS_results_HMP1 --config=phylosiftrc_mcb5896.txt
  
 Understanding the code:
  -- paired (to let them know we are using paired reads from Illumina, followed by the two directories that hold all forward reads and then all reverse reads.
  -- disable updates (phylosift will scan for updates to the reference marker genes and the taxonomic information if we do not disable the updates)
  --output (here we specify the name of the directory that will hold all the results)
  -- config (information about the run???????)
  
    
 ## Outputs
 
marker_summary.txt = how many reads hit each marker
taxa_summary = overall taxonomic data for your sample
sequence_taxa = information about each sequence and its probability distribution

and an html file that shows a Krona plot

## Analyzig our data set


3.	PhyloSift section = download PS_results_SRR100123.fastq; how to run the program, results and discussion 
