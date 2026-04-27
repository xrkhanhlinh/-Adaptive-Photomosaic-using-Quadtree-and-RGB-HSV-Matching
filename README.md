# Adaptive Photomosaic using Quadtree and RGB/HSV Matching

## Overview
This project implements an **adaptive photomosaic system** that reconstructs an input image using a collection of small tile images.  
Instead of dividing the image into a fixed grid, the system analyzes image detail using **Canny edge detection** and applies **quadtree-based adaptive splitting**:

- **High-detail regions** → smaller blocks  
- **Smooth regions** → larger blocks  

Each block is then matched with the most suitable tile using **RGB** or **HSV** color features.  
To improve the visual result, the system also includes:
- **anti-repeat tile placement**
- **blending with the original image**
- **quality evaluation using MSE, PSNR, and SSIM**

---

## Main Idea
The goal of this project is to recreate a target image from many small images while preserving the overall visual structure of the original image.

Unlike a basic photomosaic approach that uses a uniform grid, this project uses an **adaptive strategy**:
- regions with more edges or stronger color variation are divided into smaller blocks
- simple background regions are kept larger

This helps balance:
- visual quality
- structural preservation
- computational cost

---

## Pipeline
The system follows these main steps:

1. **Load tile dataset**  
   Read all tile images and resize them to a base tile size.

2. **Load input image**  
   Read the target image and resize it while keeping aspect ratio.

3. **Compute edge map**  
   Use Canny edge detection to estimate local image detail.

4. **Build adaptive blocks**  
   Apply quadtree splitting based on:
   - edge density
   - local color variation

5. **Extract block features**  
   Compute representative color features for each block.

6. **Match tiles**
   Select the best tile for each block using:
   - RGB matching
   - or HSV matching

7. **Anti-repeat placement**  
   Reduce visual repetition by discouraging nearby blocks from using the same tile.

8. **Build photomosaic**  
   Resize the selected tile to the current block size and place it into the mosaic.

9. **Blend with original image**  
   Improve readability by mixing the mosaic with the original image.

10. **Evaluate results**  
    Compare outputs using:
    - **MSE**
    - **PSNR**
    - **SSIM**

---

## Key Features
- **Adaptive block size with quadtree**
- **Canny-based detail analysis**
- **RGB and HSV tile matching**
- **Anti-repeat tile placement**
- **Blending for better visual quality**
- **Quantitative evaluation with image quality metrics**

---

## Output Files
The program generates multiple outputs for comparison, such as:

- `00_original.png`
- `01_edge_map.png`
- `02_block_map.png`
- `03_rgb_mosaic.png`
- `04_hsv_mosaic.png`
- `05_rgb_blend.png`
- `06_hsv_blend.png`
- `07_rgb_blend_sharp.png`
- `08_hsv_blend_sharp.png`

It also prints:
- a metrics table
- tile usage statistics

---

## Evaluation Metrics

### MSE
Measures the average squared pixel error between the output image and the reference image.

### PSNR
Measures reconstruction quality based on pixel-level error.  
Higher PSNR generally indicates a result closer to the original image.

### SSIM
Measures structural similarity between images.  
This metric is especially useful in photomosaic because it better reflects how well the output preserves overall visual structure.

---

## Why This Project
This project is a good practical exercise for fundamental image processing topics such as:

- color spaces (**RGB**, **HSV**)
- edge detection (**Canny**)
- adaptive image partitioning (**quadtree**)
- feature-based matching
- image quality evaluation

It also shows the trade-off between:
- image similarity
- mosaic appearance
- block size
- runtime

---

## Future Improvements
Possible extensions include:

- larger and more diverse tile datasets
- better tile scoring strategies
- texture-aware matching
- face-aware or saliency-aware region splitting
- faster search and matching
- improved blending methods

---

## Conclusion
This project builds an adaptive photomosaic pipeline that combines **detail-aware block splitting**, **color-based tile matching**, **anti-repeat placement**, and **post-processing**.  
The result is a more flexible and visually meaningful photomosaic compared to a basic fixed-grid approach.
