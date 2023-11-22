# sequence_assembly
## Genome Assembly

During sequencing, the DNA was broken into smaller fragments.  Assembly is the process of turning these 'reads' (shorter individual measurements) back into 'contigs' (longer contiguous sequences). To establish the DNA composition of the organism, a **genome assembly** is performed. If building the transcript (RNA) expression for the organism, that is a **transcriptome assembly**.
&nbsp;

Sequence data for the bacteria Staphylococcus aureus known for its potential to cause various skin and soft tissue infections.
&nbsp;

![Screenshot_2023-11-22_annot](https://github.com/programweb/sequence_assembly/assets/12736699/720151a0-0901-4400-98de-51c17ee1139f)
&nbsp;

![Screenshot_2023-11-22_annot2](https://github.com/programweb/sequence_assembly/assets/12736699/acc43a04-3683-4b5d-ad09-bdfa230df8f0)
&nbsp;

Install FastQC (dmg on Mac OS) to run a report (or generate an HTML report)
&nbsp;

Left is SRR022868; the right plot is for run SRR022865
&nbsp;

<img width="776" alt="Screenshot 2023-11-22 at 7 07 11 AM" src="https://github.com/programweb/sequence_assembly/assets/12736699/33b8e473-6242-49ad-b6a6-71831645496d">
&nbsp;

&nbsp;

&nbsp;

## Ebola Example
&nbsp;

Demonstration.
Picking a run from the Ebola virus with run ID:  [SRR1553425](https://www.ncbi.nlm.nih.gov/sra/?term=SRR1553425 "Run ID: SRR1553425")


Take a subset of 100,000 reads (of the 3.6 million total reads)
This will result in files with extension: .fastq. The FASTQ format is a text-based format for storing both a biological sequence and its corresponding quality scores. Both the sequence letter and quality score are each encoded with a single ASCII character for brevity.
```bash
fastq-dump SRR1553425 -X 100000 --split-files
```

Focus on the first pairs (filename suffix "_1") and assign it to a system variable "READS"
```bash
READS=SRR1553425_1.fastq
```

Here using the [Minia assembler](https://github.com/GATB/minia "The Minia assembler") 
to demonstrate the typical usage patterns during an assembly process. 
Minia is a short-read assembler based on a de Bruijn graph.
This command utilizes the READS system variable that I made in the last step.
This outputs a file called genome.contigs.fa
```bash
minia -in $READS -out genome
```

Run quick statistics on the genome.contigs.fa file using
[SeqKit](https://bioinf.shenwei.me/seqkit/ "SeqKit Program")
which is an ultrafast toolkit for FASTA/Q file analysis and manipulation.
```bash
seqkit stat genome.contigs.fa
file               format  type  num_seqs  sum_len  min_len  avg_len  max_len
genome.contigs.fa  FASTA   DNA     190     16,812      63     88.5      277
```

* 190 contigs
* the average length is 88.5bp
* the longest is 277bp

&nbsp;

--- --- --- _I COULD ADD MORE TO THIS CODE SAMPLE IN THE FUTURE._ --- --- ---
&nbsp;
