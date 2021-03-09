Bootstrap: docker
From: nvidia/cuda:10.0-devel

%setup
mkdir ${SINGULARITY_ROOTFS}/workspace

%files
%labels
    Pytorch environment
    Build with:
    sudo singularity build --writable dtorch.img dtorch.txt
    singularity exec --nv dtorch.img python


%post
mkdir /project /scratch

#Now install everythin
apt-get update && apt-get -y install wget

DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        python3 \
        python3-tk \
        python3-pip \
        python3-dev
rm -rf /var/lib/apt/lists/*
pip3 install pipenv
wget -c https://repo.continuum.io/miniconda/Miniconda3-4.5.12-Linux-x86_64.sh
bash Miniconda3-4.5.12-Linux-x86_64.sh -p /miniconda -b
rm Miniconda3-4.5.12-Linux-x86_64.sh
PATH=/miniconda/bin:${PATH}

conda update -y conda
conda install pytorch==1.0.0 torchvision==0.2.1 cuda100 -c pytorch
cd /workspace

%environment
export PATH=/miniconda/bin:${PATH}


%runscript
