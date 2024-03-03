# LSFM Image Stitcher
- Created by the [Yongsoo Kim Lab](https://kimlab.io/)

This code is designed to stitch together images taken by light sheet fluorescence microscopy (LSFM) using SmartSPIM (product of LifeCanvas Technologies). It takes raw TIF (.tif) files from the SmartSPIM system and stitches them together based on the best cross matching coordinates. The code calls on ImageJ for image processing.

## Description of code's functionality (pseudocode)

"This program takes LSFM data acquired as a set of tiled images and stitches them together to form a 3D image (stored as a set of 2D images). This is a parallelized stitching algorithm optimized for conserving hard drive space and memory consumption initially based on Wobbly Stitcher17. The algorithm starts by collecting metadata and calculating tile normalization parameters to be applied during stitching. Stitching begins by collecting 10% outer edges of each image tile and making a maximum intensity projection (MIP) of outer edges in the axial (z) direction for every set of 32 slices of the entire stack. The algorithm then aligns z coordinates of MIP images across image columns, followed by the x and y coordinate alignment. Finally, 32 slices within each MIP are adjusted based on curve fitting to reach final coordinates of each tile. This is run on one channel and other channels from the same acquisition time are stitched using identical parameters. This algorithm only reads the raw images two times (at the beginning and the final writing), which significantly reduces the bottleneck of reading large files in a storage drive. Finally, there are options to create resampled versions of the dataset and move the data to an alternate location." [(Kronman et al, 2023)](https://www.biorxiv.org/content/10.1101/2023.09.14.557789v1)

- Previously implemented for:
    - Whole mouse brain mapping of the oxytocin wiring system: [doi](https://doi.org/10.1523/JNEUROSCI.0307-22.2022)
    - Cerebrovasculature and vascular cell type mapping in the adult and aging mouse brain: [preprint](https://www.biorxiv.org/content/10.1101/2023.05.23.541998v1)
    - Creating a multimodal developmental mouse brain common coordinate framework: [preprint](https://www.biorxiv.org/content/10.1101/2023.09.14.557789v1)

## System Requirements
> Please make sure the following requirements (ie. operating system, software) are installed on your machine prior to code use.

### Hardware
Ideally, a high-performance computer with a 32- or 64-core processor to perform parallel computing in MATLAB.
- Microsoft Windows 10, 64-bit (operating system that the code was built and tested with) 

### Software
#### Environment
The code was initially developed and tested on
- MATLAB 2019a
- ImageJ (FIJI) win64

#### Requirements
- MATLAB (MathWorks): [download](https://www.mathworks.com/products/matlab.html?s_tid=hp_products_matlab)
  - Further Tested using MATLAB versions 2019a, R2020a, and R2021b
  - Toolbox Dependencies:
    - Curve Fitting Toolbox
    - Image Processing Toolbox
    - Optimization Toolbox
    - Parallel Computing Toolbox
    - Signal Processing Toolbox
    - Wavelet Toolbox
- FIJI (ImageJ2): [download](https://imagej.net/software/fiji/)
  - Tested using ImageJ (1.53t) with Java 1.8.0_172 (64-bit)

 ## Installation guide
To Install this program, simply unzip the main directory and store it in a location that you can access via MATLAB. This should only take seconds.
  
## How To Use

1. Create a new folder in a local computer drive (preferable) and rename with sample ID information. This will be the working directory containing the stitched data output.
2. Open the script **RUN_THIS_FILE.m** in MATLAB.
3. Under **Basic Settings**, set "Source_folder" equal to the path for the main directory containing the imaged TIFs, meta data, and tile settings.
4. Example directory structure:
    - Ex_488_Em_525
    - Ex_561_Em_600
    - Ex_642_Em_680
    - ASI_logging.txt
    - metadata.txt
    - TileSettings.ini
4. Set "Working_folder" equal to the path for the working directory created in Step 1. Stitched data output will be deposited here, along with copies of the raw TIFs, meta data, and tile settings.
5. Set "channel_for_stitching" equal to the "number of channels" used (ie. 2, if all three wavelengths were acquired).
    - 00 = 488 nm (green)
    - 01 = 561 nm (red)
    - 02 = 642 nm (far red)
6. To create a downsized TIF stack of the stitched raw data for easier viewing, set *"making_shrink_after_stitching"* equal to 1. Set this function equal to 0 if you do not want a downsized image.
- Set the downsizing factors for XY and Z directions.
  - For example, if downsizing by a factor of 10, set the *"shrink_ratio"* equal to [5.55, 2].
   

## Limitations
The code is designed for stitching SmartSPIM (LifeCanvas) acquired images with its file structure and potential artifacts that other microscopes might not have.



## Disclaimer:
* This script is provided as-is and may require customization to suit specific use cases. There are many hardcoded paths and values that are optimized for our datasets. You may need to modify some values to optimize for your data. Users are encouraged to review and modify the script as needed for their research projects.



## License
Shield: [![CC BY 4.0][cc-by-shield]][cc-by]

This work is licensed under a
[Creative Commons Attribution 4.0 International License][cc-by].

[![CC BY 4.0][cc-by-image]][cc-by]

[cc-by]: http://creativecommons.org/licenses/by/4.0/
[cc-by-image]: https://i.creativecommons.org/l/by/4.0/88x31.png
[cc-by-shield]: https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg




## Conditions for Use
The DevCCF is a [Brain Initiative Cell Census Network](https://biccn.org/) (BICCN) resource.

BICCN data, tools, and resources, including the DevCCF are generally released under the Creative Commons Attribution 4.0 International Public License (CC BY 4.0, https://creativecommons.org/licenses/by/4.0/legalcode) (“CC BY 4.0 License”). Under the  CC BY 4.0 License external data users may freely download, analyze and publish results based on any BICCN open-access data and tools as soon as they are released, provided they give appropriate credit, a link to the license, and indicate if changes were made.  The CC BY 4.0 License applies to all open-access datasets generated by individual members of the Network, regardless of type or size.

Researchers using unpublished BICCN data are encouraged to contact the data producers to discuss possible coordinated publications; however, this is optional. The Network will continue to publish the results of its own analysis efforts in independent publications.




## Citation Information
We require that researchers who use BICCN datasets (published or unpublished) in any tools, web applications, presentations, and publications cite and acknowledge the BICCN and BICCN production laboratory(s) for referenced dataset(s).

DevCCF Preprint citation:
Kronman, F. A. et al. Developmental Mouse Brain Common Coordinate Framework. bioRxiv 2023.09.14.557789 (2023) doi:10.1101/2023.09.14.557789.

DevCCF citation will be updated once published in peer review.


