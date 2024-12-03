**Final-Repository---Extra-Credit---s4-jelfman**

# Lab 8 Commands

```bash
sed 's/*//' ~/lab04-$MYGIT/heatshockfam/heatshockfam.homologs.fas > ~/lab08-$MYGIT/heatshockfam/heatshockfam.homologs.fas
```
• `sed 's/*//'`: Removes any asterisk characters (*) from the file, often used as stop codons in FASTA files.
• Input file: Refers to `heatshockfam.homologs.fas` from Lab 4.
• `>`: Redirects the output to a new file.
• Output file (`~/lab08-$MYGIT/heatshockfam/heatshockfam.homologs.fas`): Saves the cleaned sequences to this new file.

```bash
rpsblast -query ~/lab08-$MYGIT/heatshockfam/heatshockfam.homologs.fas -db ~/data/Pfam/Pfam -out ~/lab08-$MYGIT/heatshockfam/heatshockfam.rps-blast.out -outfmt "6 qseqid qlen qstart qend evalue stitle" -evalue .0000000001
```
• `rpsblast`: Runs an RPS-BLAST search to find protein domains.
• `-query`: Specifies the input file for the query sequences.
• `-db`: Points to the Pfam database used for identifying domains.
• `-out`: Specifies the output file for the results.
• `-outfmt "6 ..."`: Defines the output format with columns for sequence ID, length, start/end positions, e-value, and title.
• `-evalue`: Sets a strict e-value threshold for significant matches.

```bash
cp ~/lab05-$MYGIT/heatshockfam/heatshockfam.homologsf.outgroupbeta.treefile ~/lab08-$MYGIT/heatshockfam
```
• `cp`: Copies a file.
• Source: Copies `heatshockfam.homologsf.outgroupbeta.treefile` from Lab 5.
• Destination: Saves the copy to the heatshockfam folder in Lab 8.

```bash
Rscript --vanilla ~/lab08-$MYGIT/plotTreeAndDomains.r ~/lab08-$MYGIT/heatshockfam/heatshockfam.homologsf.outgroupbeta.treefile ~/lab08-$MYGIT/heatshockfam/heatshockfam.rps-blast.out ~/lab08-$MYGIT/heatshockfam/heatshockfam.tree.rps.pdf
```
• `Rscript --vanilla`: Runs an R script without saving or restoring R environment variables.
• Script (`plotTreeAndDomains.r`): Visualizes a tree and domain data together.
• Input tree file: Specifies the tree file.
• Domain file: The RPS-BLAST output, containing domain annotations.
• Output file: Saves the plotted visualization as a PDF.

```bash
mlr --inidx --ifs "\\t" --opprint cat ~/lab08-$MYGIT/heatshockfam/heatshockfam.rps-blast.out | tail -n +2 | less -S
```
• `mlr`: Processes the RPS-BLAST output in a tabular format.
• `--inidx --ifs "\\t"`: Specifies tab-delimited input format.
• `cat`: Prints the content of the file.
• `tail -n +2`: Skips the first line of the output.
• `| less -S`: Opens the output in a scrollable view.

```bash
cut -f 1 ~/lab08-$MYGIT/heatshockfam/heatshockfam.rps-blast.out | sort | uniq -c
```
• `cut -f 1`: Extracts the first column of the RPS-BLAST output.
• `sort`: Sorts the data.
• `uniq -c`: Counts unique occurrences, displaying the frequency of each sequence.

```bash
cut -f 6 ~/lab08-$MYGIT/heatshockfam/heatshockfam.rps-blast.out | sort | uniq -c
```
• `cut -f 6`: Extracts the sixth column (titles of domains).
• `sort`: Sorts the data.
• `uniq -c`: Counts occurrences for each domain title.

```bash
awk '{a=$4-$3;print $1,'\t',a;}' ~/lab08-$MYGIT/heatshockfam/heatshockfam.rps-blast.out | sort -k2nr
```
• `awk`: Calculates the domain length by subtracting the start position (column 3) from the end (column 4).
• `print`: Outputs the sequence ID and calculated length.
• `sort -k2nr`: Sorts by length in descending order.

```bash
cut -f 1,5 -d $'\t' ~/lab08-$MYGIT/heatshockfam/heatshockfam.rps-blast.out
```
• `cut -f 1,5`: Extracts columns 1 and 5 (sequence ID and e-value).
• `-d $'\t'`: Specifies tab as the spacer called a "delimeter" which I had no idea was a thing.


