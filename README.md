Docker container run environment for BUSCO (*Benchmarking Universal Single-Copy Orthologs*)

> About BUSCO
> BUSCO v3 provides quantitative measures for the assessment of genome assembly, gene set, and transcriptome completeness, based on evolutionarily-informed expectations of gene content from near-universal single-copy orthologs selected from OrthoDB v9.

> BUSCO assessments are implemented in open-source software, with a large selection of lineage-specific sets of Benchmarking Universal Single-Copy Orthologs. These conserved orthologs are ideal candidates for large-scale phylogenomics studies, and the annotated BUSCO gene models built during genome assessments provide a comprehensive gene predictor training set for use as part of genome annotation pipelines.

> - http://busco.ezlab.org/


## Usage

To run, mount your input directory with -v, and then use standard run_BUSCO.py commands. For example, to run the proteins annotation check (with `-m proteins`) on a fasta called `seq.faa` in the current directory, use the following:

``` bash
docker run \
  -v "$PWD":/input \
  kastman/busco:3.0.0 \
  --in /input/seq.faa \
  -m proteins -o out_label -m proteins
```

You will probably want to grab the correct lineage profile from the Busco site. For example,
to run with the high-level `fungi` dataset, first download the profile and then pass it as an argument when running.

``` bash
lineage=fungi_odb9
wget http://busco.ezlab.org/datasets/$lineage.tar.gz
tar -xzvf $lineage.tar.gz && rm $lineage.tar.gz

docker run \
  -v "$PWD":/input \
  kastman/busco-docker:3.0.0 \
  --in /input/seq.faa \
  --lineage_path /input/$lineage
  -m proteins -o out_label -m proteins
```

For a complete list of available lineage profiles, see the [full list](http://busco.ezlab.org/frame_wget.html) on the BUSCO site or read the User Guide.

## Note

Currently this docker repo contains only the 3.0.0 version, with and without
R and ggplot2 for plotting (R adds about 400MB to the docker download so it is
not included by default.)

To use the R container, specify it with the `with_r` suffix on the tag: `kastman/busco-docker:3.0.0.with_r`.

## Reference

For more information, see:

BUSCO: assessing genome assembly and annotation completeness with single-copy orthologs.
Felipe A. Simão, Robert M. Waterhouse, Panagiotis Ioannidis, Evgenia V. Kriventseva, and Evgeny M. Zdobnov
Bioinformatics, published online June 9, 2015 [doi:10.1093/bioinformatics/btv351](https://doi.org/10.1093/bioinformatics/btv351).
