STRIP
=====

ShorT-Read Identification and Profiling of Microbial Communities

1. General:
The STRIP repository contains programs for reconstruction of microbial species identities and frequencies from massively parallel sequencing short-reads data. 

The repository includes source code, executables and example datasets. 

2. Installation:
Download the file STRIP.tgz from https://github.com/orzuk/STRIP
Extract the STRIP.tgz file to a directory of your choice, add to Matlab path and run.
Alternatively, you can clone the repository directly from github, by running the following: 
T.B.D.

2.1. Dependencies:
STRIP requires the installation of additional packages for some of its operations. To ensure operations of all STRIP modules, you will need to download the following packages: 
(i) CVX - Matlab convex optimization toolbox. 
Please download and install from http://cvxr.com/cvx/.
The package is required for mixture reconstruction module.
(ii) Mothur - Microbial ecology bioinformatics package. 
   Please download from http://www.mothur.org/ , install in a directory of your choice and add to path.  
This package is required only for the solution comparison module of STRIP. 

	2.2. Mex files:
To enhance performance, parts of STRIP are written in C and compiled to .mex files accessible by Matlab. We’ve provided .mex files for unix and pc in the directory /src/mex. If you need to create .mex files for your environment, you will need to run the following command in Matlab: 
		CompileSTRIPMexFiles 
	
	2.3 Demo/Usage Example: 
	After installation, you can run the following script/function
	STRIPMain
	This script demonstrates most of STRIP’s main modules. 
It simulates a bacterial mixture, sample reads, reconstruct identities, and compare reconstructed solution to original vector. 


3. Overview of main modules
3.1. Preparing the database:
This module prepares a sequence database in .mat format from a fasta file containing 
16S rRNA sequences. 
To prepare sequence database for a region of interest, perform the following steps:
(i) download the desired database as a fasta file 
(ii) If a specific PCR-amplified region is needed, perform in-silico PCR for the desired primers, and output the region from all amplified sequences to a new fasta file (we will name it for convenience db.fasta).
(iii) Run in the command line the PrepareDB script:
PrepareDB database-name output-mat-file-name (T.B.D.)

T.B.D.:
repeatWhenLowerThanThisValue
realReadsFromFileFlag
preprocessByExistanceFlag
Provide code for splitting the database


This will result in output-mat-file-name, a .mat file with prepared database in STIRP format, which is then used in the main solver (section 3.2). 

The program comes with the 16S sequence database described in the paper (see section 4). 

3.2. Reconstruct mixture identities from reads:
This is the main utility of STRIP. It reconstructs a microbial sample from short read data, 
and a prepared sequence database (see Section 3.1).
Programs

1. Main solver: SolveMixingMatrixFromReads

Input:
Reads (fasta file)
Database (T.B.D.)
Parameters

Output:
T.B.D.

Usage: SolveMixingMatrixFromReads reads-file database-file parameters-file output-file-name



3.3. Experiment processing:
script
Input:
reads (fasta)
output:
T.B.D.
Algorithm:
(i) Local noise processing (k-mer to k-10-mer) → normalized reads (T.B.D.)
(ii) Global noise processing (median filtering) → normalized reads (T.B.D.)
(iii) Main solver
(iv) L1-solution minimization

Usage: PreprocessData

3.4. Read Simulation Module:
This module simulates short-read data obtained from a bacterial mixture. 
Input:
number of reads, error model, number of bacteria, freq. distribution, read length, bacteria ID (optional)
Output:
simulated reads (fasta? or reads for solver?)

Usage: SimulateReadsFromSequences ….


3.5. Evaluation of Solution Accuracy:
This module evaluates the accuracy of the reconstructed solution, when a ‘ground-truth’ solution 
is available (either in simulations or using other technologies, e.g. Sanger sequencing). 

Input:
Original mixture file (Two columns: ID+Freq)
Reconstructed mixture (Two columns: ID+Freq)
Similarity threshold
Frequency threshold

Output
Weighted recall and precision (or other metrics?) 

Usage: 


4. Data:
The following files are available in the ‘database’ directory: 
current_prokMSA_unaligned.fasta.gz - a fasta file with 16s database - Downloaded from greengenes database  (T.B.D.)
s16_data_uni_packed.mat - a preprocessed version of the 16s database. Can be generated by running the following: (T.B.D.)



5. Acknowledgment

STRIP was developed by: 
Amnon Amir, Noam Shental, Amit Zeisel and Or Zuk, as part of work on the papers,

(i) “Accurate Identification and Profiling of Microbial Communities using Massively Parallel Sequencing”, O. Zuk, A. Amir, A. Zeisel, O. Shamir and N. Shental (submitted).

(ii) “High resolution microbial community reconstruction by integrating of short reads from multiple 16S rRNA regions“ 
A. Amir, A. Zeisel, O. Zuk, M. Elgart, S. Stern, O. Shamir, P.J. Turnbaugh, Y. Soen and N. Shental (submitted).

Please cite the above papers if using the package. 

6. Support
For any questions or comments, please contact: 
- Noam Shental: shental@openu.ac.il
- Or Zuk: orzuk@ttic.edu

