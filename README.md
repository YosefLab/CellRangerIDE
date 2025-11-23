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

```bash
#!/bin/bash

cd /opt
wget -O cellranger-9.0.1.tar.gz "https://cf.10xgenomics.com/releases/cell-exp/cellranger-9.0.1.tar.gz?Expires=1739846992&Key-Pair-Id=APKAI7S6A5RYOXBWRPDA&Signature=lWj4nhoNebGYpV7bZzkYzxxmnhdlFD0zuLKtbLQsqPevb5VRscVDDsEdlnXdjnavCB6vyQMJ8DzgH9CHZqFIWwIfJz8jL4iPDGXXIZq4zqW1LG46hR18xergOgDrLaysRxzUZiFI2BOimjDtARViyyxZRSeVEsN3oILMLpWRukOPRt3czKfSbffpRq4Nw-QSlsTQQovruwQ5x27AgZ7ENApYSOgGKF5GF~hbOJYVbTchDUHNvyHChwmLPgENTefM3ZeGS1-Vs0X2XUL~pbIDeVdVUvLrwj~McjPzZuvXq-XB26qbD3jWNQrhmEG31OUVUfGvsbC2xdkur9EJwTCssA__"
tar -xzvf cellranger-9.0.1.tar.gz
export PATH=/opt/cellranger-9.0.1:$PATH

wget -O cellranger-atac-2.1.0.tar.gz "https://cf.10xgenomics.com/releases/cell-atac/cellranger-atac-2.1.0.tar.gz?Expires=1739846838&Key-Pair-Id=APKAI7S6A5RYOXBWRPDA&Signature=e91w5zq4U~sU4G3ibOj1fvO5HW19FrwFMs8WpsresMLUy~IoBbI2FfZbB3QsC1UvrXZjqZ2f4WEkLz36Ww7nfdI37-AkOnpaVZVt3gjwjnoUPfAbLdM3p1S37AgEtGJ00TOS4xzP3l1rxfV-9aGnIlGCVGojtQfT20L3j0mydvUVPmhvs2HXqzdbtgDcUeFU-d8YBt7GvcFrSaM6d4veWXgMKeX1K8fn7s9AlsvBfKeRAKTZu6UPK8w4DTbCpB9--nmTDNyKJjRH9I6AhIXp0NmDDJ81wuhVDQ5f6x0o1q0yX1UWnv8oWbvF5bAtUgLqF68E9v8L-2cANe1pgpjKCA__"
tar -xzvf cellranger-atac-2.1.0.tar.gz
export PATH=/opt/cellranger-atac-2.1.0:$PATH

```

Instead of downloading cellranger softwares to your environment and only if you use wexac you can run:

```bash

ml CellRanger/9.0.0
ml CellRanger-ATAC/2.0.0

```

## Example notebook
