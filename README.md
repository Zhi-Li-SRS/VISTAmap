# VISTAmap: Stripes Removal for Optical Microscopy Images

This project provides a Python implementation of VISTAmap (VIgnetted Stitched-Tile Adjustment using Morphological Adaptive Processing) for removing stitching stripes and correcting vignetting in optical microscopy images, specifically designed for SRS and other whole slide imaging modalities.

## Comparison of Raw and Processed Images
![SRS DeStripe Comparison](https://github.com/Zhi-Li-SRS/SRS_DeStripe/blob/main/comparison/raw_vs_removed.png?raw=true)

- **Left Image**: Raw SRS (Stimulated Raman Scattering) image showing prominent stripes. These stripes are common in whole slide imaging in SRS microscopy.

- **Right Image**: The same SRS image after processing with VISTAmap. 

## Installation

1. Clone this repository:
   ```
   git clone https://github.com/Zhi-Li-SRS/SRS_DeStripe.git
   cd SRS_DeStripe
   ```

2. Create a virtual environment (optional but recommended):
   ```
   conda create -n destripe python=3.9
   conda activate destripe
   ```

3. Install the required packages:
   ```
   pip install -r requirements.txt
   ```

## Usage

### Basic Usage
Run the script with the following command:

```
python vistamap.py --image_path path/to/your/image.tif --mask_path path/to/your/mask.tif --output_path output/result.tif --tile_size 250
```

### Command Line Arguments
- `--image_path`: Path to the input image file (default: "MAX_Left-HSI.tif")
- `--mask_path`: Path to the mask file (default: "MAX_Left-HSI-mask.tif"). If the mask file doesn't exist or isn't provided, the algorithm will automatically generate a mask using texture-based tissue isolation
- `--output_path`: Path to save the processed output image (default: "output/process_protein.tif")
- `--tile_size`: Size of each tile in pixels (default: 250). If provided, this value will be used instead of FFT-based tile size detection

### Automatic Mask Generation
If you don't have a mask file, VISTAmap can automatically generate one:

```
python vistamap.py --image_path your_image.tif --output_path output/result.tif --tile_size 250
```

The algorithm uses texture-based morphological operations to automatically isolate tissue regions from the background.


## Requirements

The script requires the following Python packages (automatically installed via requirements.txt):
- numpy==1.24.3
- opencv-python==4.8.0.76
- opencv-contrib-python==4.8.0.76
- scipy==1.10.1
- scikit-learn==1.3.0
- tifffile==2024.9.20
- matplotlib (for visualization)

## Output

The algorithm generates:
- **Processed image**: Saved at the specified output path
- **Comparison image**: A side-by-side comparison saved as `[output_name]_compare.png`

## Recommendations

- **Mask Usage**: For optimal results, provide a binary mask separating foreground tissue from background. If unavailable, the automatic mask generation works well for most tissue samples.
- **Tile Size**: If you know the exact tile size used during image acquisition, specify it using `--tile_size` for more accurate and faster processing.
- **Image Format**: The algorithm specifically works with 2D images.
- **Performance**: VISTAmap is particularly effective for images with both striping artifacts and vignetting issues common in large-area stitching issue in optical microscopy.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Citation

If you use this codebase or otherwise found our work valuable, please cite our paper:

```bibtex
@article{vistamap2025,
    title={Single-Frame Vignetting Correction for Post-Stitched-Tile Imaging Using VISTAmap},
    author={Fung, AA and Fung, AH and Li, Z and Shi, L},
    journal={Nanomaterials},
    year={2025}
}
```



