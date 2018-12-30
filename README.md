## Thicket


Parallel bootstrapping for Maximum-Likelihood (ML) phylogenies using Nextflow

[![Nextflow](https://img.shields.io/badge/nextflow-%E2%89%A50.32.0-brightgreen.svg)](https://www.nextflow.io/)
![Singularity Container available](https://img.shields.io/badge/singularity-available-7E4C74.svg)

## Introduction

**Thicket** is a Nextflow wrapper around popular the ML phylogeny frameworks `RAxML-NG`, `PhyML` and `FastTree`. It parallelizes bootstrap computation (`Felsenstein`, `Transfer Bootstrap Expectation`, `Shimodaira-Hasegawa like local support values`) on any distributed system available through Nextflow using `conda` environments, cloud support for `AWS Batch` and soon `Google Cloud`, as well as containerization with `Singularity`.

The pipeline computes bootstrap replicates of an alignment using `golign` and can launch each replicate in a separate submission to job executors supported by Nextflow, such as the `local` system, `PBS/Torque` or `SGE`. If the input is a variant file in binary `Plink` format for diploid genomes, a concatenated alignment can be generated, with options to exclude invariant sites or translate heterozygous sites into ambiguous IUPAC DNA codes. Bootstraps are summarized onto a main phylogeny using methods selected from the tree constructors. User-defined option strings for the main phylogeny and bootstrap replicates expose all arguments of the command line interfaces from the ML software used in **Thicket**.

**Thicket** was built to facilitate large parallel computation of bootstrap values (> 100 cores) for high density genome array data from diploid organisms (canine genome, in this case), but can be used for any other data, where computation of a large number of bootstrap replicate trees is computationally infeasible on systems with fewer cores or where tree estimation is time consuming.

## Pipeline steps

By default alignment input, the pipeline currently performs the following:

* Generates bootstrap replicates of the alignment (`Goalign`)
* Launches each bootstrap computation in the ML software (`RAxML-NG`, `PhyML 3` or `FastTree 2`)
* Launches computation of main phylogeny to map bootstrap values to (`RAxML-NG`, `PhyML 3` or `FastTree 2`)
* Summarizes bootstrap values onto the phylogeny (`RAxML-NG`, `PhyML 3` or `FastTree 2`)
* Provides summary of bootstrap statistics and distribution (`Gotree`)

If the input is a diploid genome and a variant file in binary PLINK format (`Plink`)

* Concatenate and optionally translate into ambiguous IUPAC codes to generate input alignment (`BioPython`) 

## Quick Start

1. Install [`nextflow`](docs/installation.md)
2. Install [`conda`](https://conda.io/miniconda.html)
3. Download the pipeline

```bash
nextflow pull esteinig/thicket
```

4. Set up your job with default parameters using `RAxML-NG`, model `GTRG+G` and default 100 bootstraps


```bash
nextflow run thicket -profile <local/pbs/sge/slurm> --alignment <align.fasta>
```

5. See the overview of the run under default `thicket/thicket.html`, bootstrapped 
tree in `thicket/thicket.tree` and bootstrap trees in `thicket/bootstraps.tree`

Modifications to the default pipeline are easily made using various options
as described in the documentation.

## Documentation

Thicket comes with documentation about the pipeline, found in the `docs/` directory:

1. [Installation](docs/installation.md)
2. Pipeline configuration
    * [Local installation](docs/configuration/local.md)
    * [Adding your own system](docs/configuration/adding_your_own.md)
3. [Running the pipeline](docs/usage.md)
4. [Output and how to interpret the results](docs/output.md)
5. [Troubleshooting](docs/troubleshooting.md)

This template will be used for `nf-core` release of Thicket.

## Credits

This pipeline was written by Eike Steinig ([esteinig](https://github.com/esteinig)), 
as part of an initiative to study dingo populations using high density genomic data
in collaboration with Kyall Zenger at James Cook University.

## References


* **RAxML-NG** download: [https://github.com/amkozlov/raxml-ng/](https://github.com/amkozlov/raxml-ng/)
* **PhyML** 
* **FastTree**
* **Goalign** download: [https://github.com/amkozlov/raxml-ng/](https://github.com/amkozlov/raxml-ng/)
* **Gotree** download: [https://github.com/amkozlov/raxml-ng/](https://github.com/amkozlov/raxml-ng/)
* **Nextflow**


