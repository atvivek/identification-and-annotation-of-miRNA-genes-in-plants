# Identification-and-annotation-of-miRNA-genes-in-plants

### Hi all! Lets get our hands dirty in this session and find some miRNAs. 
--------------------------------------------------------------------------------------------------------------------------------
       
   1.For Windows User

   Install Putty software
   Open Putty and enter in Host Name (or IP address):
   	 
      workshop@172.16.1.__ 
      
   After this,  a new window pops up.
      
      Enter password
   

   2.For Linux and Mac users
  
   Open terminal and access server by typing the following command 
	 																
	   ssh user@17.16.1.__  
       Enter password:
  
--------------------------------------------------------------------------------------------------------------------------------
  
  
  ### Input-Data
- ath_mb21.txt : A tab-delimited text file of Arabidopsis thaliana miRBase 21 MIRNA hairpins and their coordinates in the TAIR10      
  (Athaliana_167.fa) genome.

- Athaliana_167.fa : Genome assembly for Arabidopsis thaliana via Phytozome. TAIR10 nuclear genome as well as plastid and mitochondrial 
   genomes. FASTA formatted.
	 
- SRR051927.fastq : FASTQ-formatted raw reads from SRA accession SRR051927. These are 50 nt single-end untrimmed small RNAs from 
   Arabidopsis thaliana aerial tissues from the Carrington Lab.
	 
 --------------------------------------------------------------------------------------------------------------------------------
  

   Use the "cd" command to go to a directory on your name.
	 	For example,			   
	  
		cd A_T_VIVEK
   Use the "ls" command to know what files are in your directory   
		
		ls 
   Type the below to know file size 	
		
		du -ch *
		
   Now, type in the below to get a hang of the ShortStack tool
	 
	  ShortStack 
   Try --help option to explore 
    
          ShortStack --help
	 	  
--------------------------------------------------------------------------------------------------------------------------------
		  
   
  **TEST 1**
  
  Type in command line below to perform  *de novo* annotation of a small RNAs
	
	ShortStack --adapter CTGTAGGC --readfile SRR051927.fastq --outdir test1 --genomefile Athaliana_167.fa

  ###### (Use option --bowtie_cores [x] while performing analysis of multiple samples)
	
> If you are running it for the first time, then, the run will first index the genome using samtools faidx, then build bowtie indices in preparation for alignment. After that, adapters are trimmed from the reads, and the reads are aligned to the genome. Finally, small RNA clusters are annotated.

 When this completes, you will have a directory called 'test1' (name was specified by the --outdir option) that contains all of the results.
  
  ### Questions?
  - What output files do you see?
  - How miRNAs are reported?  
  
		
  **TEST 2**
  
 Use the alignments made in test one to analyze pre-determined regions of the genome (in this case, the regions annotated as MIRNA  
 hairpins by miRBase version 19).
    
	ShortStack --bamfile test1/SRR051927_trimmed.bam --locifile ath_mb21.txt --outdir test2 --genomefile Athaliana_167.fa
  
  After succesful run, manipulate few files as below to generate miRNA sequence file in fasta format and annotation file respectively.  
    
    grep -p '\tY\t|#Locus' Results.txt > miRNA.txt
    awk '{print ">" $2 "\n "$9}' miRNA.txt > miRNA.fa
    
    grep 'MIRNA=Y|#Locus' ShortStack_All.gff3 > miRNA.gff3 
    

    
   ### Questions?
  - What output files do you see?
  - How many miRbase reported miRNAs are predicted?
  - How many family members of miR156 is reported?
  - Find the raw  and normalized counts of miR156 gene? 
    
  **TEST 3** 
  - Use psRNAtarget online tool to predict miRNA targets using miRNA.fa file
  
  ### Questions?
  - How many targets do you find for miRNA156?
	
  
    
--------------------------------------------------------------------------------------------------------------------------------
                                                       # END OF THIS SESSION
--------------------------------------------------------------------------------------------------------------------------------

    
    
  
