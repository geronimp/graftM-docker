###################################################################
# Dockerfile
#
# Version:          1
# Software:         graftM
# Software Version: 0.9.4
# Website:          https://github.com/geronimp/graftM
# Provides:         graftM 0.9.4
# Base Image:       ubuntu:14.04
# Build Cmd:        sudo docker build -t graftm_0.9.4-docker_img .
# Pull Cmd:         docker pull geronimp/graftM
# Run Cmd:          run -v `pwd`:/data graftm_0.9.4-docker_img graft --forward 16s.fna --graftm_package 4.01.2013_08_greengenes_61_otus.gpkg
###################################################################
# Base image as Unbuntu
FROM ubuntu:14.04
# Copy in resources 
COPY resources $PWD
# Set up environment
ENV USER=root
######################### Set up environment ######################
RUN sudo apt-get update && \
    sudo apt-get -y install software-properties-common wget tar git libc6-dev gcc-4.8-base && \
    sudo add-apt-repository ppa:fkrull/deadsnakes && \
    sudo apt-get -y install python python-dev python-distribute python-pip pkg-config libfreetype6-dev libpng-dev camlp4-extra gawk \
			    libgsl0-dev libsqlite3-dev libz-dev m4 make ocaml patch python-scipy python-numpy python3-scipy liblapack-dev \
			    gfortran unzip cython libhdf5-dev fasttree mafft
RUN pip install tempdir
RUN pip install h5py
RUN wget https://github.com/wwood/OrfM/releases/download/v0.5.2/orfm-0.5.2.tar.gz \
	 https://github.com/marbl/Krona/releases/download/v2.6/KronaTools-2.6.tar \
	 http://github.com/bbuchfink/diamond/releases/download/v0.7.10/diamond-linux64.tar.gz \
	 https://github.com/matsen/pplacer/releases/download/v1.1.alpha17/pplacer-Linux-v1.1.alpha17.zip \
	 https://github.com/ctSkennerton/fxtract/releases/download/1.2/fxtract1.2-Linux-64bit \
   http://selab.janelia.org/software/hmmer3/3.1b2/hmmer-3.1b2-linux-intel-x86_64.tar.gz
RUN tar xzf orfm-0.5.2.tar.gz && tar xopf KronaTools-2.6.tar && tar xzf diamond-linux64.tar.gz && unzip pplacer-Linux-v1.1.alpha17.zip && tar xzf hmmer-3.1b2-linux-intel-x86_64.tar.gz
RUN mv diamond pplacer-Linux-v1.1.alpha17/rppr pplacer-Linux-v1.1.alpha17/pplacer pplacer-Linux-v1.1.alpha17/guppy /usr/local/bin/ && \
	chmod +x fxtract1.2-Linux-64bit && mv fxtract1.2-Linux-64bit /usr/local/bin/fxtract	
WORKDIR hmmer-3.1b2-linux-intel-x86_64/ 
RUN ./configure && make && cp binaries/* /usr/local/bin/
WORKDIR ../orfm-0.5.2 
RUN ./configure && make && sudo make install
WORKDIR ../KronaTools-2.6 
RUN sudo apt-get --assume-yes install perl && perl install.pl
RUN pip install /graftm-0.9.4.tar.gz 
RUN sudo add-apt-repository ppa:ubuntu-toolchain-r/test && sudo apt-get update && sudo apt-get install -y g++-4.8
WORKDIR /data
ENTRYPOINT ["graftM"]
