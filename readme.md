## Base Ubuntu Singularity 2.3 container with Nvidia GPU support

We bootstrap the container with the Nvidia Docker image, a list of available Docker images are at [https://hub.docker.com/r/nvidia/cuda/](https://hub.docker.com/r/nvidia/cuda/).

This necessitates to set environment variables in the `%environment` section to point to the `/usr/local/cuda` directory.

We are using the Singularity 2.3+ `--nv` flag to bring in the Nvidia driver stack from the host. This only works for the execution commands (`exec`, `shell`, etc.), not for bootstrap, but, installations inside bootstrap dont necessarily need the GPU access. `%post` testing is a different story - as the GPU driver stack is not in during the `%post`, instead of running tests in `%post` during bootstrap, we do it after bootstrap with `singularity exec`. See the `build_container23.sh` script for details.

Thanks to the `--nv` command this container should be independent from the host GPU driver version.

To build the container, do the following:
```
ml singularity
./build_container23.sh
```
(note that you will need sudo access to singularity, which all hpcapps users should have, or build on your own machine with root).

To shell into the container, do:
```
ml singularity
singularity shell --nv -B /scratch -s /bin/bash ubuntu_gpu.img 
```

Useful links:
- Nvidia Docker images: https://hub.docker.com/r/nvidia/cuda/
- Singularity hub container which I used as a base: https://singularity-hub.org/containers/1844/
