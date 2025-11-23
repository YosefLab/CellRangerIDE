# CellRangerIDE
This repo includes the future program to come for running various cellranger pipelines and additional algorithms. Have a look in the this README file!

Hello CellRanger users!

Here you can use various cellranger pipelines of 10x genomics.

Hopefully we will set an infrastracture that will make those pipelines more accessable 
and also new algorithems which are not included in 10x genomics.

The API should contain:

1) Converting BCL to Fastqs
2) Count pipelines
3) Multiplexing
4) Demultiplexing 
5) Quality checks
6) Dealing with various samples: GEX, VDJ, Antibodies etc.
7) PCA & TSNE & UMAP presentations
8) Optional: Preprocessing algorithems


Instructions:

1) Fill out the config file located in the const_file folder

2) Dynamic parameters such as: RAM usage, number of cpu cores, will be updated in the program through the script input fields, for example: on your machine run: "python path_to_CellrangerIDE\BackHand\Scripts\main.py 10 5 70" where 10 refers to the number of job, 5 refers to the number of cpu cores and 70 refers to the amout of RAM (70GB)






Hello yosef lab memebers

Welcome to cellrangeride! 

Here you can find general software for handling several methods:

1) Aligning 10x samples and converting fastqs to h5ads.
2) Create QC reports for your generated data.
3) Demultiplexing methods for you data.
4) Support different types of expirements: rna-seq, atac-seq, cite-seq.
5) Support different types of samples: gex, vdj, antibody, flex.

#!/bin/bash
cd /opt
wget -O cellranger-9.0.1.tar.gz "https://cf.10xgenomics.com/releases/cell-exp/cellranger-9.0.1.tar.gz?Expires=1739846992&Key-Pair-Id=APKAI7S6A5RYOXBWRPDA&Signature=lWj4nhoNebGYpV7bZzkYzxxmnhdlFD0zuLKtbLQsqPevb5VRscVDDsEdlnXdjnavCB6vyQMJ8DzgH9CHZqFIWwIfJz8jL4iPDGXXIZq4zqW1LG46hR18xergOgDrLaysRxzUZiFI2BOimjDtARViyyxZRSeVEsN3oILMLpWRukOPRt3czKfSbffpRq4Nw-QSlsTQQovruwQ5x27AgZ7ENApYSOgGKF5GF~hbOJYVbTchDUHNvyHChwmLPgENTefM3ZeGS1-Vs0X2XUL~pbIDeVdVUvLrwj~McjPzZuvXq-XB26qbD3jWNQrhmEG31OUVUfGvsbC2xdkur9EJwTCssA__"
tar -xzvf cellranger-9.0.1.tar.gz
export PATH=/opt/cellranger-9.0.1:$PATH

