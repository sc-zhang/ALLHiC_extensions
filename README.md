# Usage
## Prune
### Dependencies
* htslib
### Installation
This is a new version of ALLHiC_prune, for directly use
```bash
git clone https://github.com/sc-zhang/ALLHiC_components.git
cd Prune
chmod +x ALLHiC_prune
```

For build
```bash
git clone https://github.com/sc-zhang/ALLHiC_components.git
cd Prune
export CPPFLAGS="-I/path/to/htslib/include"
export LDFLAGS="-L/path/to/htslib/lib"
make
```
### Usage
```bash
************************************************************************
    Usage: ./ALLHiC_prune -i Allele.ctg.table -b sorted.bam
      -h : help and usage.
      -i : Allele.ctg.table
      -b : sorted.bam
************************************************************************
```
## Other scripts
### Dependencies
* pysam
* numpy
* matplotlib
* jcvi
### Installation
```bash
git clone https://github.com/sc-zhang/ALLHiC_components.git
chmod +x *.py
chmod +x *.sh
```
### Usage
**partition_gmap.py** is used for spliting bam and contig level fasta by chromosomes with allele table.
```bash
usage: partition_gmap.py [-h] -r REF -g ALLELETABLE [-b BAM] [-d WORKDIR]
                         [-t THREAD]

optional arguments:
  -h, --help            show this help message and exit
  -r REF, --ref REF     reference contig level assembly
  -g ALLELETABLE, --alleletable ALLELETABLE
                        Allele.gene.table
  -b BAM, --bam BAM     bam file, default: prunning.bam
  -d WORKDIR, --workdir WORKDIR
                        work directory, default: wrk_dir
  -t THREAD, --thread THREAD
                        threads, default: 10
```

**ALLHiC_partition.py** is an **experimental** script for clustering contigs into haplotypes.
```bash
usage: ALLHiC_partition.py [-h] -r REF -b BAM -d BED -a ANCHORS -p POLY
                           [-e EXCLUDE] [-o OUT]

optional arguments:
  -h, --help            show this help message and exit
  -r REF, --ref REF     Contig level assembly fasta
  -b BAM, --bam BAM     Prunned bam file
  -d BED, --bed BED     dup.bed
  -a ANCHORS, --anchors ANCHORS
                        anchors file with dup.mono.anchors
  -p POLY, --poly POLY  Ploid count of polyploid
  -e EXCLUDE, --exclude EXCLUDE
                        A list file contains exclude contigs for partition,
                        default=""
  -o OUT, --out OUT     Output directory, default=workdir
```

**ALLHiC_rescue.py** is a new version of rescue use jcvi to prevent the collinear contigs be rescued to same group.
```bash
usage: ALLHiC_rescue.py [-h] -r REF -b BAM -c CLUSTER -n COUNTS -g GFF3 -j
                        JCVI [-e EXCLUDE] [-w WORKDIR]

optional arguments:
  -h, --help            show this help message and exit
  -r REF, --ref REF     Contig level assembly fasta
  -b BAM, --bam BAM     Unprunned bam
  -c CLUSTER, --cluster CLUSTER
                        Cluster file of contigs
  -n COUNTS, --counts COUNTS
                        count REs file
  -g GFF3, --gff3 GFF3  Gff3 file generated by gmap cds to contigs
  -j JCVI, --jcvi JCVI  CDS file for jcvi, bed file with same prefix must
                        exist in the same position
  -e EXCLUDE, --exclude EXCLUDE
                        cluster which need no rescue, default="", split by
                        comma
  -w WORKDIR, --workdir WORKDIR
                        Work directory, default=wrkdir
```

**ALLHiC_plot.py** is used to plot heatmap of Hi-C singal, and compare with original version, it can reduce the usage of memory, and easier plot heatmap with other resolution.
```bash
usage: ALLHiC_plot.py [-h] -b BAM -a AGP -l LIST [-n NPZ] [-m MIN_SIZE]
                      [-s SIZE] [-o OUTDIR]

optional arguments:
  -h, --help            show this help message and exit
  -b BAM, --bam BAM     Input bam file
  -a AGP, --agp AGP     Input AGP file
  -l LIST, --list LIST  Chromosome list, contain: ID Length
  -n NPZ, --npz NPZ     npz file of hic signal, optional, if not exist, it
                        will be generate after reading hic signals, or it will
                        be loaded for drawing other resolution of heatmap
  -m MIN_SIZE, --min_size MIN_SIZE
                        Minium bin size of heatmap, default=50k
  -s SIZE, --size SIZE  Bin size of heatmap, can be a list separated by comma,
                        default=500k, notice: it must be n times of min_size
                        (n is integer) or we will ajust it to nearest one
  -o OUTDIR, --outdir OUTDIR
                        Output directory, default=workdir
```

**Other scripts** are under development, and not recommend to use.