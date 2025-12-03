# DDPM in C++ (LibTorch)

![DDPM Sample](https://github.com/rajtilakls2510/diffusion_mnist/raw/main/ddpm/diffusion_1764730964.png)


Implementation of **Denoising Diffusion Probabilistic Models (DDPM)** in modern C++ using **LibTorch**. The original DDPM paper can be found here:

[https://arxiv.org/abs/2006.11239](https://arxiv.org/abs/2006.11239)

This README includes instructions to **set up LibTorch**, **prepare the MNIST dataset**, **train the DDPM model**, and **generate samples** using a trained checkpoint.

---

## Build & Setup Instructions

### 1. Download LibTorch

1. Visit the official PyTorch website.
2. In the **Language** dropdown, choose **LibTorch**.
3. Download the appropriate **CPU** or **CUDA** LibTorch version.
4. Extract the downloaded folder and place it inside:

```
/opt/libtorch
```

Your LibTorch CMake config should now be located at:

```
/opt/libtorch/share/cmake/Torch/TorchConfig.cmake
```

---

### 2. Build the project

From the **root directory** of this repository:

```bash
mkdir build/
```

Before building, open `CMakeLists.txt` and replace:

```
/path/to/libtorch/
```

with:

```
/opt/libtorch
```

Then run:

```bash
cd build
cmake ..
make -j4
```

This compiles the project and generates binaries inside `build/bin/`.

---

## MNIST Dataset Setup

1. In the **root directory**, create the following folder:

```
mkdir -p data/mnist/
```

2. Download the 4 MNIST data files from the link below:

Google Drive link:

```
https://drive.google.com/drive/folders/1kPywbt6T_sXG-ZhiaM4w0sxQBFfxSiK3?usp=sharing
```

3. Place all 4 downloaded files directly inside:

```
data/mnist/
```

The folder structure should now look like:

```
data/
  mnist/
    train-images-idx3-ubyte
    train-labels-idx1-ubyte
    t10k-images-idx3-ubyte
    t10k-labels-idx1-ubyte
```

---

## Training

To start training the DDPM model on MNIST:

```bash
cd build/
./train ../data/mnist ../checkpoint1/
```

This command:

* Loads the MNIST dataset from `../data/mnist`
* Saves checkpoints into `../checkpoint1/`
* Trains for **100 epochs**
* Uses a **batch size of 64** by default

---

## Sampling

To generate a sample from a trained checkpoint:

```bash
cd build/
./sample ../checkpoint1/
```

This command:

* Loads the trained diffusion model from the directory `../checkpoint1/`
* Produces **one generated sample**
* Creates a **video of the reverse diffusion process**
* Saves the **final generated image** inside the same checkpoint directory

---