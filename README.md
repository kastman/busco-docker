Docker container run environment for BUSCO (*Benchmarking Universal Single-Copy Orthologs*)

> About BUSCO
> BUSCO v3 provides quantitative measures for the assessment of genome assembly, gene set, and transcriptome completeness, based on evolutionarily-informed expectations of gene content from near-universal single-copy orthologs selected from OrthoDB v9.

> BUSCO assessments are implemented in open-source software, with a large selection of lineage-specific sets of Benchmarking Universal Single-Copy Orthologs. These conserved orthologs are ideal candidates for large-scale phylogenomics studies, and the annotated BUSCO gene models built during genome assessments provide a comprehensive gene predictor training set for use as part of genome annotation pipelines.

> - http://busco.ezlab.org/


## Usage

To run, mount your input and output directories with -v, and then use standard run_BUSCO.py commands. For example, to run the proteins annotation check (with `-m proteins`), use the following:

``` bash
faa_dir=/path/to/input/
faa=seq.faa  # Protein-formatted input files

docker run \
  -v "${faa_dir}":/input \
  kastman/busco:3.0.0 \
  --in /input/$faa \
  -m proteins -o out_label -m proteins
```


## Reference

For more information, see:

BUSCO: assessing genome assembly and annotation completeness with single-copy orthologs.
Felipe A. Simão, Robert M. Waterhouse, Panagiotis Ioannidis, Evgenia V. Kriventseva, and Evgeny M. Zdobnov
Bioinformatics, published online June 9, 2015 [doi:10.1093/bioinformatics/btv351](https://doi.org/10.1093/bioinformatics/btv351).
