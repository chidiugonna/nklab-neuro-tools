Bootstrap: docker
From: ubuntu:xenial

%help
Please refer to https://github.com/chidiugonna/nklab-neuro-tools for documentation about this singularity container.

%setup
cp ./src/resting_pipeline.py $SINGULARITY_ROOTFS
cp ./src/resting_pipeline_orig.py $SINGULARITY_ROOTFS
cp ./src/fsl_sub $SINGULARITY_ROOTFS
cp ./src/statusfeat.py $SINGULARITY_ROOTFS
cp ./src/runfeat-1.py $SINGULARITY_ROOTFS
cp ./src/make_fsl_stc.py $SINGULARITY_ROOTFS
cp ./src/changePython2.sh $SINGULARITY_ROOTFS
cp ./src/changePython3.sh $SINGULARITY_ROOTFS
cp ./src/license.txt $SINGULARITY_ROOTFS

%environment
LD_LIBRARY_PATH=/usr/local/cuda/lib64:/.singularity.d/libs:/usr/lib:/opt/freesurfer/mni/lib:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH
export FSLDIR=/opt/fsl
export PATH=$FSLDIR/bin:$PATH
export PATH=$FSLDIR/bin/FSLeyes:$PATH
export BXHVER=bxh_xcede_tools-1.11.1-lsb30.x86_64
export BXHBIN=/opt/$BXHVER
export RSFMRI=/opt/rsfmri_python
export PATH=$BXHBIN/bin:$PATH
export PATH=$BXHBIN/lib:$PATH
export PATH=$RSFMRI/bin:$PATH
export PATH=/opt/bin:$PATH
export PATH=/opt/abin:$PATH
export PATH=/opt/mrtrix3/bin:$PATH
export FREESURFER_HOME=/opt/freesurfer
export FUNCTIONALS_DIR=/opt/freesurfer/sessions
export FSFAST_HOME=/opt/freesurfer/fsfast
export SUBJECTS_DIR=/opt/freesurfer/subjects
export MINC_BIN_DIR=/opt/freesurfer/mni/bin
export MINC_LIB_DIR=/opt/freesurfer/mni/lib
export FSL_DIR=/opt/fsl
export MNI_DIR=/opt/freesurfer/mni
export MNI_DATAPATH=/opt/freesurfer/mni/data
export FSF_OUTPUT_TYPE=nii.gz
export SUBJECTS_DIR=/opt/data/freesurfer-outputs
export PATH=$FREESURFER_HOME/bin:$PATH
export PATH=$FREESURFER_HOME/tktooks:$PATH
export PATH=$FREESURFER_HOME/fsfast/bin:$PATH
export PATH=$FREESURFER_HOME/mni/bin:$PATH
export PATH=$MNI_DIR/bin:$PATH
export ANTSPATH=/opt/ANTScode/bin/bin
export PATH=$ANTSPATH:$PATH
export ITK_GLOBAL_DEFAULT_NUMBER_OF_THREADS=4 
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH=/.singularity.d/libs:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH=/usr/lib:$LD_LIBRARY_PATH
export PATH=/usr/local/cuda/bin:$PATH
%files

%runscript
. $FSLDIR/etc/fslconf/fsl.sh
cd /opt/data
exec "$@"


%test

%post
mkdir /uaopt /extra /xdisk /opt/data /opt/bin
export BXHVER=bxh_xcede_tools-1.11.1-lsb30.x86_64
export BXHLOC=7384
export BXHBIN=/opt/$BXHVER
export RSFMRI=/opt/rsfmri_python
apt-get update && apt-get install -y \
	nano \
	wget \
	curl \
        dc \
	lsb-core \
	python-pip \
        libx11-6 \
        libgl1 \
        libgtk-3-0 \
        libgtk-3-dev \
        libsm6 \
        libxext6 \
        libxt6 \
        mesa-common-dev \
        freeglut3-dev \
        zlib1g-dev \
        libpng-dev \
        expat \
        unzip \
        libeigen3-dev \
        zlib1g-dev \
        libqt4-opengl-dev \
        libgl1-mesa-dev \
        libfftw3-dev \
        libtiff5-dev \
        graphviz \
        libgraphviz-dev \
        software-properties-common
add-apt-repository universe
apt-get update && apt-get install -y \
        tcsh \
        xfonts-base \
        python-qt4 \
        gsl-bin \
        gnome-tweak-tool \
        libjpeg62 \
        xvfb \
        xterm \
        vim \
        libglu1-mesa-dev \
        libglw1-mesa   \
        libxm4 \
        netpbm
apt-get update && apt-get install -y \
        hdf5-tools \
        openmpi-bin \
        openmpi-doc \
        libopenmpi-dev \
        gfortran \
        python-matplotlib \
        git \
        x11-xserver-utils \
        firefox \
        midori \
        python3-pip \
        
pip install --upgrade pip
pip install numpy
pip install scipy
pip install nibabel
pip install networkx==1.11
pip install nipype
pip install rdflib
pip install nipy
pip install dipy
pip install jupyter

pip3 install --upgrade pip
pip3 install xgboost
pip3 install numpy
pip3 install scipy
pip3 install nibabel
pip3 install networkx
pip3 install nipype
pip3 install rdflib
pip3 install nipy
pip3 install dipy
pip3 install nitime
pip3 install nilearn
pip3 install MNE
pip3 install nilearn
pip3 install jupyter

cd /tmp
echo "LC_ALL=en_US.UTF-8" >> /etc/environment
echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen
echo "LANG=en_US.UTF-8" > /etc/locale.conf
locale-gen en_US.UTF-8

cd /tmp
wget "https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_375.26_linux-run"
mkdir -p nvidia_installers
chmod +x cuda_8.0.61_375.26_linux-run
./cuda_8.0.61_375.26_linux-run -extract=`pwd`/nvidia_installers
rm cuda_8.0.61_375.26_linux-run
cd nvidia_installers
rm cuda-samples*
rm NVIDIA-Linux*
./cuda-linux64-rel-8.0.61-21551265.run -noprompt
cd ..
rm -R nvidia_installers
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH=/.singularity.d/libs:$LD_LIBRARY_PATH
export PATH=/usr/local/cuda/bin:$PATH

cd /tmp
wget https://cmake.org/files/v3.10/cmake-3.10.0-rc1.tar.gz
tar xz -f cmake-3.10.0-rc1.tar.gz
rm cmake-3.10.0-rc1.tar.gz
cd cmake-3.10.0-rc1
./configure
make
make install
./bootstrap --prefix=/usr
make
make install

cd /tmp
wget http://www.vtk.org/files/release/7.1/VTK-7.1.1.tar.gz
tar xz -f VTK-7.1.1.tar.gz
rm VTK-7.1.1.tar.gz
cd VTK-7.1.1
cmake .
make
make install

chmod 777 /opt
cd /opt
git clone https://github.com/MRtrix3/mrtrix3.git
cd /opt/mrtrix3
./configure
./build

export FREESURFER_HOME=/opt/freesurfer
cd /opt
wget ftp://surfer.nmr.mgh.harvard.edu/pub/dist/freesurfer/6.0.0/freesurfer-Linux-centos6_x86_64-stable-pub-v6.0.0.tar.gz
tar xz -f freesurfer-Linux-centos6_x86_64-stable-pub-v6.0.0.tar.gz
cd /usr/lib/x86_64-linux-gnu
ln -s libtiff.so.4 libtiff.so.3
rm freesurfer-Linux-centos6_x86_64-stable-pub-v6.0.0.tar.gz

export ANTSPATH=/opt/ANTScode/bin/bin
mkdir /opt/ANTScode 
cd /opt/ANTScode
git clone https://github.com/stnava/ANTs.git
mkdir /opt/ANTScode/bin
cd /opt/ANTScode/bin
cmake /opt/ANTScode/ANTs
make -j 4
ln -sf /usr/lib/ants/N4BiasFieldCorrection /usr/local/bin/

cd /opt
wget https://julialang-s3.julialang.org/bin/linux/x64/0.6/julia-0.6.1-linux-x86_64.tar.gz
tar xz -f julia-0.6.1-linux-x86_64.tar.gz
rm julia-0.6.1-linux-x86_64.tar.gz
mv julia-* julia
ln -s /opt/julia/bin/julia /usr/local/bin/julia
chmod -R 777 /opt/julia

export HOMEBACK=$HOME
export HOME=/opt
cd /opt
wget https://afni.nimh.nih.gov/pub/dist/bin/linux_ubuntu_16_64/@update.afni.binaries
/bin/tcsh @update.afni.binaries -package linux_ubuntu_16_64  -do_extras
export HOME=$HOMEBACK

cd /opt
export FSLDIR=/opt/fsl
export PATH=${FSLDIR}/bin:${PATH}
wget https://www.dropbox.com/s/fappgvj52xpfyzj/fsl-5.0.10-sources.tar.gz
tar xz -f fsl-5.0.10-sources.tar.gz
rm fsl-5.0.10-sources.tar.g
chmod -R 777 fsl
sed -i 's/#FSLCONFDIR/FSLCONFDIR/g' ${FSLDIR}/etc/fslconf/fsl.sh
sed -i 's/#FSLMACHTYPE/FSLMACHTYPE/g' ${FSLDIR}/etc/fslconf/fsl.sh
sed -i 's/#export FSLCONFDIR/export FSLCONFDIR /g' ${FSLDIR}/etc/fslconf/fsl.sh
. ${FSLDIR}/etc/fslconf/fsl.sh
cp -r ${FSLDIR}/config/linux_64-gcc4.8 ${FSLDIR}/config/${FSLMACHTYPE}
sed -i "s#scl enable devtoolset-2 -- c++#c++#g" $FSLDIR/config/$FSLMACHTYPE/systemvars.mk
sed -i "s#CUDA_INSTALLATION = /opt/cuda-7.5#CUDA_INSTALLATION = /usr/local/cuda-7.5#g" $FSLDIR/config/$FSLMACHTYPE/systemvars.mk
sed -i "s#VTKDIR_INC = /home/fs0/cowboy/var/caper_linux_64-gcc4.4/VTK7/include/vtk-7.0#VTKDIR_INC = /usr/local/include/vtk-7.1/#g" $FSLDIR/config/$FSLMACHTYPE/externallibs.mk
sed -i "s#VTKDIR_LIB = /home/fs0/cowboy/var/caper_linux_64-gcc4.4/VTK7/lib#VTKDIR_LIB = /usr/local/lib/#g" $FSLDIR/config/$FSLMACHTYPE/externallibs.mk
sed -i "s#VTKSUFFIX = -7.0#VTKSUFFIX = -7.1#g" $FSLDIR/config/$FSLMACHTYPE/externallibs.mk
sed -i "s#{LIBRT}#{LIBRT} -ldl#g" $FSLDIR/src/mist-clean/Makefile
sed -i "s#lpng -lz#lpng -lz -lm#g" $FSLDIR/src/miscvis/Makefile
cd ${FSLDIR}
./build
sed -i "s#dropprivileges=1#dropprivileges=0#g" ${FSLDIR}/etc/fslconf/fslpython_install.sh
${FSLDIR}/etc/fslconf/fslpython_install.sh
cd  ${FSLDIR}/bin
wget https://fsl.fmrib.ox.ac.uk/fsldownloads/patches/eddy-patch-fsl-5.0.11/centos6/eddy_cuda8.0
chmod +x eddy_cuda8.0
wget https://fsl.fmrib.ox.ac.uk/fsldownloads/patches/eddy-patch-fsl-5.0.11/centos6/eddy_openmp
chmod +x eddy_openmp
wget https://fsl.fmrib.ox.ac.uk/fsldownloads/fsleyes/FSLeyes-latest-ubuntu1604.zip
unzip FSLeyes-latest-ubuntu1604.zip
rm FSLeyes-latest-ubuntu1604.zip

mv /changePython2.sh /opt/bin/changePython2.sh
mv /changePython3.sh /opt/bin/changePython3.sh
cd /opt
. /opt/bin/changePython3.sh
pip3 install -r https://raw.githubusercontent.com/poldracklab/mriqc/master/requirements.txt
pip3 install git+https://github.com/poldracklab/mriqc.git
. /opt/bin/changePython2.sh


cd /tmp
wget "http://www.nitrc.org/frs/download.php/$BXHLOC/$BXHVER.tgz"
wget "https://wiki.biac.duke.edu/_media/biac:analysis:rsfmri_python.tgz"
tar -xzf $BXHVER.tgz -C /opt
mv biac:analysis:rsfmri_python.tgz rsfmri_python.tgz
tar -xzf rsfmri_python.tgz  -C /opt
rm rsfmri_python.tgz
rm $BXHVER.tgz

chmod -R 777 /opt 

mv /resting_pipeline.py $RSFMRI/bin
mv /resting_pipeline_orig.py $RSFMRI/bin
mv /fsl_sub $FSLDIR/bin
mv /statusfeat.py $RSFMRI/bin
mv /runfeat-1.py $RSFMRI/bin
mv /make_fsl_stc.py $RSFMRI/bin
mv /license.txt $FREESURFER_HOME

echo ". $FSLDIR/etc/fslconf/fsl.sh" >> $SINGULARITY_ENVIRONMENT

