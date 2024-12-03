 **Final Repository - Extra Credit - s4-jelfman**
# Lab 3 Commands

# Lab 3 Commands

`git clone https://github.com/Bio312/lab03-$MYGIT`
* This downloads a copy of the GitHub repository fro Lab 3 to the computer. We do this for every lab, so I'll only mention this once.
* `$MYGIT` was specified in an earlier lab to redirect to my specific Github username (s4-jelfman).
* `Pwd` To check you're in the right spot. It's used a lot, so I'll only mention it here.

`cd ~/lab03-$MYGIT`
* This is another command which is used frequently. It changes the directory to the main lab folder associated with the user's ID ($MYGIT/s4-jelfman), and specifying it for all further commands in this terminal until specified otherwise.

`ncbi-acc-download -F fasta -m protein "NP_005138.3"`
* Downloads the specific protein sequence from the NCBI database using the BLAST code NP_005138.3. The `-F fasta` part specifies the file format, `-m protein` specifies that it's a protein sequence.
 
`makeblastdb -in allprotein.fas -dbtype prot`
* Prepares `allprotein.fas` as a searchable protein database that can be used with BLAST (a tool for comparing biological sequences). This allows searching within this combined protein file.

`mkdir ~/lab03-$MYGIT/heatshockfam`
* Creates a new folder named heatshockfam in the main lab directory. This folder is specifically for storing information in this lab strictly for my gene family.

!Note that the downlaod of "NP_005138.3" from NCBI did not occur in this order, and was dragged and dropped into this new directory after it was created.

`cd ~/lab03-$MYGIT/heatshockfam`
* Changes the working directory to heatshockfam, making it the active folder for commands related to this specific gene family.
 
`blastp -db ../allprotein.fas -query NP_005138.3.fa -outfmt 0 -max_hsps 1 -out heatshockfam.blastp.typical.out`
* This runs a BLASTP search to compare the query protein file (NP_005138.3.fa) against the allprotein.fas database.
* `-outfmt 0`: Specifies that the output format should be standard.
* `-max_hsps 1`: Limits each result to only one best match.
* `-out heatshockfam.blastp.typical.out`: Sets the name for the output file.

`blastp -db ../allprotein.fas -query NP_005138.3.fa -outfmt "6 sseqid pident length mismatch gapopen evalue bitscore pident stitle" -max_hsps 1 -out heatshockfam.blastp.detail.out`
* Similar to the previous command but with more detailed output:
* `-outfmt "6 ..."`: Adds extra information such as match length, percentage similarity, gaps, and other details.
* `-max_hsps 1`: Keeps each result to a single best match.
* `-out heatshockfam.blastp.detail.out`: Saves results in a file named heatshockfam.blastp.detail.out.

`grep -c H.sapiens heatshockfam.blastp.detail.out`
* Counts how many times "H.sapiens" (for Homo sapiens, or humans) appears in heatshockfam.blastp.detail.out, giving the number of human matches in the results.

`awk '{if ($6< 1e-30)print $1 }' heatshockfam.blastp.detail.out > heatshockfam.blastp.detail.filtered.out`
* Filters the results by keeping only those with very high significance (e-value less than 1e-30).
* It saves only the sequence IDs of these highly significant matches to heatshockfam.blastp.detail.filtered.out.

`wc -l heatshockfam.blastp.detail.filtered.out`
* Counts the lines in heatshockfam.blastp.detail.filtered.out, giving the total number of significant matches after filtering.

`grep -o -E "^[A-Z]\\.[a-z]+" heatshockfam.blastp.detail.filtered.out | sort | uniq -c`
* Extracts and counts unique organism initials from the filtered output.
* Gives a list of different species represented in the results along with how many times each species appears.
