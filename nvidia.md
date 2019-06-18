# Some tips to install your NVIDIA drivers and CUDA on Ubuntu for Pytorch

If you are using Pytorch framework, chances are that you will struggle to install all dependencies correctly.
At least, it was my case.

To draw the big picture, installing Pytorch on a GPU requires three installations:
- NVIDIA drivers to allow your computer to talk with your GPU;
- CUDA toolkit to compile Pytorch code to the GPU;
- and of course, Pytorch library.

## Find which version of CUDA you want.

There are two cases: either you want Pytorch > 1.0, either you are working on legacy code that requires Pytorch < 1.0.

In the first case, it means you require a version of CUDA of **9.0* or *10.0* (check the)


## nvidia-drm appears to be loaded 

https://unix.stackexchange.com/questions/440840/how-to-unload-kernel-module-nvidia-drm


## Check NVIDIA and CUDA work properly 

`nvidia-smi` and `nvcc --version`
