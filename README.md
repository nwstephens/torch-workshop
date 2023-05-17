# torch-workshop

This workshop presents a conceptual overview of the [R interface for PyTorch](https://torch.mlverse.org/). Emphasis will be on basic structures and applications for deep learning. With torch there is no need to install or use Python. Torch and its associated packages – torchaudio, torchvision, luz – will run on CPU or GPU. This workshop will demonstrate torch for R using an NVIDIA GPU environment, which significantly accelerates computations.

## Materials

![](Keydana.jpg)

Materials for this workshop are based on the new book, [Deep Learning and Scientific Computing with R torch](https://skeydan.github.io/Deep-Learning-and-Scientific-Computing-with-R-torch/) by [Sigrid Keydana](https://divergences.xyz/). This workshop is part of the Rocky Mountain Advanced Computing Consortium’s (RMACC) High Performance Computing Symposium (5/18/2023). [For slides click here](https://rpubs.com/nwstephens/torch-workshop).

## Getting Started

[Torch for R](https://torch.mlverse.org/) is an open source machine learning framework based on PyTorch. `torch` provides fast array computation with strong GPU acceleration and a neural networks library built on a tape-based autograd system. The "torch for R"" ecosystem is a collection of extensions for torch. For details on getting started, see the [Installation Vignette](https://torch.mlverse.org/docs/articles/installation.html).

### Windows and Mac (CPU)

1. Install RStudio desktop
2. Install `torch`

```{r}
install.packages("torch")
```

3. Clone this repos and make sure the working directory is `torch-workshop`
4. Download `Tiny ImageNet` data

```{r}
tiny_imagenet_dataset(".", download = TRUE)
```

5. Install the `modeldata` package from the `2021-06-08` snapshot

```{r}
install.packages("modeldata", repos = "https://packagemanager.rstudio.com/cran/__linux__/bionic/2021-06-08")
```

### Linux (GPU)

1. Have a CUDA compatible NVIDIA GPU with [compute capability](https://developer.nvidia.com/cuda-gpus#compute) 6.0 or higher
2. Install the [NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html)
3. Pull and run the RStudio Rocker container

```{bash}
docker pull rocker/rstudio
docker run --gpus=all -d -t -e PASSWORD=rstudio -p 8787:8787 --name rstudio rocker/rstudio
```

4. Open RStudio Server from your browser by opening `http://<your.ip.address>:8787/`. Make sure port 8787 is open. Your username is `rstudio` and your password is `rstudio`
5. Configure RStudio Server to download package binaries from the [Posit Package Manager](https://packagemanager.rstudio.com/client/#/)

```
# For Red Hat 8 use:
https://packagemanager.rstudio.com/cran/__linux__/centos8/latest

# For Ubuntu 20.04 use:
https://packagemanager.rstudio.com/cran/__linux__/focal/latest
```
6. Install `torch` from the pre-built binaries (Warning! This download is 2Gb)

```{r}
options(timeout = 600)
install.packages("torch", repos = "https://storage.googleapis.com/torch-lantern-builds/packages/cu117/0.10.0/")
```

7. Make sure your CUDA device is available (this should return `TRUE`)

```{r}
library(torch)
cuda_is_available()
```

8. Clone this repos and make sure the working directory is `torch-workshop`
9. Download `Tiny ImageNet` data

```{bash}
wget http://cs231n.stanford.edu/tiny-imagenet-200.zip
unzip tiny-imagenet-200.zip
```

10. Install the `modeldata` package from the `2021-06-08` snapshot

```{r}
install.packages("modeldata", repos = "https://packagemanager.rstudio.com/cran/__linux__/bionic/2021-06-08")
```
