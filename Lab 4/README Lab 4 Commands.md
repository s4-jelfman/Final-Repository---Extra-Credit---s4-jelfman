**Final-Repository---Extra-Credit---s4-jelfman**
# Lab 4 Commands



`mkdir ~/lab04-$MYGIT/heatshockfam`
* `mkdir`: Creates a new directory.
* `~/lab04-$MYGIT/heatshockfam`: Sets the path and name for the directory, which will store heatshockfam files and results.

`cd ~/lab04-$MYGIT/heatshockfam`
* `cd`: Changes the working directory to the newly created folder.
* `~/lab04-$MYGIT/heatshockfam`: Pulls up the heatshockfam directory for gene family analysis.

`pwd`
* `pwd`: Outputs the full path of the current working directory for confirming we're in the correct location.

`seqkit grep --pattern-file ~/lab03-$MYGIT/heatshockfam/heatshockfam.blastp.detail.filtered.out ~/lab03-$MYGIT/allprotein.fas | seqkit grep -v -p "carpio" > ~/lab04-$MYGIT/heatshockfam/heatshockfam.homologs.fas`
* `seqkit grep --pattern-file`: Searches for sequences matching patterns listed in a separate file.
* `~/lab03-$MYGIT/heatshockfam/heatshockfam.blastp.detail.filtered.out`: File containing patterns (sequence IDs) from previous BLAST results for identifying homologs.
* `~/lab03-$MYGIT/allprotein.fas`: Input file with all protein sequences.
* Pipe `|`: Directs the output from the first search to a second seqkit grep.
* `seqkit grep -v -p "carpio"`: Excludes sequences containing "carpio" to refine results.
* `> ~/lab04-$MYGIT/heatshockfam/heatshockfam.homologs.fas`: Saves the filtered output to heatshockfam.homologs.fas.

`muscle -align ~/lab04-$MYGIT/heatshockfam/heatshockfam.homologs.fas -output ~/lab04-$MYGIT/heatshockfam/heatshockfam.homologs.al.fas`
* `muscle -align`: Aligns sequences in the specified file using MUSCLE.
* Input file (`~/lab04-$MYGIT/heatshockfam/heatshockfam.homologs.fas`): Contains the homolog sequences identified in lab 3.
* Output file (`-output`): Specifies the destination file for the alignment results (heatshockfam.homologs.al.fas).

`alv -kli ~/lab04-$MYGIT/heatshockfam/heatshockfam.homologs.al.fas | less -RS`
* `alv -kli`: Uses the alignment viewer in key-length indicator mode for viewing alignment regions.
* `~/lab04-$MYGIT/heatshockfam/heatshockfam.homologs.al.fas`: Specifies the alignment file for viewing.
* Pipe `|` and `less -RS`: Passes the output to less for paginated display, with -RS handling line wrapping for readability.

`alv -kli --majority ~/lab04-$MYGIT/heatshockfam/heatshockfam.homologs.al.fas | less -RS`
* `alv -kli --majority`: Similar to the previous command but includes a majority consensus line in the alignment view.
* `~/lab04-$MYGIT/heatshockfam/heatshockfam.homologs.al.fas`: Points to the alignment file for majority view.
* `less -RS`: Displays results with line wrapping. 

!Note: heatshockfam.homologs.al.fas alongisde all other files mentioned in this lab and others are available to view in this lab folder-

`Rscript --vanilla ~/lab04-$MYGIT/plotMSA.R ~/lab04-$MYGIT/heatshockfam/heatshockfam.homologs.al.fas`
* `Rscript --vanilla`: Executes an R script Dr. Rest placed in the repository without saving or restoring the R environment. This is what creates the PDF saved under the name heatshockfam.homologs.al.fas, which resembles the ALV view but in a prettier more readable format.
* `~/lab04-$MYGIT/plotMSA.R`: Path to the R script that visualizes the multiple sequence alignment.
* `~/lab04-$MYGIT/heatshockfam/heatshockfam.homologs.al.fas`: Specifies the alignment file 
`muscle -align ~/lab04-$MYGIT/heatshockfam.homologs.fas -output ~/lab04-$MYGIT/heatshockfam.homologs.al.fas`
* `muscle -align`: Initiates MUSCLE, a program for multiple sequence alignment, to align the sequences in the specified file.
* `~/lab04-$MYGIT/heatshockfam.homologs.fas`: The input file with sequences to be aligned.
* `-output`: Specifies where to save the alignment results.
* `~/lab04-$MYGIT/heatshockfam.homologs.al.fas`: Output file where the aligned sequences will be saved.

`alv -kli ~/lab04-$MYGIT/heatshockfam.homologs.al.fas`
* `alv -kli`: Runs the alignment viewer (alv) in "key-length indicator" mode, which highlights alignment details.
* `~/lab04-$MYGIT/heatshockfam.homologs.al.fas`: Specifies the file to be viewed and analyzed, displaying matched and mismatched regions.

`t_coffee -other_pg seq_reformat -in ~/lab04-$MYGIT/heatshockfam.homologs.al.fas -output sim`
* `t_coffee -other_pg seq_reformat`: Uses the T-Coffee tool's reformatting function to convert the alignment.
* `-in ~/lab04-$MYGIT/heatshockfam.homologs.al.fas`: Specifies the alignment input file for reformatting.
* `-output sim`: Outputs the alignment in a similarity format, useful for comparing sequence similarity across sequences.

`alignbuddy -pi ~/lab04-$MYGIT/heatshockfam.homologs.al.fas`
* `alignbuddy`: Calls the AlignBuddy tool, used for managing and analyzing sequence alignments.
* `-pi`: Displays alignment information with positional indexing for insights into similarities and gaps.
* `~/lab04-$MYGIT/heatshockfam.homologs.al.fas`: Specifies the alignment file for processing.

`alignbuddy -pi ~/lab04-$MYGIT/heatshockfam.homologs.al.fas | awk ' (NR>2) { for (i=2;i<=NF;i++){ sum+=$i;num++} } END{ print(100*sum/num) } '`
* `alignbuddy -pi`: Analyzes the file heatshockfam.homologs.al.fas, providing indexed alignment information.
* Pipe `|`: Passes the output from AlignBuddy directly into the awk command.
* AWK script: Computes the average similarity percentage across the alignment:
  * `(NR>2)`: Skips the first two lines of output.
  * Loop `for (i=2;i<=NF;i++){ sum+=$i;num++}`: Iterates over each numeric field, summing the values and counting the occurrences.
  * `print(100*sum/num)`: Outputs the average similarity as a percentage.

  !Note: some of this is contains repeated steps and commands. It's just the way I did it and it worked. Some of dr. Rest's scripts don't specify what they're doing, so for safety I used buscle before and after MSA.