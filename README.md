# sbx_lewis2015
Sunbeam extension to reproduce key results from Lewis et al 2015 (PMID: 26468751)

## Background

This report uses the [Sunbeam pipeline](https://github.com/sunbeam-labs/sunbeam) to reproduce results from the 2015 Lewis *et al.* paper entitled "Inflammation, Antibiotics, and Diet as Environmental Stressors of the Gut Microbiome in Pediatric Crohn's Disease" [(PMID: 26468751)](https://www.ncbi.nlm.nih.gov/pubmed/26468751). A key finding of this study was that individuals with Crohn's disease form two distinct clusters by Multidimensional Scaling (MDS)--the dysbiotic cluster tended to have a high human DNA fraction. Here, we test whether we can reproduce this observation using the originial data submitted to the SRA, and compare three different read-based classification methods available in Sunbeam or as Sunbeam extensions: Kaiju, Kraken, and MetaPhlAn2.

## Installing

Make sure you have Sunbeam installed--if not, [see the instructions here](https://sunbeam.readthedocs.io/en/latest/quickstart.html)

Clone the repo into your Sunbeam extensions directory, and install dependencies through Conda:

    source activate sunbeam
    cd $SUNBEAM_DIR/extensions
    git clone https://github.com/louiejtaylor/sbx_lewis2015
    conda install -c bioconda -c conda-forge --file sbx_lewis2015/requirements.txt

You'll want a Kraken database to query--see the [Kraken documentation](http://ccb.jhu.edu/software/kraken/MANUAL.html#kraken-databases) for database-building instructions if you don't already have one.

This report depends on output from two other extensions: [sbx_kaiju](https://github.com/sunbeam-labs/sbx_kaiju) and [sbx_metaphlan](https://github.com/sunbeam-labs/sbx_metaphlan/). Make sure to install them (by following the instructions in the above links) before running this extension, if they are not already installed. As a final check, make sure you've added the config options from both extensions to your Sunbeam configuration file, and that you've included the locations of your Kraken and Kaiju databases in the config file!

## Running

Since the Lewis 2015 data is available through NCBI SRA, all you need to do is pass the SRA project identifier to `sunbeam init`:

    sunbeam init Lewis2015 --data_acc SRP057027
    
And then run Sunbeam, specifying `lewis_report` as the target rule:

    sunbeam run --configfile sunbeam_config.yml --cores 20 lewis_report
    
The report will be located in the `reports` directory in your Sunbeam output folder (usually named `sunbeam_output`).
    
