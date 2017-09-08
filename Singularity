Bootstrap: docker
From: nvidia/cuda:8.0-cudnn7-devel-ubuntu14.04
# for list of available Docker images see https://hub.docker.com/r/nvidia/cuda/

%environment

  #Use bash as default shell
  SHELL=/bin/bash
  
  #Add nvidia driver paths
  
  PATH="/nvbin:$PATH"
  LD_LIBRARY_PATH="/nvlib:$LD_LIBRARY_PATH"
  
  #Add CUDA paths
  
  CPATH="/usr/local/cuda/include:$CPATH"
  PATH="/usr/local/cuda/bin:$PATH"
  LD_LIBRARY_PATH="/usr/local/cuda/lib64:$LD_LIBRARY_PATH"
  CUDA_HOME="/usr/local/cuda"
  
  export PATH LD_LIBRARY_PATH CPATH CUDA_HOME

%setup
  #Runs on host
  #The path to the image is $SINGULARITY_ROOTFS

%post
  #Post setup script
  
  #Default mount paths
  mkdir /scratch /uufs
  
  #Nvidia Library mount paths
  mkdir /nvlib /nvbin

  #Updating and getting required packages
  apt-get update
  apt-get install -y wget git vim

  # CUDA samples for testing
  #echo CUDA_PKG_VERSION $CUDA_PKG_VERSION
  # CUDA_PKG_VERSION is not defined in %post, or in %test, so, need to run tests outside
  #apt-get install -y cuda-samples-$CUDA_PKG_VERSION

%files
  test.sh /opt/test.sh

%test
  # build the deviceQuery sample and run it - it should show available GPU(s)
  # since CUDA_PKG_VERSION is not defined in %test, need to run this test outside
  #cd /usr/local/cuda/samples/1_Utilities/deviceQuery
  #make; make run
