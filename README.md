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

### Single image
```
python vistamap.py \
  --image_path input/787.tif \
  --mask_path input/srs_mask.tif \
  --output_path output/lung/787.tif \
  --tile_size 250
```

### Batch processing with one shared mask
```
python vistamap.py \
  --image_path input \
  --mask_path input/srs_mask.tif \
  --output_dir output/lung
```

To also save comparison images in batch mode, add:
```
--save_comparison
```

### Command Line Arguments
- `--image_path`: Path to a single image file or an input directory for batch processing (default: `input`).
- `--mask_path`: Path to the mask file (default: `input/srs_mask.tif`). If missing or not found, a mask will be generated automatically using texture-based tissue isolation.
- `--output_path`: Path to save the processed output image in single-file mode (default: `output/lung/787.tif`).
- `--output_dir`: Directory to save outputs in batch mode (default: `output/lung`).
- `--tile_size`: Size of each tile in pixels (default: 250). If provided, this value will be used instead of FFT-based tile size detection.
- `--save_comparison`: When set, also save a side-by-side comparison figure (`*_compare.png`) next to each output image.

### Automatic Mask Generation
If you don't have a mask file, VISTAmap can automatically generate one.

- Single image (no mask provided):
```
python vistamap.py --image_path input/787.tif --output_path output/lung/787.tif --tile_size 250
```

- Batch processing (no mask provided):
```
python vistamap.py --image_path input --output_dir output/lung --tile_size 250
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
- **Processed image**: Saved at the specified `--output_path` (single-file) or inside `--output_dir` (batch mode).
- **Comparison image (optional)**: Saved only when `--save_comparison` is provided, as `[output_basename]_compare.png` in the same directory as the output.

## Recommendations

- **Mask Usage**: For optimal results, provide a binary mask separating foreground tissue from background. If unavailable, the automatic mask generation works well for most tissue samples.
- **Tile Size**: If you know the exact tile size used during image acquisition, specify it using `--tile_size` for more accurate and faster processing.
- **Image Format**: The algorithm specifically works with 2D images.
- **Performance**: VISTAmap is particularly effective for images with both striping artifacts and vignetting issues common in large-area stitching issue in optical microscopy.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Citation

If you use this codebase or otherwise found our work valuable, please cite our paper:

```
@article{paper,
      title={Single-Frame Vignetting Correction for Post-Stitched-Tile Imaging Using VISTAmap}, 
      author={Fung AA, Fung AH, Li Z, Shi L},
      year={2025},
      journal={Nanomaterials}
}
```



