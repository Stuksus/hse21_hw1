# hse21_hw1
## Команды
$ ln -s /usr/share/data-minor-bioinf/assembly/oil_R1.fastq 

$ ln -s /usr/share/data-minor-bioinf/assembly/oil_R2.fastq

$ ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R2_001.fastq

$ ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R1_001.fastq

$ seqtk sample -s42 oilMP_S4_L001_R1_001.fastq 1500000 > sub11.fq   

$ seqtk sample -s42 oilMP_S4_L001_R2_001.fastq 1500000 > sub22.fq

$ seqtk sample -s42 oil_R1.fastq 5000000 > sub11_pre.fq

$ seqtk sample -s42 oil_R2.fastq 5000000 > sub22_pre.fq

$ mkdir fastqc

$ ls sub* | xargs -P 4 -tI{} fastqc -o fastqc {}

$ mkdir multifastqc   

$ multiqc -o multiqc fastqc

scp -P 5222 -i mykey aasmetanin@92.242.58.92:/home/aasmetanin/fastqc/sub11_fastqc.html /Users/anton/Desktop/JupyterProjects/Bioinformatics

scp -P 5222 -i mykey aasmetanin@92.242.58.92:/home/aasmetanin/fastqc/sub11_pre_fastqc.html /Users/anton/Desktop/JupyterProjects/Bioinformatics

scp -P 5222 -i mykey aasmetanin@92.242.58.92:/home/aasmetanin/fastqc/sub22_fastqc.html /Users/anton/Desktop/JupyterProjects/Bioinformatics

scp -P 5222 -i mykey aasmetanin@92.242.58.92:/home/aasmetanin/fastqc/sub22_pre_fastqc.html /Users/anton/Desktop/JupyterProjects/Bioinformatics

platanus_internal_trim sub11.fq  sub22.fq


platanus_trim  sub11_pre.fq sub22_pre.fq


$ rm oilMP_S4_L001_R1_001.fastq

$ rm oilMP_S4_L001_R2_001.fastq

$ rm oil_R2.fastq

$ rm oil_R1.fastq



mkdir fastqc2

ls *.fq.* | xargs -P 4 -tI{} fastqc -o fastqc2 {}

multiqc -o multiqc fastqc2


scp -P 5222 -i mykey aasmetanin@92.242.58.92:/home/aasmetanin/fastqc2/sub11.fq.int_trimmed_fastqc.html /Users/anton/Desktop/JupyterProjects/Bioinformatics

scp -P 5222 -i mykey aasmetanin@92.242.58.92:/home/aasmetanin/fastqc2/sub11_pre.fq.trimmed_fastqc.html /Users/anton/Desktop/JupyterProjects/Bioinformatics

scp -P 5222 -i mykey aasmetanin@92.242.58.92:/home/aasmetanin/fastqc2/sub22.fq.int_trimmed_fastqc.html /Users/anton/Desktop/JupyterProjects/Bioinformatics

scp -P 5222 -i mykey aasmetanin@92.242.58.92:/home/aasmetanin/fastqc2/sub22_pre.fq.trimmed_fastqc.html /Users/anton/Desktop/JupyterProjects/Bioinformatics


mkdir trimmed_fq

mv -v *.fq.* *trimmed trimmed_fq/


time platanus assemble -o Poil -t 1 -f trimmed_fq/sub11_pre.fq.trimmed trimmed_fq/sub22_pre.fq.trimmed

time platanus scaffold -o Poil -t 1 -c Poil_contig.fa -IP1 trimmed_fq/sub11_pre.fq.trimmed trimmed_fq/sub22_pre.fq.trimmed -OP2 trimmed_fq/sub11.fq.int_trimmed trimmed_fq/sub22.fq.int_trimmed 2> scaffold.log

time platanus gap_close -o Poil -t 1 -c Poil_scaffold.fa -IP1 trimmed_fq/sub11_pre.fq.trimmed trimmed_fq/sub22_pre.fq.trimmed -OP2 trimmed_fq/sub11.fq.int_trimmed trimmed_fq/sub22.fq.int_trimmed 2>gapclose.log

Скриншоты из отчета:
