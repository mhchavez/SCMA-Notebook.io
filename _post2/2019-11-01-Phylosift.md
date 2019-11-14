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
  
      phylosift all --paired <sequences_file_read1> <sequences_file_read2> --disable_updates --output=<resul_file_name> --config=phylosiftrc_mcb5896.txt
  
 Understanding the code:
 
  -- paired (to let it know we are using paired reads from Illumina, followed by the two directories that hold all forward reads and then all reverse reads. It receives FASTA, paired FASTA, Fastq, .gz, .bz2
  
  -- disable updates (phylosift will scan for updates to the reference marker genes and the taxonomic information if we do not disable the updates)
  
  --output (here we specify the name of the directory that will hold all the results)
  
  -- config (information about the run???????)
  
    
 ## Outputs
 
marker_summary.txt = how many reads hit each marker
taxa_summary = overall taxonomic data for your sample
sequence_taxa = information about each sequence and its probability distribution

and an html file that shows a Krona plot

## Analyzig our data set

In these section we obtained the result for a data set SRR100123.fastq. These dataset belongs to a study of the microbiome of 5 healthy cats

The feline fecal microbiota plays an important role not only to animal health but also to human health as a reservoir for potential zoonotic pathogens and antibiotic resistant strains. In order to characterize the fecal microbial community and its functional capacity in domestic cats, we performed this study as the pioneer to use gene-centric metagenomic approach. Pooled fecal DNA samples from five healthy household cats were subjected to pyrosequencing. 454 GS junior system generated 152,494 pyrosequencing reads (total of 5,405 contigs) which have been classified to both phylogenetic and metabolic diversity of feline fecal microbiota. The Bacteroides/Chlorobi group is the most predominant bacterial phyla comprised ~68% and followed by Firmicutes (~13%) and Proteobacteria (~6%) respectively. Archaea, fungi and virus were minor community in overall diversity. Different from other metagenomes, three functional catagories such as dormancy and sporulation, macromolecular synthesis and secondary metabolism were depleted. Interestingly, this study also provided the diversity of enteric zoonotic pathogens (0.01-2.5%) as well as genes involved in antimicrobial resistant mechanisms. According to the similarity and distances based clustering among nine gastrointestinal metagenomes from five different hosts, cat metagenome clustered closely together with chicken both in phylogenetic level and in metabolic level (>80%). Future studies are required to provide deeper understanding on both intrinsic and extrinsic effects such as age, genetics and dietary interventions in feline gastrointestinal microbiome.



 results and discussion 
