# Image Inpainting and Super-Resolution with Diffusion Models and GANs

This project explores deep generative models for two image generation tasks:

- **Image Inpainting** using Denoising Diffusion Probabilistic Models (DDPMs)
- **Image Super-Resolution** using both Diffusion Models and GANs

The project was developed as an experimental study, with a strong focus on understanding the behavior of the models, designing the training procedures, and evaluating different approaches through quantitative and qualitative experiments.

## Project Overview

The project is divided into two parts.

### 1. Image Inpainting

Image inpainting consists of reconstructing missing regions of an image while preserving the visible parts.

The implemented approach is inspired by diffusion-based inpainting methods such as RePaint. The image is progressively noised and denoised, while the known region is continuously used to condition the generation of the missing region.

The main components explored include:

- Denoising Diffusion Probabilistic Models (DDPMs)
- U-Net-based denoisers
- Noise scheduling and iterative denoising
- Repeated noising/denoising steps to improve consistency
- Training from scratch vs. using a pretrained component
- Experiments with different inference hyperparameters
- Quantitative evaluation using **Fréchet Inception Distance (FID)**
- Human evaluation through pairwise image comparisons

The model was evaluated on **ImageNet** and **CelebA**, and compared against existing approaches including MAT and Palette.

### 2. Image Super-Resolution

The second part investigates the task of increasing the resolution of an image while generating plausible high-resolution details.

Two different approaches were implemented and evaluated:

#### Diffusion-based Super-Resolution

A DDPM-based approach was adapted from the inpainting method.

The low-resolution image is first upscaled and then progressively refined through the diffusion process.

#### GAN-based Super-Resolution

A conditional GAN architecture was implemented using:

- Encoder-decoder architecture
- Residual blocks
- Skip connections
- Instance Normalization
- Positional Normalization
- Conditional low-resolution input
- High-resolution conditioning
- Adversarial loss
- Cycle consistency loss

During training, the balance between the generator and discriminator was investigated and adjusted experimentally.

## Experiments

A significant part of the project focused on experimentation and understanding how architectural and training choices affected the results.

Examples include:

- Different denoising strategies
- Different diffusion hyperparameters
- Different model depths
- Different image resolutions
- Different numbers of downsampling blocks
- Training stability of the GAN
- Combining inpainting and super-resolution
- Comparison between diffusion and GAN-based approaches

Due to hardware limitations, experiments were primarily performed at resolutions up to **128×128 for inpainting** and **128×128 → 256×256 for super-resolution**.

## Results

### Image Inpainting

FID results on ImageNet:

| Model | Small Mask | Large Mask |
|---|---:|---:|
| This project | 10.8 | 15.0 |
| MAT | 1.07 | 2.9 |
| Palette | 5.2 | 8.9 |

FID results on CelebA:

| Model | Small Mask | Large Mask |
|---|---:|---:|
| This project | 15.8 | 30.9 |
| MAT | 2.86 | 4.86 |
| Palette | 11.7 | 20.8 |

Human evaluation was also performed by asking participants to choose between generated images from the different models.

The experiments showed that larger masks generally make the inpainting task more difficult, particularly for human faces. The results also highlighted the importance of the denoiser architecture and its ability to capture the underlying image distribution.

### Super-Resolution

FID results:

| Model | ImageNet | CelebA |
|---|---:|---:|
| This project's GAN | 25.8 | 28.4 |
| This project's Diffusion Model | 30.2 | 38.4 |
| Pretrained ResNet | 19.3 | 25.4 |

The GAN performed better than the diffusion-based approach in the experiments.

The effect of model depth was also investigated. For the GAN, increasing the number of downsampling blocks improved the FID:

| Downsampling Blocks | ImageNet | CelebA |
|---:|---:|---:|
| 0 | 35.6 | 38.2 |
| 1 | 28.1 | 32.2 |
| 2 | 25.8 | 28.4 |

The experiments suggest that a deeper architecture could potentially improve performance further, although available hardware limited the model size and image resolution that could be explored.

## Technical Topics

The project provided practical experience with:

- Deep Learning
- Generative Models
- Diffusion Models
- DDPMs
- GANs
- Image Inpainting
- Image Super-Resolution
- U-Net architectures
- Residual Networks
- Encoder-decoder architectures
- Skip Connections
- Instance Normalization
- Positional Normalization
- Adversarial Training
- Cycle Consistency Loss
- FID
- Experimental model evaluation
- Hyperparameter experimentation

## Repository Structure

The repository contains the code and notebooks used for the experiments.

```text
.
├── Inpainting_and_super_resolution.ipynb
├── report/
│   ├── ...
└── README.md
