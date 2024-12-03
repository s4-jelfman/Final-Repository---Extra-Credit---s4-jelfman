**Final-Repository---Extra-Credit---s4-jelfman**

# Lab 6 Commands
```bash
mamba create -n my_python27_env python=2.7
```
•	`mamba create -n`: Creates a new environment with Mamba, a faster Conda alternative.
•	Environment name (`my_python27_env`): The name assigned to the environment.
•	`python=2.7`: Specifies Python version 2.7 for compatibility with older tools.

```bash
conda activate my_python27_env
```
•	`conda activate`: Switches to the environment just created.
•	Environment (`my_python27_env`): Activates the Python 2.7 environment to install and run compatible tools.

```bash
mamba install -y ete3
```
•	`mamba install -y`: Installs the ete3 package
•	`ete3`: This toolkit handles phylogenetic trees, making it easier to visualize and manipulate trees within Python.


```bash
cd lab06-$MYGIT
```
•	`cd`: Changes the directory to where the Lab 6 repository was cloned.
•	`lab06-$MYGIT`: Moves to this lab folder

```bash
pwd
```
•	`pwd`: Displays the current directory path, confirming your location in the file system.

```bash
java -jar ~/tools/Notung-3.0_24-beta/Notung-3.0_24-beta.jar --help
```
•	`java -jar`: Runs the Notung program using Java.
•	File path: Points to Notung, a program for reconciling gene trees with species trees.


```bash
nw_display ~/lab06-$MYGIT/heatshockfam.tre
```
•	`nw_display`: Visualizes the species tree in `toyspecies.tre`.

```bash
java -jar ~/tools/Notung-3.0_24-beta/Notung-3.0_24-beta.jar -s ~/lab06-$MYGIT/heatshockfam.tre -g ~/lab06-$MYGIT/toygenetree.tre --reconcile --speciestag prefix --savepng --events --outputdir ~/lab06-$MYGIT/
```
•	`java -jar`: Runs Notung with Java.
•	`-s`: Specifies the species tree file, `heatshockfam.tre`.
•	`-g`: Specifies the gene tree file, `heatshockfam.tre`.
•	`--reconcile`: Tells Notung to reconcile the gene tree with the species tree.
•	`--speciestag prefix`: Interprets species names as prefixes in the gene tree file.
•	`--savepng`: Saves the resulting tree as a PNG.
•	`--events`: Records evolutionary events (duplications, transfers, etc.).
•	`--outputdir`: Specifies the output directory as the main Lab 6 folder.

```bash
conda activate my_python27_env
```
•	`conda activate`: Activates the environment to run scripts that need Python 2.7.

```bash
python2.7 ~/tools/recPhyloXML/python/NOTUNGtoRecPhyloXML.py -g ~/lab06-$MYGIT/heatshockfam.tre.rec.ntg --include.species -o ~/lab06-$MYGIT/heatshockfam.tre.rec.xml
```
•	`python2.7`: Runs the script in Python 2.7.
•	Script path: Converts Notung output into RecPhyloXML format for better tree visualization.
•	`-g`: Points to the Notung-generated gene tree.
•	`--include.species`: Adds species info to the XML output.
•	`-o`: Specifies the output as `heatshockfam.tre.rec.xml`.

```bash
thirdkind -Iie -f ~/lab06-$MYGIT/heatshockfam.tre.rec.xml -o ~/lab06-$MYGIT/heatshockfam.tre.rec.svg
```
•	`thirdkind -Iie`: Converts XML to SVG format for visualization.
•	`-f`: Specifies the input XML file.
•	`-o`: Sets the output as `heatshockfam.tre.rec.svg`.

```bash
convert -density 300 ~/lab06-$MYGIT/heatshockfam.tre.rec.svg ~/lab06-$MYGIT/heatshockfam.tre.rec.pdf
```
•	`convert -density 300`: Adjusts image quality to 300 dpi and converts SVG to PDF.
•	Input: The SVG file to be converted.
•	Output: Saves the result as a PDF.

```bash
cd ~/lab06-$MYGIT/heatshockfam
```
•	`cd`: Changes directory.
•	`heatshockfam`: Moves into the folder dedicated to your gene family.

```bash
ls ~/lab06-$MYGIT/heatshockfam/heatshockfam.homologsf.outgroupbeta.treefile
```
•	`ls`: Lists the contents of the specified file path, showing `heatshockfam.homologsf.outgroupbeta.treefile`

```bash
gotree prune -i ~/lab06-$MYGIT/heatshockfam/heatshockfam.homologsf.outgroupbeta.treefile -o ~/lab06-$MYGIT
```
•	`gotree prune`: Removes specified branches from a tree file.
•	`-i`: Points to the input tree file.
•	Species list: Defines branches to prune, removing specific hemoglobin subunits.
•	`-o`: Saves the pruned tree as `heatshockfam.homologsf.pruned.treefile`.

```bash
mkdir ~/lab06-$MYGIT/heatshockfam
```
•	`mkdir`: Creates a directory named mygenefamily for organizing files related to the analysis.

```bash
cp ~/lab05-$MYGIT/heatshockfam/heatshockfam.homologs.al.mid.treefile ~/lab06-$MYGIT/heatshockfam/toygenetree.tre.rec.pdf
```
•	`cp`: Copies the tree file from Lab 5 into the Lab 6 folder.

```bash
java -jar ~/tools/Notung-3.0_24-beta/Notung-3.0_24-beta.jar -s ~/lab05-$MYGIT/species.tre -g ~/lab06-$MYGIT/heatshockfam/heatshockfam.homologsf.pruned.treefile --reconcile --speciestag prefix --savepng --events --outputdir ~/lab06-$MYGIT/heatshockfam/
```
•	`java -jar`: Runs Notung.
•	Species tree: Loads the species tree from Lab 5.
•	Gene tree: Uses the pruned gene tree for reconciliation.
•	Reconciliation options: Saves outputs, including PNGs and event information, to the heatshockfam folder.

```bash
nw_display ~/lab05-$MYGIT/heatshockfam.tre
```
•	`nw_display`: Shows the species tree in `species.tre`.

```bash
grep NOTUNG-SPECIES-TREE ~/lab06-$MYGIT/heatshockfam/heatshockfam.homologsf.pruned.treefile.rec.ntg | sed -e "s/^\\[&&NOTUNG-SPECIES-TREE//" -e "s/\\]/;/" | nw_display -
```
•	`grep NOTUNG-SPECIES-TREE`: Extracts lines with species tree data.
•	`sed`: Edits the output to remove extra symbols.
•	Pipe and `nw_display`: Shows the cleaned-up species reconciliation tree.
