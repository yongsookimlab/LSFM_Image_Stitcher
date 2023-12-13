# LSFM Image Stitcher
This code is designed to stitch together images taken by light sheet fluorescence microscopy (LSFM) using SmartSPIM (product of LifeCanvas Technologies). It takes raw TIF (.tif) files from the SmartSPIM system, deforms the image to correct the aberration, adjust the intensity profile to correct the photo bleaching, and finally stitch them together based on the best cross matching coordinates. The code calls on ImageJ for image processing.  

## How To Use
The following programs must first be installed in your computer before code launch: MATLAB, ImageJ (FIJI)

1. Create a new folder in a local drive (preferable) and rename with sample ID information. This will be the working directory containing the stitched data output.
2. Open the script *RUN_THIS_FILE.m* in MATLAB.
3. Under *Basic Settings*, set *"Source_folder"* equal to the path for the main directory containing the imaged TIFs, meta data, and tile settings.
4. Example directory structure:
    - Ex_488_Em_525
    - Ex_561_Em_600
    - Ex_642_Em_680
    - ASI_logging.txt
    - metadata.txt
    - TileSettings.ini
4. Set *"Working_folder"* equal to the path for the working directory created in Step 1. Stitched data output will be deposited here, along with copies of the raw TIFs, meta data, and tile settings.
5. Set *"channel_for_stitching"* equal to the "number of channels" used (ie. 2, if all three wavelengths were acquired).
    - 00 = 488 nm (green)
    - 01 = 561 nm (red)
    - 02 = 642 nm (far red)
6. To create a downsized TIF stack of the stitched raw data for easier viewing, set *"making_shrink_after_stitching"* equal to 1. Set this function equal to 0 if you do not want a downsized image.
- Set the downsizing factors for XY and Z directions.
  - For example, if downsizing by a factor of 10, set the *"shrink_ratio"* equal to [5.55, 2].
   

## Limitations
The code is designed for stitching SmartSPIM (LifeCanvas) acquired images with its file structure and potential artifacts that other microscopes might not have.

## Environment
The code was developed and tested on
- MATLAB 2019a
- ImageJ (FIJI) win64

## License
Free academic use.
