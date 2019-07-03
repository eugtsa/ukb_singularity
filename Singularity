Bootstrap: library
From: debian:9

%help

    Container with Anaconda 3 (Conda 2019.3) and full ukb environment for Debian 9.x (Stretch).
    This installation is based on Python 3.7

%files
  ./requirements.txt /requirements.txt

%post

  #Installing all dependencies

  touch /.condarc
  apt-get update && apt-get -y upgrade
  apt-get -y install \
    build-essential \
    wget \
    bzip2 \
    ca-certificates \
    libglib2.0-0 \
    libxext6 \
    libsm6 \
    libxrender1 \
    git

  rm -rf /var/lib/apt/lists/*
  apt-get clean

  wget -c https://repo.anaconda.com/archive/Anaconda3-2019.03-Linux-x86_64.sh
    /bin/bash Anaconda3-2019.03-Linux-x86_64.sh -bfp /usr/local

  #Conda configuration of channels from .condarc file

  conda config --file /.condarc --add channels defaults
  conda config --file /.condarc --add channels conda-forge
  conda config --file /.condarc --add channels pytorch
  conda config --file /.condarc --add channels bioconda
  conda update conda

  #Install environment
   conda install --file requirements.txt
