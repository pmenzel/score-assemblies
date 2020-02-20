# score-assemblies

A snakemake-wrapper for running [pomoxis](https://github.com/nanoporetech/pomoxis) assess_assembly and assess_homopolymers on multiple assemblies and reference sequences.

## Installation
Clone repository, for example:
```
git clone https://github.com/pmenzel/score-assemblies.git /opt/software/score-assemblies
```
Install dependencies into an isolated conda environment
```
conda env create -n score-assemblies --file /opt/software/score-assemblies/environment.yaml
```
and activate environment:
```
source activate score-assemblies
```

## Usage
First, prepare a data folder, which must contain subfolders for the assemblies and the reference genomes.
```
.
├── assemblies
│   ├── raven.fa
│   ├── raven+medaka.fa
│   └── raven+medaka+pilon.fa
│   
└── references
    ├── reference1.fa
    └── reference2.fa
```

Run workflow, e.g. with 20 allocated threads:
```
snakemake -s /opt/software/score-assemblies/Snakefile --cores 20
```


### Modules
Currently, score-assemblies will run these sub-modules:

#### [pomoxis](https://github.com/nanoporetech/pomoxis) assess_assembly and assess_homopolymers

Each assembly will be scored against each reference genome using these two scripts.  
Additionally to the tables and plots from pomoxis, summary plots for each reference genome will be created in the plots folder.

#### busco

Set the lineage via the snakemake call:
```
snakemake -s /opt/software/score-assemblies/Snakefile --cores 20 --config busco_lineage=burkholderiales
```
If not set, the default lineage `bacteria` will be used.
Available datasets can be listed with `busco --list-datasets`

