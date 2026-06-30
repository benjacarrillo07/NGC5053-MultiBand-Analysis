# Multi-Band Photometry and Spatial Analysis of NGC 5053

This repository contains the configuration files, catalogs, and documentation required to reproduce the photometric extraction and spatial analysis of the globular cluster NGC 5053, as presented in the paper: *"Multi-Band Photometry and Spatial Analysis of the Globular Cluster NGC 5053: Revealing Tidal Disruption through SExtractor and Gaia DR3 Kinematics"*.

## Repository Structure

* `data/`
  * `raw/`: *(Note: Raw FITS images exceed GitHub's file size limits. See "Data Acquisition" below to download them).*
  * `catalogs/`: Final combined catalogs (g, r, z bands) and Gaia DR3 cross-matches.
* `sextractor/`: Complete suite of SExtractor configuration files used for point-source extraction (`.sex`, `.param`, `.conv`, `.nnw`).
* `analysis/`: TOPCAT session files containing the exact Boolean masks and kinematic subsets.
* `paper/`: LaTeX source code, `.bib` references, and generated figures.

## Software Requirements

To fully reproduce this analysis in a Linux environment, you will need:
* **SExtractor** (Source-Extractor) v2.25.0 or higher.
* **TOPCAT** (Tool for OPerations on Catalogues And Tables) - *Can be executed via JAR or AppImage*.
* **LaTeX** distribution (e.g., TeX Live) for compiling the manuscript.

## Data Acquisition

The primary photometric data was obtained from the **DESI Legacy Imaging Surveys DR10**. 
To run the extraction locally, download the $g$, $r$, and $z$ band FITS cutouts centered on NGC 5053 and place them in the `data/raw/` directory.

## Reproducing the Photometry (Dual-Image Mode)

To overcome the high sky background and airglow inherent to near-infrared observations, the $z$-band photometry was extracted using SExtractor in **dual-image mode**. 

This approach uses the high signal-to-noise $r$-band image for source detection and morphological classification (`CLASS_STAR`), and strictly measures the flux within those predefined apertures on the $z$-band image.

Navigate to the root directory in your terminal and execute the following command:

```bash
sex data/raw/image_r.fits data/raw/image_z.fits -c sextractor/default.sex
