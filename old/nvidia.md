# Some tips to install your NVIDIA drivers and CUDA on Linux for Pytorch

If you are using Pytorch framework, chances are that you will struggle to install all dependencies correctly.
At least, it was my case.

To draw the big picture, installing Pytorch on a GPU requires three installations:
- NVIDIA drivers to allow your computer to talk with your GPU;
- CUDA toolkit to compile Pytorch code to the GPU;
- and of course, Pytorch library.

During this tutorial, you need to know the name of your GPU. If you don't remember, you can retrieve it with:

```
lspci | grep VGA
```

## Correspondance between Pytorch versions and CUDA versions.

There are two cases: either you want Pytorch > 1.0, either you are working on legacy code that requires Pytorch < 1.0.

In the first case, it means you require a version of CUDA of **9.0* or *10.0* -- it is the [only available options for now](https://pytorch.org/get-started/locally/).
In the second case, you can do down until CUDA 7.5. Of course, you can also install Pytorch without CUDA, but in this case, you will not be able to run your code on GPUs. 


## Which GPU drivers can you run? 

Unfortunately, we don't all have the latest-fanciest GPU available. Unfortunately again, NVIDIA removes supports for its oldest GPUs. Consequently, you should check which versions of GPUs you want to use. 

To check it, visit [NVIDIA website](https://www.nvidia.com/Download/index.aspx) and find the most recent version that is supported by your GPU. 

For example, if you have an RTX2070, you want to install the latest LTS driver to date, 430.26.
If you have a Quadro FX 580, you want to install the 340.107 drivers.

## Correspondance between CUDA versions and GPU drivers

Now, you need to find which version of CUDA can be run with your drivers requirements following [this table](https://docs.nvidia.com/deploy/cuda-compatibility/index.html#binary-compatibility__table-toolkit-driver).

Following previous examples, both CUDA 9.0 and CUDA 10.0 can be chosen with an RTX2070, whereas... bad news, no CUDA version support your old FX580! 

## Download your installer 

Now you should be decided on which version of CUDA and drivers you want. 


## Download your installer 

Now you should be decided on which version of CUDA 
## nvidia-drm appears to be loaded 

https://unix.stackexchange.com/questions/440840/how-to-unload-kernel-module-nvidia-drm


## Check NVIDIA and CUDA work properly 

`nvidia-smi` and `nvcc --version`
