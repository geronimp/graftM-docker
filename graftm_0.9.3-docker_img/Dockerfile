###################################################################
# Dockerfile
#
# Version:          1
# Software:         graftM
# Software Version: 0.9.3
# Website:          https://github.com/geronimp/graftM
# Provides:         graftM 0.9.3
# Base Image:       ubuntu:14.04
# Build Cmd:        sudo docker build -t graftm_0.9.3-docker_img .
# Pull Cmd:         docker pull geronimp/graftM
# Run Cmd:          run -v `pwd`:/data graftm_0.9.3-docker_img graft --forward 16s.fna --graftm_package 4.01.2013_08_greengenes_61_otus.gpkg
###################################################################

# Base image as Unbuntu
FROM ubuntu:14.04

###################### BEGIN INSTALLATION #########################

######################### Set up environment ######################
RUN sudo apt-get update
RUN sudo apt-get --assume-yes install software-properties-common
RUN sudo apt-get --assume-yes install wget
RUN sudo apt-get --assume-yes install tar
RUN sudo apt-get --assume-yes install git
RUN sudo apt-get --assume-yes install libc6-dev gcc-4.8-base  
RUN sudo apt-get install -f
RUN sudo add-apt-repository ppa:fkrull/deadsnakes
RUN sudo apt-get --assume-yes install python
RUN sudo apt-get --assume-yes install python-dev
RUN sudo apt-get --assume-yes install python-distribute
RUN sudo apt-get --assume-yes install python-pip
RUN sudo apt-get --assume-yes install pkg-config
RUN sudo apt-get --assume-yes install libfreetype6-dev
RUN sudo apt-get --assume-yes install libpng-dev
RUN sudo apt-get --assume-yes install camlp4-extra
RUN sudo apt-get --assume-yes install gawk 
RUN sudo apt-get --assume-yes install libgsl0-dev
RUN sudo apt-get --assume-yes install libsqlite3-dev
RUN sudo apt-get --assume-yes install libz-dev
RUN sudo apt-get --assume-yes install m4
RUN sudo apt-get --assume-yes install make
RUN sudo apt-get --assume-yes install ocaml
RUN sudo apt-get --assume-yes install patch
RUN sudo apt-get --assume-yes install python-scipy
RUN sudo apt-get --assume-yes install python-numpy
RUN sudo apt-get --assume-yes install python3-scipy
RUN sudo apt-get --assume-yes install liblapack-dev
RUN sudo apt-get --assume-yes install gfortran

################ Intstall non-pythonic dependencies ###############
#- OrfM -#
RUN wget https://github.com/wwood/OrfM/releases/download/v0.5.2/orfm-0.5.2.tar.gz
RUN tar xzf orfm-0.5.2.tar.gz
WORKDIR orfm-0.5.2
RUN ./configure
RUN make
RUN sudo make install
RUN orfm -h
WORKDIR ../

#- FastTree -#
RUN sudo apt-get --assume-yes install fasttree
RUN mv /usr/bin/fasttree /usr/bin/FastTree
RUN mv /usr/bin/fasttreeMP /usr/bin/FastTreeMP

RUN FastTreeMP -help
RUN FastTree -help

#- krona -#
RUN wget https://github.com/marbl/Krona/releases/download/v2.6/KronaTools-2.6.tar
RUN tar xopf KronaTools-2.6.tar
WORKDIR KronaTools-2.6 
RUN sudo apt-get --assume-yes install perl
RUN perl install.pl
RUN ktImportText -h

#- mafft -#
RUN sudo apt-get --assume-yes install mafft
# No -h option?

#- HMMER -#
RUN sudo apt-get --assume-yes install hmmer
RUN hmmsearch -h

#- DIAMOND -#
RUN wget http://github.com/bbuchfink/diamond/releases/download/v0.7.10/diamond-linux64.tar.gz
RUN tar xzf diamond-linux64.tar.gz
RUN mv ./diamond /usr/bin
RUN diamond -h

#- pplacer -#
RUN sudo apt-get --assume-yes install unzip
RUN wget https://github.com/matsen/pplacer/releases/download/v1.1.alpha17/pplacer-Linux-v1.1.alpha17.zip
RUN unzip pplacer-Linux-v1.1.alpha17.zip 
RUN mv pplacer-Linux-v1.1.alpha17/rppr pplacer-Linux-v1.1.alpha17/pplacer pplacer-Linux-v1.1.alpha17/guppy /usr/bin/
RUN pplacer --help
# RUN rppr -help  ----- prints help message but sends non-0 exit status.

#- fxtract -#
RUN git clone --recursive https://github.com/ctSkennerton/fxtract.git
WORKDIR fxtract
RUN make NO_PCRE=1	
RUN mv fxtract /usr/bin/
WORKDIR ../

RUN pip install tempdir
RUN pip install graftm==0.9.3
RUN sudo apt-get --assume-yes install cython
RUN sudo apt-get --assume-yes install libhdf5-dev
RUN pip install h5py

RUN mkdir /gpkg
RUN mkdir /hmm
RUN mkdir /reads

WORKDIR /data
ENTRYPOINT ["graftM"]


##################### INSTALLATION END #####################

