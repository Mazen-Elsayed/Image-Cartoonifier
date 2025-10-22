# Image Cartoonifier

A Python-based image processing project that transforms regular photographs into cartoon-style images with flat colors and bold edges.

## Overview

This project implements an image cartoonification pipeline using OpenCV. It converts standard photos into cartoon-like images by:
- Detecting edges using Laplacian filter
- Creating a black-and-white sketch
- Smoothing colors with bilateral filtering
- Combining the sketch with flat colors for the final cartoon effect

## Features

- **Edge Detection**: Uses Laplacian filter with adjustable kernel sizes (3×3, 5×5, 7×7)
- **Noise Reduction**: Median filter preprocessing to ensure clean edge detection
- **Color Smoothing**: Bilateral filter applied iteratively to create flat cartoon colors
- **Binary Sketch**: Threshold-based conversion to clean black-and-white edges
- **Customizable Parameters**: Adjustable filter sizes and iteration counts for different styles

## Requirements

See `requirements.txt` for all dependencies. Main libraries:
- OpenCV (cv2)
- NumPy
- Matplotlib

## Installation

1. Clone this repository:
```bash
git clone <your-repo-url>
cd image-cartoonifier
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

## Usage

1. Place your input image in the `images/input/` folder
2. Open `cartoonify.ipynb` in Jupyter Notebook or VS Code
3. Update the `image_path` variable to point to your image:
```python
image_path = 'images/input/your_image.jpg'
```
4. Run all cells to process the image
5. Output will be saved in `images/output/`

## How It Works

### Pipeline Steps:

1. **Load Image**: Read input image and convert from BGR to RGB
2. **Grayscale Conversion**: Convert to grayscale for edge detection
3. **Median Filtering**: Remove noise while preserving edges (kernel sizes: 3, 5, 7)
4. **Laplacian Edge Detection**: Detect edges using second derivative (kernel sizes: 3, 5, 7)
5. **Binary Thresholding**: Create clean sketch with threshold = 70
6. **Bilateral Filtering**: Smooth colors iteratively while keeping edges sharp
   - Parameters: d=9, sigmaColor=9, sigmaSpace=7
   - Iterations: 1, 3, 7, or 1000 for different effects
7. **Combine**: Overlay sketch edges onto smoothed colors using bitwise AND
8. **Save Output**: Export final cartoon image

### Key Parameters:

- **Median Blur Kernel**: Controls noise reduction strength (3×3, 5×5, 7×7)
- **Laplacian Kernel**: Affects edge detection sensitivity (3×3, 5×5, 7×7)
- **Bilateral Filter Iterations**: More iterations = flatter colors (typical: 7-1000)
- **Threshold Value**: Determines sketch edge intensity (default: 70)

## Examples

Input images and their cartoonified outputs can be found in the `images/` directory.

## Technical Details

### Filters Used:

- **Median Filter**: Edge-preserving noise reduction
- **Laplacian Filter**: Second derivative edge detector (sensitive to fine details)
- **Bilateral Filter**: Smooths colors while preserving edges (key to cartoon effect)

### Why These Filters?

- **Median over Gaussian**: Better edge preservation for cleaner sketches
- **Laplacian over Sobel**: Detects edges in all directions simultaneously
- **Multiple Bilateral Iterations**: Progressive color flattening is faster and more effective than a single large filter

## Project Structure

```
image-cartoonifier/
├── cartoonify.ipynb          # Main Jupyter notebook
├── README.md                 # This file
├── requirements.txt          # Python dependencies
└── images/
    ├── input/               # Place input images here
    └── output/              # Cartoonified images saved here
```

## Notes

- Works best with high-contrast images
- Portraits and landscapes produce good results
- Adjust bilateral filter iterations based on desired flatness level
- Experiment with threshold values for different sketch intensities