FROM rocker/r-ver:4.4.1

RUN apt-get update && apt-get install --no-install-recommends -y \
    build-essential \
    libcurl4-gnutls-dev \
    libxml2-dev \
    libssl-dev \
    libxml2 \
    libxt6 \
    zlib1g-dev \
    libbz2-dev \
    liblzma-dev \
    libpcre3-dev \
    libicu-dev \
    libjpeg-dev \
    libpng-dev \
    libxml2-dev \
    libglpk-dev

RUN R -e "install.packages('remotes');" \
&& R -e "install.packages('BiocManager');" \
&& R -e "BiocManager::install('VariantAnnotation'); if (!library(VariantAnnotation, logical.return=T)) quit(status=10)" \
&& R -e "BiocManager::install('rtracklayer'); if (!library(rtracklayer, logical.return=T)) quit(status=10)" \
&& R -e "BiocManager::install('tximport') ; if (!library(tximport, logical.return=T)) quit(status=10)" \
&& R -e "BiocManager::install('GenomicRanges') ; if (!library(GenomicRanges, logical.return=T)) quit(status=10)" \
&& R -e "install.packages('data.table'); if (!library(data.table, logical.return=T)) quit(status=10)" \
&& R -e "remotes::install_github(repo = 'damhof/RiboseQC'); if (!library(RiboseQC, logical.return=T)) quit(status=10)" \
&& R -e "remotes::install_version('tidyverse', repos = c('http://cran.us.r-project.org')); if (!library(tidyverse, logical.return=T)) quit(status=10)"
