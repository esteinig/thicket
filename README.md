## Thicket


Parallel bootstrapping for maximum-likelihood phylogenies using Nextflow

[![Build Status](https://travis-ci.org/nf-core/eager.svg?branch=master)](https://travis-ci.org/nf-core/eager)
[![Nextflow](https://img.shields.io/badge/nextflow-%E2%89%A50.32.0-brightgreen.svg)](https://www.nextflow.io/)
[![Singularity Container available](https://img.shields.io/badge/singularity-available-7E4C74.svg)

## Introduction

Thicket is a Nextflow wrapper around popular ML phylogeny framework `RAxML-NG`, `PhyML 3` and `FastTree 2`. It paralellizes bootstrap computation (`Felsenstein`, `Transfer Bootstrap Expectation`, `Shimodaira-Hasegawa like local support values`) on any distributed systems available through Nextflow, including cloud support, `conda` environments, and packaging in `Singularity` containers.

The pipeline computes bootstrap replicates of an alignment using `golign` and can launch each replicate in a separate submission to job executors supported by NExtflow, such as `PBS/Torque` or `SGE`. If the input is a variant file in binary PLINK format for diploid genomes, a concatenated alignment can be generated, with options to exclude invariant sites or translate heterozygous sites into ambiguous IUPAC DNA codes before concatenation. Bootstraps are sumamrized using methods from any of the three tree constructors. Option strings for the main phylogeny and bootstrap replicate processes expose all arguments of the command line interfaces from the ML software used in Thicket.


## Pipeline steps

By default, alignment input to pipeline currently performs the following:

* Generates bootstrap replicates of the alignment (`Goalign`)
* Launches each bootstrap computation in the ML software (`RAxML-NG`, `PhyML 3` or `FastTree 2`)
* Launches computation of main phylogeny to map bootstrap values to (`RAxML-NG`, `PhyML 3` or `FastTree 2`)
* Summarizes bootstrap values onto the phylogeny (`RAxML-NG`, `PhyML 3` or `FastTree 2`)
* Provides summary of bootstrap statistics and distribution (`Gotree`)

If the input is a diploid genome and a variant file in binary PLINK format (`Plink`)

* Concatenate and optionally translate into ambiguous IUPAC codes to generate input alignment (`BioPython`) 
