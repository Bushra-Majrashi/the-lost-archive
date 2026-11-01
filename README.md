# The Lost Archive - LoRA Training Notebook

A custom LoRA model trained on Stable Diffusion to generate AI artwork
in a personal visual style, using the Kohya-ss training framework on Google Colab.

## Overview

This notebook trains a LoRA (Low-Rank Adaptation) model on a curated set
of personal photographs, then uses the trained weights with ControlNet
(canny + depth) to generate stylized artwork from new source images.

The generated works explore Arabian and Saudi cultural scenes through
a learned personal aesthetic.

## Workflow

1. Run the config cell first - set DRIVE_ROOT to your own folder
2. Mount Google Drive and verify GPU (T4)
3. Install diffusers, transformers, and Kohya-ss sd-scripts
4. Verify training dataset (images + captions)
5. Train LoRA for 8000 steps with cosine restart scheduler
6. Load ControlNet pipeline with trained LoRA weights
7. Generate final artworks from source photos
8. Upscale outputs with Real-ESRGAN

## What You Need to Provide

None of the following are included in this repo:

    YOUR_FOLDER/
      models/realisticVisionV60B1_v51VAE.safetensors   (download separately)
      prod_train/img/10_BushraStyle/                    (your images + .txt captions)
      raw_input/                                        (source photos for generation)

The 10_ prefix in the folder name is the Kohya-ss repeat count.

To train from scratch, remove the --network_weights line from the training cell.
To resume from a checkpoint, set CHECKPOINT to your own .safetensors file.

## Models Used

- Training base: Realistic Vision V6.0 B1 (CreativeML OpenRAIL-M)
- Generation base: Stable Diffusion v1.5 (CreativeML OpenRAIL-M)
- ControlNet: canny + depth (lllyasviel)
- Depth estimation: Intel DPT-Large
- Upscaler: Real-ESRGAN

Model licences are separate from the code licence in this repo.

## Tech Stack

Python, PyTorch, Diffusers, Transformers, Kohya-ss sd-scripts,
ControlNet, Real-ESRGAN, Google Colab (T4 GPU)

## Setup

Edit the config cell at the top of the notebook before running:

    DRIVE_ROOT = "/content/drive/MyDrive/YOUR_FOLDER_NAME"

All other paths are derived from this variable.

## Licence

Code: MIT
Models: see each model's own licence terms above.

## Author

Bushra Majrashi
