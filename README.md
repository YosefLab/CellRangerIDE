# CellRangerIDE

Hello yosef lab memebers

Welcome to cellrangeride! 

Here you can find general software for handling several methods:

1) Aligning 10x samples and converting fastqs to h5ads.
2) Create QC reports for your generated data.
3) Demultiplexing methods for you data.
4) Support different types of expirements: rna-seq, atac-seq, cite-seq.
5) Support different types of samples: gex, vdj, antibody, flex.

## Installation

First clone the git repo to your local computer

```bash
git clone https://github.com/YosefLab/CellRangerIDE
```

Due to contradictions between different types of environments we separate between cellbender and cellranger.
Therefore, if you only use cellbender please run:

```bash

conda env create -f cbenv.yaml
conda activate cellbender

```
In case you are using the rest of the API use the next environment

```bash

conda env create -f crenv.yaml
conda activate cellranger

```

For downloading cellranger software to your local computer please run the next code:
```bash
#!/bin/bash

cd /opt
wget -O cellranger-10.0.0.tar.gz "https://cf.10xgenomics.com/releases/cell-exp/cellranger-10.0.0.tar.gz?Expires=1764019025&Key-Pair-Id=APKAI7S6A5RYOXBWRPDA&Signature=jN-EZAjhSuFQdfmuSfBnB-8O9RRs1bKDhUVhVN3bN9V66g~qIrU4lP2VPL8jDx13Q4EMhRRzcA9GrMVziYNOAJ7Us7lV4EAxMX4R3Hpa7A25rGa3-X7bgbWGd6xtZ~6IKjdy1wbW4vYCtZ6BJw1ObHwjElg0FbasLV79kwVAVR8l6SQsWPGZHsl5Rxq22uVvOZMhqfGrkucTt1iFAiyGxXhpORaMeT1pz4J~SgBwZmZSNXjUROtlFef-f1xbnlbRfpGpggf~Byp93gXxrw95Wxgv3KR6UsN9r-HlgJPus~8GTrxF88sHG2ZijB90OLWpWNDbxDA50p6X618SO0Hm9g__"
tar -xzvf cellranger-9.0.1.tar.gz
export PATH=/opt/cellranger-9.0.1:$PATH

wget -O cellranger-atac-2.2.0.tar.gz "https://cf.10xgenomics.com/releases/cell-atac/cellranger-atac-2.2.0.tar.gz?Expires=1764019226&Key-Pair-Id=APKAI7S6A5RYOXBWRPDA&Signature=X2yIbdt3t1AhP-W56O30Gwr8yP0ehfRILoSRQdISFZ1FMSRYbjmh8dNLPhETKbz~rc1igaMtTmU7m2FJUj7IB66eH2ZTshZ8XPHlk5CblKvPWdeTNEsiTYnOYoq0JshCzX-7L7kviTAU77wpJPabohzHOPNlKobKq-aTq1i7jevgxGhENgkXDDsTyZXUDQIfPrXHD0ADDj7zvP3FHNeWb386Pgy30h8J3a143BmhUkjfku0MELCUf-Xv04Rr4hDZzAJxLD1tZN8pwHNkk8jZEP-dpStfU7cocj0MXPo0UZlaj7eBAO6e5vdhnpyK3in4E08CrsWrAphBq6v7L8bJWQ__"
tar -xzvf cellranger-atac-2.1.0.tar.gz
export PATH=/opt/cellranger-atac-2.1.0:$PATH

```
cellranger can be downloaded from the next link as well: https://www.10xgenomics.com/support/software/cell-ranger/downloads#download-links

cellranger-atac can be downloaded from the next link as well: https://www.10xgenomics.com/support/software/cell-ranger-atac/downloads#download-links

Instead of downloading cellranger softwares to your environment and only if you use wexac you can run:

```bash

ml CellRanger/9.0.0
ml CellRanger-ATAC/2.0.0

```

## Running explantation

For running cellrangeride there are 2 main options:
1) specify arguments according to the next template:
```bash

python CellRangerIDE/BackHand/Scripts/main.py \
--cellrangeride-path path/to/CellRangerIDE \
--pipeline \
--project-name \
--id \
--aligner-software-path \
--reference-genome \
--incpm-link \
--fastq-folder-path \
--fastq-folders-names \
--sample-names \
--multiplexing-method \
--feature-reference-csv \
--feature-types \
--hto-ids \
--hto-names \
--hto-reads \
--hto-pattern \
--hto-sequence \
--hto-feature-type \
--sample-id-cmo \
--cmo-barcode-csv \
--cmo-id \
--probe-set-path \
--probe-barcode-csv \
--probe-description \
--include-introns \
--create-bam \
--expected_cells \
--R1-length \
--R2-length \
--R1-vdj-length \
--R2-vdj-length \
--cellbender-path \
--chosen-pipeline \ 
--demultiplex-method \
--priors-probabilities \
--adata-path \
--running-machine \
--num-of-jobs \ 
--memory-size \
--cpu-cores \
--queue-name

```
Of course not all of the parameters are needed to be set it depends of the pipeline you are using and also part of these arguments have default parameters.
Therefore, you can check the cellranger_arguments.xlsx file to understand what is necessary and isn't.

## Example run tutorial

2) In case you are not using part of those paramters they will be read by the relevant .yaml file in the const_files folder, This is another unpopular way to run the software and it will be used if part of the sections will remain empty or won't be used at all.
If you still wish to modify these config files so at first you have to modify the config_general.yaml file and according to the pipeline you chose you have to fill the extra compatible config file.

## Example config file setup

