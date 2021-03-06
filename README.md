# prune
A neural network appraoch to DNA contamination removal

Uses the Keras Libary for neural network creation to filter specific sequences from a fastq/fasta

# Usage

Provide a txt file containing the seqeunces to be serached for and a fastq as your background.

<i> Change the Input files in the scripts accordingly. </i> 

### System
Linux : use a the command line to create a conda envoirement and also clone the repo , than the files can easily be run with <code> PYTHONHASHSEED= </code>  parameter

Windows : i used anacondas Powershell prompt which lets you use all your packages. You can also install git on anaconda so git clone will work as well on the powershell. Just run the Programms via python. Hashseedfixing via <code> $env:PYTHONHASHSEED= </code> and a number

### Preparation

1. Clone or copy the files, one easy way to do this is <code> git clone https://github.com/JonasDauster/prune </code>

2. Provide a set of normal, clean sequences that do not contain the sequences you want to search for or simply your  (as fastq, for reference see example data)

3. Provide the sequences you want to search for (as txt, for reference see example data)

4. Install all requiered packages, i recommend conda for that (keras,tensorflow,pandas,biopython,numpy all python 3 versions should work fine )

### Training
1. Change the files in TrainingDataCreation.py accordingly and run it

2. Do the same with CNN.py, but before you let it run fix the python hash seed. One easy way(with linux) is to use this setup with an command line interface:  <code> PYTHONHASHSEED=6 python3 CNN.py </code> . You can use any number behind <code> PYTHONHASHSEED= </code> , just choose the same when running the next steps. In Windows the same can be achived using <code> $env:PYTHONHASHSEED=6 </code> for example

### Testing/Running

1. For testing either generate a new training file and run it with DataLoad.py (use the same hashseed as for CNN.py) or use the validation_split method built in keras. 

2. For running on data to classify, prepare the data with TestDataPrep.py . Than run DataLoad.py on the prepared data (again with the same hashseed), without proper labels you can ignore the score. The found seqeunces can be found in network_hits.csv, the clean ones in no_hits.csv

### Performance Issues
- do not use more than about 10 individual seqeunces for training, use less for better results
- do not use too short fragments, i would recommend at least 12 bases long kmers
- watch out that your reads are all about the same length, harsh indifferences lead to bad training. If the fastq you want to search has a diffrent length than the ones the network was trained with consider setting max_lengthtest in the scripts to get a fixed length


## Further Methods
- to also spot mutations of a given fragment, the script Mutated.py can be used to generate mutations. The generated txt is than used for training.
- to directly get a fastq rid of the given seqeunce, DirectFastqFilter.py can be used. 
