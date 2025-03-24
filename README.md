# kenya_2022_cholera_isolates_phylogeny_comparison_with_global_isolates

After obtaining all your fasta files, move or copy all into one folder. 
Make sure you have a reference fasta file to extract snps and do alignment
The tool for extracting and doing alignment is `parsnp`
Conda create env and install it.
`conda create -n parsnp parsnp`  and activate

Version used `Parsnp 2.1.3`

Identify the directory where your fasta files are, and where your reference files are, and also where your output will be saved.

command for running parsnp `parsnp -r /home/silantoi33/dee/N16961.fasta -d /home/silantoi33/dee/edited_fasta/
-o /home/silantoi33/dee/edited_fasta/parsnp -p 8`

- `-r /home/silantoi33/dee/N16961.fasta`: This specifies the reference genome (N16961.fasta) that will be used for the alignment.

- `-d /home/silantoi33/dee/edited_fasta/`: This is the directory where your input FASTA files (genomes) are located for alignment (other than the reference).

- `-o /home/silantoi33/dee/edited_fasta/parsnp`: This specifies the output directory where the results will be saved. The directory parsnp inside /home/silantoi33/dee/edited_fasta/ will contain the output files.

- `-p 8`: This specifies using 8 processor threads for parallel processing to speed up the computation.

Now after running parsnp, it will generate the `parsnp.ggr` file has graphical representation alignment.

Used `harvesttools` to convert to `.fasta` contain now aligned sequences of all the isolates.

To install `harvesttools` use conda `conda create -n harvesttools harvesttools` and activate it.

Version used `HarvestTools v1.3`

Use this command to convert. `harvesttools -i parsnp.ggr -S cholera_aligned2.fasta`

The `.fasta` file will now have sequences of all your isolates with reference sequences all aligned. 

If your dont want your tree to have the reference your can manually remove its sequences. 

now to rename the ID's of each sequences, that is to remove the `.fasta` use this command- `awk '/^>/ {gsub(/\.fasta$/, "", $1); print $1} !/^>/ {print $0}' cholera_aligned2.fasta > cholera_aligned2_renamed.fasta`

Now we can make the tree using iqtree2. To install use conda `conda create -n iqtree iqtree` and conda activate it.

Version used `iqtree2 2.4.0`

To run now phylogeny for our samples use this command. `iqtree2 -s cholera_aligned2_renamed.fasta --alrt 1000 -b 1000`

- `-s cholera_aligned2_renamed.fasta`: Specifies the input alignment file (cholera_aligned2_renamed.fasta) in FASTA format. This file contains the aligned sequences for the phylogenetic analysis.

- `--alrt 1000`: This option requests IQ-TREE2 to perform an Approximate Likelihood Ratio Test (aLRT) with 1000 replicates. The aLRT is used to assess the robustness of the tree branches.

- `-b 1000`: This option tells IQ-TREE2 to perform 1000 bootstrap replicates to estimate the confidence in the branches of the tree.

Use the maximum likelyhood tree of life generated file and upload it to `Itol` for visualization. 
