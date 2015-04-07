# rootstock

To run this analysis I used:
fastqc
bowtie2
samtools
bcftools
beagle

Data was unzipped and concatenated into R1 and R2 files in the subdirectory conc within each rootstock folder
eg:
```shell
gunzip *
cat 863_LIB6292_LDI5172_GTGAAA_L00*_R1.fastq.gz >m27_r1.fa
```

within the conc directory of each genome folder, fastqc was run on each pair of reads in order to assess the quality
```shell
nohup fastqc m116_r1.fq m116_r2.fq &
nohup fastqc m27_r1.fq m27_r2.fq &
nohup fastqc m9_r1.fq m9_r2.fq &
nohup fastqc m13_r1.fq m13_r2.fq &
nohup fastqc mm106_r1.fq mm106_r2.fq &
nohup fastqc gala_r1.fq gala_r2.fq &
nohup fastqc o3_r1.fq o3_r2.fq &

 ```
 
Trimming was performed with fastq-mcf 
```shell
./fastq-mcf.sh /home/groups/harrisonlab/project_files/rootstock_genetics/m27/conc/m27_r1.fq /home/groups/harrisonlab/project_files/rootstock_genetics/m27/conc/m27_r2.fq /home/groups/harrisonlab/project_files/rootstock_genetics/m27/conc/ 
./fastq-mcf.sh /home/groups/harrisonlab/project_files/rootstock_genetics/m13/conc/m13_r1.fq /home/groups/harrisonlab/project_files/rootstock_genetics/m13/conc/m13_r2.fq /home/groups/harrisonlab/project_files/rootstock_genetics/m13/conc/ 
./fastq-mcf.sh /home/groups/harrisonlab/project_files/rootstock_genetics/m116/conc/m116_r1.fq /home/groups/harrisonlab/project_files/rootstock_genetics/m116/conc/m116_r2.fq /home/groups/harrisonlab/project_files/rootstock_genetics/m116/conc/ 
./fastq-mcf.sh /home/groups/harrisonlab/project_files/rootstock_genetics/m9/conc/m9_r1.fq /home/groups/harrisonlab/project_files/rootstock_genetics/m9/conc/m9_r2.fq /home/groups/harrisonlab/project_files/rootstock_genetics/m9/conc/ 
./fastq-mcf.sh /home/groups/harrisonlab/project_files/rootstock_genetics/mm106/conc/mm106_r1.fq /home/groups/harrisonlab/project_files/rootstock_genetics/mm106/conc/mm106_r2.fq /home/groups/harrisonlab/project_files/rootstock_genetics/mm106/conc/ 
./fastq-mcf.sh /home/groups/harrisonlab/project_files/rootstock_genetics/gala/conc/gala_r1.fq /home/groups/harrisonlab/project_files/rootstock_genetics/gala/conc/gala_r2.fq /home/groups/harrisonlab/project_files/rootstock_genetics/gala/conc/
./fastq-mcf.sh /home/groups/harrisonlab/project_files/rootstock_genetics/o3/conc/o3_r1.fq  /home/groups/harrisonlab/project_files/rootstock_genetics/o3/conc/ 

./fastq-mcf.sh /home/groups/harrisonlab/project_files/rootstock_genetics/test/conc/test_r1.fq /home/groups/harrisonlab/project_files/rootstock_genetics/test/conc/test_r2.fq /home/groups/harrisonlab/project_files/rootstock_genetics/test/conc/

 ```
 
 Removal of phix
 ```shell
./bowtie.sh /home/groups/harrisonlab/project_files/rootstock_genetics/test/conc/test_r1.fq.trim /home/groups/harrisonlab/project_files/rootstock_genetics/test/conc/test_r2.fq.trim /home/groups/harrisonlab/ref_genomes/phix/phix /home/groups/harrisonlab/project_files/rootstock_genetics/test/conc/ phix_filtered.sam 50 500
 
./bowtie.sh /home/groups/harrisonlab/project_files/rootstock_genetics/m27/conc/m27_r1.fq.trim /home/groups/harrisonlab/project_files/rootstock_genetics/m27/conc/m27_r2.fq.trim /home/groups/harrisonlab/ref_genomes/phix/phix /home/groups/harrisonlab/project_files/rootstock_genetics/m27/conc/ phix_filtered 250 500
./bowtie.sh /home/groups/harrisonlab/project_files/rootstock_genetics/m116/conc/m116_r1.fq.trim /home/groups/harrisonlab/project_files/rootstock_genetics/m116/conc/m116_r2.fq.trim /home/groups/harrisonlab/ref_genomes/phix/phix /home/groups/harrisonlab/project_files/rootstock_genetics/m116/conc/ phix_filtered 250 500
./bowtie.sh /home/groups/harrisonlab/project_files/rootstock_genetics/m9/conc/m9_r1.fq.trim /home/groups/harrisonlab/project_files/rootstock_genetics/m9/conc/m9_r2.fq.trim /home/groups/harrisonlab/ref_genomes/phix/phix /home/groups/harrisonlab/project_files/rootstock_genetics/m9/conc/ phix_filtered 250 500
./bowtie.sh /home/groups/harrisonlab/project_files/rootstock_genetics/m13/conc/m13_r1.fq.trim /home/groups/harrisonlab/project_files/rootstock_genetics/m13/conc/m13_r2.fq.trim /home/groups/harrisonlab/ref_genomes/phix/phix /home/groups/harrisonlab/project_files/rootstock_genetics/m13/conc/ phix_filtered 250 500
./bowtie.sh /home/groups/harrisonlab/project_files/rootstock_genetics/mm106/conc/mm106_r1.fq.trim /home/groups/harrisonlab/project_files/rootstock_genetics/mm106/conc/mm106_r2.fq.trim /home/groups/harrisonlab/ref_genomes/phix/phix /home/groups/harrisonlab/project_files/rootstock_genetics/mm106/conc/ phix_filtered 250 500
./bowtie.sh /home/groups/harrisonlab/project_files/rootstock_genetics/gala/conc/gala_r1.fq.trim /home/groups/harrisonlab/project_files/rootstock_genetics/gala/conc/gala_r2.fq.trim /home/groups/harrisonlab/ref_genomes/phix/phix /home/groups/harrisonlab/project_files/rootstock_genetics/gala/conc/ phix_filtered 250 500

./bowtie_se.sh /home/groups/harrisonlab/project_files/rootstock_genetics/o3/conc/o3_r1.fq.trim /home/groups/harrisonlab/ref_genomes/phix/phix /home/groups/harrisonlab/project_files/rootstock_genetics/o3/conc/ phix_filtered 

 ```
  
##Assembly to reference
A hash was created for version 1 of the genome

```shell
cd /home/groups/harrisonlab/project_files/rootstock_genetics/
cd ref
mkdir v1
cd v1
bowtie2-build Malus_x_domestica.v1.0-primary.pseudo.fa Md
```

Made a shell script to submit automatically to grid engine
for version 1 of the genome!!

```shell
./bowtie.sh /home/groups/harrisonlab/project_files/rootstock_genetics/m27/conc/phix_filtered.1 /home/groups/harrisonlab/project_files/rootstock_genetics/m27/conc/phix_filtered.2 /home/groups/harrisonlab/project_files/rootstock_genetics/ref/v1/Md /home/groups/harrisonlab/project_files/rootstock_genetics/m27/analysis_v1/ m27_v1 250 500
./bowtie.sh /home/groups/harrisonlab/project_files/rootstock_genetics/m116/conc/phix_filtered.1  /home/groups/harrisonlab/project_files/rootstock_genetics/m116/conc/phix_filtered.2 /home/groups/harrisonlab/project_files/rootstock_genetics/ref/v1/Md /home/groups/harrisonlab/project_files/rootstock_genetics/m116/analysis_v1/ m116_v1 250 500
./bowtie.sh /home/groups/harrisonlab/project_files/rootstock_genetics/m9/conc/phix_filtered.1  /home/groups/harrisonlab/project_files/rootstock_genetics/m9/conc/phix_filtered.2 /home/groups/harrisonlab/project_files/rootstock_genetics/ref/v1/Md /home/groups/harrisonlab/project_files/rootstock_genetics/m9/analysis_v1/ m9_v1 250 500
./bowtie.sh /home/groups/harrisonlab/project_files/rootstock_genetics/m13/conc/phix_filtered.1  /home/groups/harrisonlab/project_files/rootstock_genetics/m13/conc/phix_filtered.2 /home/groups/harrisonlab/project_files/rootstock_genetics/ref/v1/Md /home/groups/harrisonlab/project_files/rootstock_genetics/m13/analysis_v1/ m13_v1 250 500
./bowtie.sh /home/groups/harrisonlab/project_files/rootstock_genetics/mm106/conc/phix_filtered.1  /home/groups/harrisonlab/project_files/rootstock_genetics/mm106/conc/phix_filtered.2 /home/groups/harrisonlab/project_files/rootstock_genetics/ref/v1/Md /home/groups/harrisonlab/project_files/rootstock_genetics/mm106/analysis_v1/ mm106_v1 250 500
./bowtie.sh /home/groups/harrisonlab/project_files/rootstock_genetics/gala/conc/phix_filtered.1  /home/groups/harrisonlab/project_files/rootstock_genetics/gala/conc/phix_filtered.2 /home/groups/harrisonlab/project_files/rootstock_genetics/ref/v1/Md /home/groups/harrisonlab/project_files/rootstock_genetics/gala/analysis_v1/ gala_v1 250 500

./bowtie_se.sh /home/groups/harrisonlab/project_files/rootstock_genetics/o3/conc/phix_filtered.1  /home/groups/harrisonlab/project_files/rootstock_genetics/ref/v1/Md /home/groups/harrisonlab/project_files/rootstock_genetics/o3/analysis_v1/ o3_v1.sam 

./bowtie.sh /home/groups/harrisonlab/project_files/rootstock_genetics/test/conc/phix_filtered.1 /home/groups/harrisonlab/project_files/rootstock_genetics/test/conc/phix_filtered.2 /home/groups/harrisonlab/project_files/rootstock_genetics/ref/v1/Md /home/groups/harrisonlab/project_files/rootstock_genetics/test/analysis_v1/ test_v1 250 500

```

SAM to BAM and sort
```shell
./samtools.sh /home/groups/harrisonlab/project_files/rootstock_genetics/m27/analysis/m27_v1.sam /home/groups/harrisonlab/project_files/rootstock_genetics/m27/analysis/ m27_v1.bam m27_v1.sorted 
./samtools.sh /home/groups/harrisonlab/project_files/rootstock_genetics/m9/analysis/m9_v1.sam /home/groups/harrisonlab/project_files/rootstock_genetics/m9/analysis/ m9_v1.bam m9_v1.sorted
./samtools.sh /home/groups/harrisonlab/project_files/rootstock_genetics/m116/analysis/m116_v1.sam /home/groups/harrisonlab/project_files/rootstock_genetics/m116/analysis/ m116_v1.bam m116_v1.sorted
./samtools.sh /home/groups/harrisonlab/project_files/rootstock_genetics/m13/analysis/m13_v1.sam /home/groups/harrisonlab/project_files/rootstock_genetics/m13/analysis/ m13_v1.bam m13_v1.sorted 
./samtools.sh /home/groups/harrisonlab/project_files/rootstock_genetics/mm106/analysis/mm106_v1.sam /home/groups/harrisonlab/project_files/rootstock_genetics/mm106/analysis/ mm106_v1.bam mm106_v1.sorted
./samtools.sh /home/groups/harrisonlab/project_files/rootstock_genetics/gala/analysis/gala_v1.sam /home/groups/harrisonlab/project_files/rootstock_genetics/gala/analysis/ gala_v1.bam gala_v1.sorted
./samtools.sh /home/groups/harrisonlab/project_files/rootstock_genetics/o3/analysis/o3_v1.sam /home/groups/harrisonlab/project_files/rootstock_genetics/o3/analysis/ o3_v1.bam o3_v1.sorted

./samtools.sh /home/groups/harrisonlab/project_files/rootstock_genetics/test/analysis_v1/test_v1 /home/groups/harrisonlab/project_files/rootstock_genetics/test/analysis_v1 test.bam test.sorted

```

Note- to index and then view the bam file using a simple text viewer
samtools index m9.sorted.bam
samtools tview m9.sorted.bam ../../ref/v1/Malus_x_domestica.v1.0-primary.pseudo.fa

Once indexed the program qualimap can be used with the BAM files to view statistics such as coverage and insert size etc

Index the reference genome for SAMTOOLS

```shell
cd /home/groups/harrisonlab/project_files/rootstock_genetics/ref/v1
samtools faidx Malus_x_domestica.v1.0-primary.pseudo.fa 

```

Pileup into a single vcf with v1 (http://biobits.org/samtools_primer.html)

```shell
 ./pileup.sh /home/groups/harrisonlab/project_files/rootstock_genetics/ref/v1/Malus_x_domestica.v1.0-primary.pseudo.fa bam_files /home/groups/harrisonlab/project_files/rootstock_genetics piledup.bcf

bcftools view -bvcg pileup.bam > ./vcf/var.raw.bcf
bcftools view ./vcf/var.raw.bcf | vcfutils.pl varFilter -D100 > ./beagle/var.flt.vcf

```

Define the pedigree for beagle
1) pedigree ID, 2) individual ID, 3) father’s ID, and 4) mother’s ID

m116 1 2 3
mm106 2 0 0
m27 3 5 6
o3 4 6 0
m13 5 0 0
m9 6 0 0

NB- To generate a whole consensus sequence
samtools mpileup -uf ref.fa aln.bam | bcftools view -cg - | vcfutils.pl vcf2fq > cns.fq i 

##Phasing with Beagle
http://faculty.washington.edu/browning/beagle_utilities/utilities.html
Note SHAPE could also be used- one advantage here is it can be 'read aware'  https://mathgen.stats.ox.ac.uk/genetics_software/shapeit/shapeit.html#readaware

java –Xmx 12000m –jar beagle.jar gt=./beagle/var.flt.vcf ped=./beagle/pedigree.ped out=beagle chrom=1 nthreads=4


samtools mpileup -uf ref.fa aln1.bam aln2.bam | bcftools view -bvcg - > var.raw.bcf
bcftools view var.raw.bcf | vcfutils.pl varFilter -D100 > var.flt.vcf


http://www.paintmychromosomes.com/

##Transcriptome ASE
http://www.cureffi.org/2013/08/26/allele-specific-rna-seq-pipeline-using-gsnap-and-gatk/
http://alleleseq.gersteinlab.org/downloads.html

The Allelseq pipeline, which uses vcf2diploid, then vcf2snp along with CNVnator 
looks like a good pipline to follow. 
The url above (gerstein) has most of the details and the readme files in vcf2snp is pretty comprehensive


##QTL filtering



##OLD COMMANDS


Made a shell script to submit automatically to grid engine
The reference genome was downloaded from GDR on 17/1/15
Reference location : /home/groups/harrisonlab/ref_genomes/rosaceae/malus/md_v2/Malus_x_domestica.v2.0-pht_assembly.fa

A Bowtie 2 hash was created

```shell
cd /home/groups/harrisonlab/project_files/rootstock_genetics/
mkdir ref
cd ref
bowtie2-build /home/groups/harrisonlab/ref_genomes/rosaceae/malus/md_v2/Malus_x_domestica.v2.0-pht_assembly.fa Md
```

```shell
./bowtie.sh /home/groups/harrisonlab/project_files/rootstock_genetics/m27/conc/m27_r1.fq.trim /home/groups/harrisonlab/project_files/rootstock_genetics/m27/conc/m27_r2.fq.trim /home/groups/harrisonlab/project_files/rootstock_genetics/ref/Md /home/groups/harrisonlab/project_files/rootstock_genetics/m27/analysis/ m27_ge.sam 250 500
./bowtie.sh /home/groups/harrisonlab/project_files/rootstock_genetics/m116/conc/m116_r1.fq.trim /home/groups/harrisonlab/project_files/rootstock_genetics/m116/conc/m116_r2.fq.trim /home/groups/harrisonlab/project_files/rootstock_genetics/ref/Md /home/groups/harrisonlab/project_files/rootstock_genetics/m116/analysis/ m116_ge.sam 250 500
./bowtie.sh /home/groups/harrisonlab/project_files/rootstock_genetics/m9/conc/m9_r1.fq.trim /home/groups/harrisonlab/project_files/rootstock_genetics/m9/conc/m9_r2.fq.trim /home/groups/harrisonlab/project_files/rootstock_genetics/ref/Md /home/groups/harrisonlab/project_files/rootstock_genetics/m9/analysis/ m9_ge.sam 250 500
./bowtie.sh /home/groups/harrisonlab/project_files/rootstock_genetics/m13/conc/m13_r1.fq.trim /home/groups/harrisonlab/project_files/rootstock_genetics/m13/conc/m13_r2.fq.trim /home/groups/harrisonlab/project_files/rootstock_genetics/ref/Md /home/groups/harrisonlab/project_files/rootstock_genetics/m13/analysis/ m13_ge.sam 250 500 
./bowtie.sh /home/groups/harrisonlab/project_files/rootstock_genetics/mm106/conc/mm106_r1.fq.trim /home/groups/harrisonlab/project_files/rootstock_genetics/mm106/conc/mm106_r2.fq.trim /home/groups/harrisonlab/project_files/rootstock_genetics/ref/Md /home/groups/harrisonlab/project_files/rootstock_genetics/mm106/analysis/ mm106_ge.sam 250 500
```
Convert SAM to BAM and sort BAM for SNP calling
Do this by SGE script
```shell
./samtools.sh /home/groups/harrisonlab/project_files/rootstock_genetics/m27/analysis/m27_ge.sam /home/groups/harrisonlab/project_files/rootstock_genetics/m27/analysis/ m27.bam m27.sorted 
./samtools.sh /home/groups/harrisonlab/project_files/rootstock_genetics/m9/analysis/m9_ge.sam /home/groups/harrisonlab/project_files/rootstock_genetics/m9/analysis/ m9.bam m9.sorted
./samtools.sh /home/groups/harrisonlab/project_files/rootstock_genetics/m116/analysis/m116_ge.sam /home/groups/harrisonlab/project_files/rootstock_genetics/m116/analysis/ m116.bam m116.sorted
./samtools.sh /home/groups/harrisonlab/project_files/rootstock_genetics/m13/analysis/m13_ge.sam /home/groups/harrisonlab/project_files/rootstock_genetics/m13/analysis/ m13.bam m13.sorted 
./samtools.sh /home/groups/harrisonlab/project_files/rootstock_genetics/mm106/analysis/mm106_ge.sam /home/groups/harrisonlab/project_files/rootstock_genetics/mm106/analysis/ mm106.bam mm106.sorted

```
Index the reference genome for SAMTOOLS
```shell
samtools faidx Malus_x_domestica.v2.0-pht_assembly.fa 

```
Pileup into a single vcf

```shell
#samtools mpileup -uf ./ref/Malus_x_domestica.v2.0-pht_assembly.fa.fai  ./m9/analysis/m9-sorted.bam  ./m27/analysis/m27-sorted.bam  ./m116/analysis/m116-sorted.bam  ./mm106/analysis/mm106-sorted.bam  ./m13/analysis/m13-sorted.bam | bcftools view -bvcg - > ./vcf/var.raw.bcf

samtools mpileup -uf ./ref/Malus_x_domestica.v2.0-pht_assembly.fa  ./m9/analysis/m9.sorted.bam  ./m27/analysis/m27.sorted.bam  ./m116/analysis/m116.sorted.bam  ./mm106/analysis/mm106.sorted.bam  ./m13/analysis/m13.sorted.bam >pileup.bam
bcftools view -bvcg pileup.bam > ./vcf/var.raw.bcf
bcftools view ./vcf/var.raw.bcf | vcfutils.pl varFilter -D100 > ./beagle/var.flt.vcf

```
