####Scripts were modified from several sources,but in the ones can be found also in https://catchenlab.life.illinois.edu/stacks/manual/
#### Please do not forget to change paths to files accordingly
#### I had to build all the pipeline from the scratch, hence the lines directing to program paths. You might have them in your server already.

###align data to a reference genome
mkdir mapped
PATH=$PATH:/home/msoares/software/bwa/bwa.kit
bwa index P_marinus.fa
files="<add list of files>"
for sample in $files
do
        bwa mem -t 20 P_marinus.fa ${sample}.1.fastq ${sample}.2.fastq |
         samtools view -F 0x04 -b |
         samtools sort --threads 20 > mapped/${sample}.bam
done

###use gstacks
mkdir gstacks_output
/home/msoares/stacks-2.2/gstacks -I ./ -M popmap_PE.txt --rm-pcr-duplicates -O gstacks_output/ -t 10

###use populations 
mkdir gstacks_mapped/populations
/home/msoares/stacks-2.2/populations -P gstacks_mapped/ 
  -M popmap_PE.txt -O gstacks_mapped/populations/ 
  --max_obs_het 0.5 -r 0.80 --write_single_snp --min_maf 0.01 --vcf --fstats --bootstrap --verbose -t 10

