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
  
  -- config (information about the run)
 
## Outputs
 <ol>
  <li>marker_summary.txt = how many reads hit each marker.</li>
  <li>taxa_summary = overall taxonomic data for your sample.</li>
  <li>sequence_taxa = information about each sequence and its probability distribution.</li>
  <li>An html file that shows a Krona plot.</li>
 </ol>

## Analyzig our data set

In these section we obtained the result for a data set SRR100123.fastq. These dataset belongs to a study of the fecal microbiome and the associated functions of 5 healthy cats.The Kronos plot generated after running the command is showed in the following figures. It is an interactive view showing the composition at different taxonomic levels.

<table>
  <td><p align="center"><img src="/IMAGES/nt2/bacteriacomposition.jpg"></p></td>
  <td><p align="center"><img src="/IMAGES/nt2/bacteriacomposition2.jpg"></p></td>
  <tr>
  <td><p align="center">Figure 1. Original view of total composition for dataset<p></td>
  <td><p align="center">Figure 2. Bacteria composition at the Phyla order<p></td>
  </tr>
  <tr>
  <td><p align="center"><img src="/IMAGES/nt2/firmicutescomposition.jpg"></p></td>
  <td><p align="center"><img src="/IMAGES/nt2/bacteriodetescomposition.jpg"></p></td>
  </tr>
  <tr>
  <td><p align="center">Figure3. Firmicutes composition at the Class order</p></td>
  <td><p align="center">Figure4. Bacteroides composition at the Class order</p></td>
  </tr>
 </table>

The Bacteroides/Chlorobi group is the most predominant bacterial phyla comprised ~47%, followed by Firmicutes (~40%), Proteobacteria (~6%), Fusobacteria (~4%), and Actinobacteria (~3%). 
Firmicutes is composed of ~77% Clostridia, ~15% Negativicutes and ~7% Erysipelotrichia. While Bacteriodes belongs 100% to the Bacteroidetes Class.


