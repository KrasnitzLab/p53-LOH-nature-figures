
This repository contains data and code used to infer the clonal structure of
cancer cell populations, as described in Baslan et al.

The data directory contains input files for the clonal structure analysis.
There is a subdirectory for each experiment, containing genome-wide estimates of DNA
copy number of the cells in the experiment, one column per cell. Each row corresponds to
a genomic interval (bin). The bins are defined in the mm9*.gz file in the data directory.

The scripts directory contains four R scripts, one per experiment, and a shell script. Executing a script will perform 
clonal structure analysis for the experiment using SCclust R package, with the parameters specified 
in the body of the script. The shell script run_all.sh contains Rscript calls to execute all four R scripts. In adition,
it contains shell commands to produce, for each experiment, the copy-number heat map overlaid with the phylogenetic
tree for the cells in the experiment. The Single-Cell Genome Viewer (SCGV) is invoked for this purpose. The run_all.sh 
script is executed in the Anaconda base environment. For each command, conda is run to activate another Anaconda environment,
in which Rscript or SCGV is executed.

The Dockerfile is used to create a Docker image containing all the data and code for the analysis as described. Before you pull the Docker
image and run the resulting container, make sure that Docker is installed and running on your host computer. Then run the following command 
to perform all the analysis:

```
docker run -it \
    -v '< path to working directory >':/wd \
    krasnitzlab/p53-loh-nature-figures:1.0.1
```

where you should replace **< path to working directory >** with the
absolute path to your working directory.

This command will create a subdirectory named **work** inside your working
directory. All results from data processing will be saved there.

If you prefer to explore the data and the scripts that produce the figures
you can instead start the Docker container using the following command:

```
docker run -it --entrypoint "/bin/bash" \
    -v '< path to working directory >':/wd \
    krasnitzlab/p53-loh-nature-figures:1.0.1
```
