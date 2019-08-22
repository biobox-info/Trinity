From: ubuntu:bionic
Bootstrap: docker

%help
trinity 2.6.6

%labels
MAINTAINER BioBox
Version v1.0

%environment
%environment
  PATH=/usr/local/src/trinityrnaseq-Trinity-v2.6.6:$PATH
  PATH=/usr/local/src/trinityrnaseq-Trinity-v2.6.6/util:$PATH
  PATH=/usr/local/src/trinityrnaseq-Trinity-v2.6.6/Analysis/DifferentialExpression:$PATH
  PATH=/usr/local/src/trinityrnaseq-Trinity-v2.6.6/Analysis/FL_reconstruction_analysis:$PATH
  PATH=/usr/local/src/trinityrnaseq-Trinity-v2.6.6/Analysis/GenomeViewPlugin:$PATH
  PATH=/usr/local/src/trinityrnaseq-Trinity-v2.6.6/Analysis/SuperTranscripts:$PATH
  PATH=/usr/local/src/bowtie2-2.3.4.1-linux-x86_64:$PATH
  PATH=/usr/local/src/RSEM-1.3.0:$PATH
  export LC_ALL=C

%runscript
echo "This gets run when you run the image!" 
exec /bin/bash /code/rawr.sh "$@"  

%post  
  apt-get update && apt-get dist-upgrade -y && apt-get install wget zlib1g-dev build-essential samtools python zlib1g-dev unzip r-base r-base-core r-base-dev -y && rm -rf /var/lib/apt/lists/*
  mkdir -p /usr/local/src
  cd /usr/local/src && wget https://github.com/trinityrnaseq/trinityrnaseq/archive/Trinity-v2.6.6.tar.gz -O trinity.tar.gz && tar xf trinity.tar.gz && rm trinity.tar.gz && cd trinityrnaseq-Trinity-v2.6.6 && make -j 8
  cd /usr/local/src && wget https://datapacket.dl.sourceforge.net/project/bowtie-bio/bowtie2/2.3.4.1/bowtie2-2.3.4.1-linux-x86_64.zip -O bowtie2.zip && unzip bowtie2.zip && rm bowtie2.zip
  cd /usr/local/src && wget https://github.com/deweylab/RSEM/archive/v1.3.0.tar.gz -O rsem.tar.gz && tar xf rsem.tar.gz && rm rsem.tar.gz && cd RSEM-1.3.0 && make -j 8
  Rscript -e "source(\"http://bioconductor.org/biocLite.R\"); biocLite('edgeR'); biocLite('limma'); biocLite('DESeq2') ;  biocLite('ctc') ; biocLite('Biobase') ; install.packages('gplots'); install.packages('ape')"
  mkdir /scratch
