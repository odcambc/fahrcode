# STROMBOLI: Sequencing Through Rapid Optimization of Mutational Barcode Orientation and Linkage Identification

**A Snakemake pipeline for nanopore-based barcode variant mapping**

This is a [Snakemake](https://snakemake.readthedocs.io/en/stable/) pipeline for processing barcoded long-read sequencing data. The pipeline is designed to take noisy nanopore data, robustly identify and cluster barcode sequences, then call consensus variants for each barcode cluster.

## Quick start

```bash
git clone https://github.com/odcambc/STROMBOLI
cd STROMBOLI
conda env create --file stromboli_env.yaml
conda activate STROMBOLI
```

Note: for ARM64 Macs, try the following (assuming [Rosetta](https://support.apple.com/en-us/102527) is installed):

```bash
git clone https://github.com/odcambc/STROMBOLI
cd STROMBOLI
CONDA_SUBDIR=osx-64 conda env create --file stromboli_env.yaml
conda activate STROMBOLI
```

## Overview

The pipeline proceeds in the following steps:

1. **Barcode identification**: Putative barcode sequences are identified by matching constant flanking regions using cutadapt.
2. **Barcode clustering**: The barcodes are clustered and canonical sequences are identified using starcode.
3. **Variant sequence grouping**: All reads corresponding to a single barcode are grouped together.
4. **Read mapping**: Each barcode group is mapped to a reference genome using minimap2.
5. **Variant calling**: Variants are called using bcftools.

## Roadmap

- [ ] Complete pipeline (all rules and scripts)
  - [ ] Need to make a scatter-gather rules for handling the new groups of barcodes generated by starcode
- [ ] Add tests
- [ ] Add documentation (usage, installation, etc.)
- [ ] QC and visualization output
- [ ] Perform [parameter optimization](https://snakemake.readthedocs.io/en/stable/snakefiles/rules.html#parameter-space-exploration)
  - [ ] cutadapt stringency
  - [ ] starcode clustering parameters
  - [ ] minimap2 mapping parameters
  - [ ] bcftools variant calling parameters
    - [ ] Minimum barcode group size to call variants?
    - [ ] Q-score weighting?
    - [ ] Imputing missing data as WT?

## Installation

### Dependencies

#### Via conda (recommended)

The simplest way to handle dependencies is with [Conda](https://conda.io/docs/) and the provided environment file.

```bash
conda env create --file stromboli_env.yaml
```

If using an ARM64 Mac, try the following:

```bash
CONDA_SUBDIR=osx-64 conda env create --file stromboli_env.yaml
```

#### Manually

The following are the dependencies required to run the pipeline:

- [Snakemake](https://snakemake.readthedocs.io/en/stable/)
- [Samtools](http://www.htslib.org/)
- [BCFtools](https://samtools.github.io/bcftools/)
- [minimap2](https://github.com/lh3/minimap2)
- [cutadapt](https://cutadapt.readthedocs.io/en/stable/)
- [starcode](https://github.com/gui11aume/starcode)

## License

This is licensed under the MIT license. See the LICENSE file for details.

## Contributing

Contributions and feedback are welcome. Please submit an issue or pull request.

## Getting help

For any issues, please open an issue on the GitHub repository. For
questions or feedback, [email Chris](https://www.wcoyotelab.com/members/).