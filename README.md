# In-silico Digestion of CSP & MSP2 Variants
Computes 13-mer epitope-abundance matrices for malaria vaccine antigens

# Purpose
This repository delivers a ready-to-run Galaxy workflow that converts a multi-sequence FASTA file of Plasmodium falciparum circumsporozoite protein (CSP) or merozoite surface protein 2 (MSP2) variants into a matrix that counts every overlapping 13-mer peptide found in each sequence. The matrix is the starting point for the antigenic clustering analyses reported in Braeken et al. (2025) and can be fed directly into GeneCluster 3.0, R, or Python heat-map tools.

# How the workflow works
Digestor cuts every protein in the input FASTA into 13-residue peptides using an “unspecific cleavage” rule and a 12-residue overlap (sliding window of one amino acid).

The digested FASTA is converted to a two-column table (peptide, variantID).

The file is split so each variant becomes its own dataset.

Galaxy’s Group tool counts how many times each peptide occurs in every variant.

Column join merges all per-variant tables on the peptide column, filling absent peptides with zeros. The joined table is the epitope-abundance matrix used in the paper.

# Running the workflow
# Requirements
Any Galaxy instance that hosts the listed tools (most public servers already do, including usegalaxy.eu and usegalaxy.org.au). No local installation of OpenMS or extra scripts is needed.

# Quick start
Log in to Galaxy, create a new history and upload your multi-sequence FASTA file.

Import the workflow: choose Workflows → Import, paste the JSON from workflows/In_silico…ga or upload the file.

Launch the workflow, picking your FASTA as the only input. Default parameters reproduce the paper’s settings.

When the run finishes, download Peptide_abundance_matrix.tabular. Each row is a unique 13-mer and each column a variant; values are raw counts.

# Customisation
Change peptide length, overlap, or enzyme specificity by editing the Digestor step before running. 

# Downstream use
Open the matrix in R (read.table) or Python (pandas.read_csv) and compute Spearman correlations for heat-map clustering.

GeneCluster 3.0 accepts the matrix as is; choose “complete linkage”.

# Citation
If this workflow supports your work, please cite:

Braeken R, Margerie L, Osterholz H et al. Antigenic and structural diversity of the intrinsically disordered malaria vaccine candidates CSP and MSP2. eBioMedicine (under review, 2025).

and link back to this repository.

Licence and reuse
All files are released under CC-BY-SA-4.0. You may copy, adapt and redistribute, provided you give appropriate credit and share improvements under the same terms.

Contact
Open an issue on GitHub or email dfplazag@gmail.com or sherwin.chan@ki.se for questions, suggestions, or pull requests.
