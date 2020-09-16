Bootstrap: docker
From: neurodebian:latest

%help

    Container with Anaconda 3 (Conda 2019.3) and full ukb environment from neurodebian.
    This installation is based on Python 3.7

%files
  ./requirements.txt /requirements.txt
  ./tools/flashpca /flashpca

%post

  #Installing all dependencies
  mv /flashpca /usr/bin/flashpca
  mkdir /gpfs
  chmod 755 /usr/bin/flashpca
  
  apt-get update
  DEBIAN_FRONTEND=noninteractive apt-get -yq install \
    build-essential \
    wget \
    unzip \
    git

  rm -rf /var/lib/apt/lists/*
  
  apt-get clean

  wget -c http://s3.amazonaws.com/plink2-assets/alpha2/plink2_linux_avx2.zip
  mkdir /plink
  mv plink2_linux_avx2.zip /plink/plink2_linux_avx2.zip
  cd plink && unzip plink2_linux_avx2.zip && mv plink2 /usr/bin/plink2 && cd /
  chmod 755 /usr/bin/plink2
  
  wget -c https://repo.anaconda.com/archive/Anaconda3-2019.03-Linux-x86_64.sh
    /bin/bash Anaconda3-2019.03-Linux-x86_64.sh -bfp /usr/local

  #Conda configuration of channels from .condarc file

  conda config --add channels defaults
  conda config --add channels conda-forge
  conda config --add channels pytorch
  conda config --add channels bioconda
  conda update conda

  #Install environment
   conda install --file requirements.txt
   git clone https://github.com/chrchang/plink-ng.git
   cd plink-ng/2.0/Python && git checkout 6fdbefc0b612fbaefdd78b82140af894fdf742c9 && python setup.py build_ext && pwd && pip install -e .
