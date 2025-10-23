# CellRangerIDE

Hey everybody!

In this section you find explanation about the script that runs CellRanger pipelines 
such as: converting BCL to fastqs files, alignment with\without multiple samples,
various options inside the pipeline like: include introns or not in the alignment, read 3’ or 5’ and so on.

**Location:**

Currently the CellRangerIDE is located in the next GitHub URL:
https://github.com/yoavnahum21/CellRangerIDE.git. 

you can find the Implementation code in the CellRangerIDE\Backhand\Scripts

**Inititiallization** 

```bash
 BIN_PATH=$(dirname$(which python))
 chmod +x ./CellRangerIDE/BackHand/Scripts/main.py
 cp ./CellRangerIDE/BackHand/Scripts/main.py $BINPATH/yosefranger
```

    
**Instructions:** 

1) Fill out the general config file.

2) The general_config.yml file is located inside the const_files folder.

3) In the pipeline choose whatever you desire, your options are:

a) mkfastq - creating fastqs out of bcl

b) count - creating count matrixes and h5 files for single sample

c) multi - creating count matrixes and h5 files for multiple samples using hashtag oligos.

d) vdj - creating count matrixes for vdj

e) mkref - creating custom/filtered transcriptome reference - TBD 

f) qc score - returns a score of the specific process

g) cellbender - remove ambient rna noises

4) according to what you have chosen in the pipeline you should fill out the right second config file named {pipeline)_config.yml

5) The config.yml file is divided into several types:

a) Optional: means this field is not necessary to the pipeline’s inputs.

b) Required: means that if you submit something not valid, the pipeline won’t work for you.

c) Default: means that if you don’t submit something there is a default input that the pipeline 
     will use. (the default is also written in the comment above).

### Requirements

- For running the cellranger software, please use:
1)  Option 1: if you are running on wexac just run before:
    
    ```bash
    ml CellRanger/9.0.0
    ml CellRanger-ATAC/2.0.0
    ```
    
    2)  Option 2: just download cellranger/cellranger-atac and add it to your path:
          For cellranger:
    
    ```bash
    #!/bin/bash
    cd /opt
    wget -O cellranger-9.0.1.tar.gz "https://cf.10xgenomics.com/releases/cell-exp/cellranger-9.0.1.tar.gz?Expires=1739846992&Key-Pair-Id=APKAI7S6A5RYOXBWRPDA&Signature=lWj4nhoNebGYpV7bZzkYzxxmnhdlFD0zuLKtbLQsqPevb5VRscVDDsEdlnXdjnavCB6vyQMJ8DzgH9CHZqFIWwIfJz8jL4iPDGXXIZq4zqW1LG46hR18xergOgDrLaysRxzUZiFI2BOimjDtARViyyxZRSeVEsN3oILMLpWRukOPRt3czKfSbffpRq4Nw-QSlsTQQovruwQ5x27AgZ7ENApYSOgGKF5GF~hbOJYVbTchDUHNvyHChwmLPgENTefM3ZeGS1-Vs0X2XUL~pbIDeVdVUvLrwj~McjPzZuvXq-XB26qbD3jWNQrhmEG31OUVUfGvsbC2xdkur9EJwTCssA__"
    tar -xzvf cellranger-9.0.1.tar.gz
    export PATH=/opt/cellranger-9.0.1:$PATH
    ```
    

             For cellranger-atac:

```bash
#!/bin/bash
cd /opt
wget -O cellranger-atac-2.1.0.tar.gz "https://cf.10xgenomics.com/releases/cell-atac/cellranger-atac-2.1.0.tar.gz?Expires=1739846838&Key-Pair-Id=APKAI7S6A5RYOXBWRPDA&Signature=e91w5zq4U~sU4G3ibOj1fvO5HW19FrwFMs8WpsresMLUy~IoBbI2FfZbB3QsC1UvrXZjqZ2f4WEkLz36Ww7nfdI37-AkOnpaVZVt3gjwjnoUPfAbLdM3p1S37AgEtGJ00TOS4xzP3l1rxfV-9aGnIlGCVGojtQfT20L3j0mydvUVPmhvs2HXqzdbtgDcUeFU-d8YBt7GvcFrSaM6d4veWXgMKeX1K8fn7s9AlsvBfKeRAKTZu6UPK8w4DTbCpB9--nmTDNyKJjRH9I6AhIXp0NmDDJ81wuhVDQ5f6x0o1q0yX1UWnv8oWbvF5bAtUgLqF68E9v8L-2cANe1pgpjKCA__"
tar -xzvf cellranger-atac-2.1.0.tar.gz
export PATH=/opt/cellranger-atac-2.1.0:$PATH

```

- For running cellbender first use the next environment:

[cbenv.yaml](attachment:8a4de6d5-b2ee-442d-9a50-144a8321900a:cbenv.yaml)

     For running any different pipeline please use the next environment:

[crenv.yaml](attachment:8885160b-c352-4b32-8433-3d65f21b876a:crenv.yaml)

```bash
# In case you are using cellbender
conda env create -f cbenv.yml
conda activate cellbender

# in case you are using something else
conda env create -f crenv.yml
conda activate cellranger

```

**NOTE:** 

- In the config files there are 3 types of files: string, list, int.
Don't change it!
- If you try to run mkfastq pipeline use before:
module load bcl2fastq2 in the terminal, if you rather have another binary file of bcl2fastq2 instead, just make sure you add the parent folder to your path using: `export $PATH:={your_bcl2fastq2_parent_folder_path}` in the terminal.
- In the config files, make sure that several lists need to have the same number of elements. (should be clarified in the comments above each attribute)
- If you decide using an aligner, we encourage you to use the multi pipeline.
This aligner generalize all kind of feature types including: Gene expression, Antibody Capture, VDJ etc.
- Please be in touch with Yoav for any further questions :)

## **Further details about the inputs of the pipeline:**

- **config_general.yml:**
    
    ![Screenshot 2025-02-16 at 11.41.01.png](attachment:9672472f-4f1b-482b-a6fb-5e27b0521142:Screenshot_2025-02-16_at_11.41.01.png)
    
    project_name: give your project a name
    
    id: this is your output from cellranger in case you are using one of its pipelines
    
    pipeline: choose your pipeline out of the list: cellbender, demulti, flex, mkfastq, mkref, multi, qc 
    
    aligner_software_path: give the path of aligner (in case you are using it), if you have exported your aligner to $PATH environment variable just use the aligner name instead.
    The aligner options:
    - cellranger
    - cellranger-atac
    
    running_machine: are you using your Wexac or your PC? for Wexac just write Wexac or use Default, for you PC write PC or leave empty
    
    aws_ec2: TBD
    
    **Runtime parameters:**
    Nothing to elaborate
    
    ________________________________________________________________________________
    
- **config_count_pipeline.yml:**
    
    ![Screenshot 2025-02-16 at 15.19.47.png](attachment:f3882ea8-771b-4f7b-bd13-82b584c67dfd:Screenshot_2025-02-16_at_15.19.47.png)
    
    id: A unique run ID string (e.g., sample345). The name is arbitrary and will be used to name the directory containing all pipeline-generated files and outputs.
    
    alignment_ref_genome_file: Path to folder containing a Cell Ranger GEX/ATAC reference.
    
    fastq_path: Path of the fastq path folder
    
    ________________________________________________________________________________
    
- **config_cellbender_pipeline.yml:**
    
    ![Screenshot 2025-02-16 at 15.20.18.png](attachment:4b98c1e9-0bd5-49ef-9e03-c655fd6693f0:Screenshot_2025-02-16_at_15.20.18.png)
    
    data_path: add the path to your cellranger output directory
    
    chosen_pipeline: specify what kind of pipeline you used to align your samples
    
    ________________________________________________________________________________
    
- **config_demulti_pipeline.yml:**
    
    
    ![Screenshot 2025-02-16 at 16.06.30.png](attachment:0c697a9a-9a6f-45d5-90f9-5f7147af5971:Screenshot_2025-02-16_at_16.06.30.png)
    
    adata_path: add you h5 you wish to use
    
    sample_names: give an arbitrary name according to the adata_path you are using
    
    hto_list_per_sample: give the hashes names in each sample
    
    demultiplex_method: there are 2 demultiplex algorithm we are using, hashsolo and demultiplex2, check out in both documentation what are the difference between them.
    hashsolo: https://www.sciencedirect.com/science/article/pii/S2405471220301952?via%3Dihub
    
    demultiplex2: https://genomebiology.biomedcentral.com/articles/10.1186/s13059-024-03177-y
    
    priors: only relevant when using hashsolo, those three elements describes the a-priors probabilities of each hypothesis: singlet, doublet, empty droplet
    
    ________________________________________________________________________________
    
- **config_flex_pipeline.yml:**
    
    ![Screenshot 2025-02-16 at 15.21.42.png](attachment:ee9708f3-2dce-4ad7-95fe-e3afc4e894d9:Screenshot_2025-02-16_at_15.21.42.png)
    

![Screenshot 2025-02-16 at 15.21.56.png](attachment:32a0d9a6-a042-47aa-ac17-a0e7f2795ea7:Screenshot_2025-02-16_at_15.21.56.png)

alignment_ref_genome_file: add reference genome path for gene expressions

when using flex you have 2 options:
**option 1:** using INCPM link

INCPM_link: add the link you get from INCPM of the fastqs

INCPM_directory: where all the data will be downloaded

**Note:** if you are using option 1, pay attention you will be still asked for more inputs while running the main.py

**option2:** manual option

fastq_path: add the paths for fastqs parent folder

probe_set_path:

create_bam: True/False, do you wish to include bam in your output?

include_intros: True/False, do you wish to include introns while aligning?

expected_cell: estimate the number of expected cells in your experiment, you can leave it blanc

sample_name: arbitrary name for your sample, usually named after the prefix in the fastq

fastq_folders_name: necessarily has to be the prefix of the fastqs
E.G: the fastq file is: 
PAC-i03-HmYC003-UNT-BMd000-xIPx-1-GEX-C_S2_L001_I1_001.fastq.gz
The prefix is:
PAC-i03-HmYC003-UNT-BMd000-xIPx-1-GEX-C

lanes_used: just leave as Default

multiplexing method: in case you are using hashes, choose your method: “feature_barcode” (hashtag oligos) or “cmo_barcode”

probe_barcode_csv: add a csv file that elaborates your multiplexing experiment according to cellranger csv format.
# In case you didn’t uploaded a csv file

sample_id_probe: arbitrary name for your sample

probe_barcode_ids: arbitrary number for  your barcode

probe_description: copied from sample_id_probe

________________________________________________________________________________

- **config_mkfastq_pipeline.yml:**
    
    ![Screenshot 2025-02-16 at 15.23.03.png](attachment:a5bfb898-3e39-4e6c-bb52-51369617f599:Screenshot_2025-02-16_at_15.23.03.png)
    
    TBD
    
    ________________________________________________________________________________
    
- **config_mkref_pipeline.yml:**
    
    ![Screenshot 2025-02-16 at 15.23.21.png](attachment:306e7b4e-8688-4265-977c-0e0b0e76a700:Screenshot_2025-02-16_at_15.23.21.png)
    

TBD

________________________________________________________________________________

- **config_multi_pipeline..yml:**
    
    ![Screenshot 2025-02-16 at 15.24.12.png](attachment:b64b9c0f-55c6-4d62-a84c-55fbab406f6c:Screenshot_2025-02-16_at_15.24.12.png)
    

![Screenshot 2025-02-16 at 15.24.37.png](attachment:12f08ac6-f403-4f2c-9a83-c921a679171a:Screenshot_2025-02-16_at_15.24.37.png)

alignment_ref_genome_file:  add reference genome path for gene expressions

alignment_ref_vdj_file: add reference genome path for vdj

when using multi you have 2 options:

**option 1:** using INCPM link

INCPM_link: add the link you get from INCPM of the fastqs

INCPM_directory: where all the data will be downloaded

**Note:** if you are using option 1, pay attention you will be still asked for more inputs while running the main.py

**option2:** manual option

fastq_path: add the paths for fastqs parent folder 

create_bam: True/False, do you wish to include bam in your output?

include_intros: True/False, do you wish to include introns while aligning?

expected_cell: estimate the number of expected cells in your experiment, you can leave it blanc 

R1_length: what is the number of counted nucleotides from R1

R2_length: what is the number of counted nucleotides from R2

sample_name: arbitrary name for your sample, usually named after the prefix in the fastq 

fastq_folders_name: necessarily has to be the prefix of the fastqs
E.G: the fastq file is: 
PAC-i03-HmYC003-UNT-BMd000-xIPx-1-GEX-C_S2_L001_I1_001.fastq.gz
The prefix is:
PAC-i03-HmYC003-UNT-BMd000-xIPx-1-GEX-C

lanes_used: just leave as Default

multiplexing method: in case you are using hashes, choose your method: “feature_barcode” (hashtag oligos) or “cmo_barcode”

feature_types: respectively your submit in the sample name/fastq_folders_name please add their types: Gene Expression, Antibody Capture, CRISPR Guide Capture, Multiplexing Capture, VDJ-B, VDJ-T, VDJ-T-GD, Antigen Capture #5', Antigen Capture only 

**In case you are using feature_barcode:**

feature_reference_csv: In case you have a prepared csv please add the path

otherwise do it manually: 

hto_id: give the hashes a name

hto_names: usually are the same as hto_id

hto_read: declare which reading you are concatenate your hashes “R1” or “R2”

hto_pattern: explain where exactly the barcode are

hto_sequence: what is the sequence of each hash

HTO_feature_type: most of the time is anybody

**In case you are using cmo_barcode:**

cmo_barcode_csv: In case you have a prepared csv please add the path

sample_id_cmo: 

cmo_id:

________________________________________________________________________________

- **config_qc.yml:**
    
    Nothing needs to be added
