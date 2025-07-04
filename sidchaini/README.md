# Supernova Spectroscopy Analysis Pipeline

This directory contains my reimplementation of the WISeREP download for comprehensive analysis of supernova spectra.

## Directory Structure

### 0. example of spectra - sdss/
Example SDSS spectra and notebooks demonstrating how to work with FITS files using AstroPy. This is a reference for myself to see the SDSS spectral format.

### 1. Download ALL WISeRep data
Scripts and notebooks for systematically downloading supernova spectra from the WISeREP repository. 
- `wiserep_downloader.py`: Downloads all spectra.

### 2. EDA Metadata and Spectra
Some EDA for me to see while I read spectra; to see what kinds of objects are failing, and then iteratively handle them later in #3 (Read and Make Single Dataset).

### 3. Read and Make Single Dataset
Scripts for combining and standardizing the SDSS and WISeREP data into a single big dataset (`tensors`). As of April 19, I have successfully read 45,062 of the 54,005 spectra downloaded, and ran basic tests on them to make sure the wavelength and flux read make sense. (See the [script](https://github.com/sidchaini/Death-and-Taxes/blob/main/sidchaini/sidhelpers.py) for more details on the checks.


— Sid Chaini


## Changelog
While creating this dataset, I decided to keep a log of every single thing I've done, to maintain reproducibility.
- **2025-05-07**:
    - Some other things have popped up for this month, but I'll be returning to this in June!

- **2025-04-18**:
    - Created a [helper script](https://github.com/sidchaini/Death-and-Taxes/blob/main/sidchaini/sidhelpers.py) to run common-sense checks on the data being read. This is to ensure that the automated reading of spectra gives us trends we expect: units, range, monotonicity, positivity etc. Take a look at the script for more details!
    - Iteratively modified the helper script to keep eliminating points of failure for spectra reading, and ended with 45,062 of the 54,005 spectra being successfully read (and passing above checks).

- **2025-03-10**: 
    - Downloaded all spectra and zip files by running script in `1. download ALL wise data`. 
    - Once downloaded, I consolidated everything into a single header file `wiserep_spectra_combined.csv` and a `spectra.tar.gz`. 
    - I also uploaded a backup to Google Drive: [URL](https://drive.google.com/drive/folders/1Vnei8ACiY5gjRboYTPTQN2t569oPIRDi?usp=sharing)
    - Tried using [DVC](https://dvc.org/) to keep track of dataset, but couldn't get GDrive to work due to UD restrictions.
- **2025-03-11**: 
    - Decided to try using Kaggle to host the dataset. Uploaded `wiserep_spectra_combined.csv` and `spectra.tar.gz` to Kaggle, but ran into an error due to the presence of the char ':' in spectra filenames.
    - Manually cleaned and changed the error-causing ':' to a '_'. (e.g. `mv CSS161010:045834-081803_2457679.64_NOT_ALFOSC_None.txt CSS161010_045834-081803_2457679.64_NOT_ALFOSC_None.txt`)
    - While doing this, I decided to run a check on the filenames in `1.2. check_dataset.ipynb` and found out that there were some files referenced in `wiserep_spectra_combined.csv` but not present in `spectra/` (after extracting `spectra.tar.gz`). So, I found out what files were missing, and manually downloaded them from WISe.
    - After fixing these changes, I finally uploaded the dataset to Kaggle successfully: [Version 1](https://www.kaggle.com/datasets/siddharthchaini/snwise-spectra) ([PUBLIC URL](https://www.kaggle.com/datasets/d07a362cc11e1dc441a7ae52fc0e6650c9a78ead744a62d993b512b156a98dcb/))
        > To download, use kagglehub with: `"siddharthchaini/snwise-spectra"`
