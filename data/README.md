# Data for workshop

We have curated data for this workshop in this repository using the following commands.
First, we downloaded a reference genome and its gene map with Nextclade.

``` bash
nextclade dataset get --name sars-cov-2 --output-dir data
```

Then, we downloaded a small SARS-CoV-2 dataset based on open data in NCBI that represents the diversity of major clades circulating during the first two years of the SARS-CoV-2 pandemic.
We uncompressed these files, to make them easier to explore during the workshop.
We also reorder the FASTA to put `Wuhan-Hu-1/2019` at the top, so IQ-TREE infers it as the root for the initial `augur tree` call.

``` bash
curl -o data/metadata.tsv.xz https://data.nextstrain.org/files/ncov/open/reference/metadata.tsv.xz
curl -o data/sequences.fasta.xz https://data.nextstrain.org/files/ncov/open/reference/sequences.fasta.xz

xz -f -d data/*.xz

mv data/sequences.fasta data/sequences-unordered.fasta
(seqkit grep    -r -p "Wuhan-Hu-1/2019" data/sequences-unordered.fasta && \
 seqkit grep -v -r -p "Wuhan-Hu-1/2019" data/sequences-unordered.fasta) > data/sequences.fasta
rm data/sequences-unordered.fasta
```
