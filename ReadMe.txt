ReadMe for DATA 602 AGN project Github repo
Here, we'll explain the structure of code we upload and datasets we'll produce

DATA
train_dataset.csv
test_dataset.csv

CODE
MLProjectDataCuration.ipynb

DATA EXPLANATION

train_dataset.csv

This dataset contains the primary data we will use to train and test our machine learning models.  
It has 2,570 confirmed AGN (from XXL and MaNGA), and 2,568 non-AGN from MPA-JHU (all features from SDSS).
The primary target column of this data is 'is_AGN'.  This target is a binary, categorial variable, 0=non-AGN, 1=AGN.
The column 'which_AGN' is similar to 'is_AGN', and may be a secondary target variable (ignore this for now).  It similarly denotes if a galaxy is an AGN, but further clarifies which electromagnetic band was used to confirm it.
There are a few identification columns which should be excluded from any ML modeling: ext_ID, objID, specObjID.


There are two primary types of features: color magnitudes and emission line flux ratios:

Color magnitudes, such as u_mag (SDSS optical) or w1mpro (WISE infrared), denote the magnitude of brightness a galaxy exhibits in a particular band of light.
These magnitudes are often subtracted to quantify how 'blue' or 'red' a galaxy is, i.e. u-r, w1-w2.

Emission line flux ratios quantify the relative strength of a galaxy's emission at wavelengths corresponding to important emission lines.
These are denoted as o3_hB, which represents log10(oiii_flux / h_beta_flux).

Redshift is an additional feature which does not fall into either of the previous catagories, but it important nonetheless.
It quantifies the degree to which a galaxy's spectrum has been shifted due to the Universe's expansion.  It is an analog to radial distance from the Earth (for cosmological sources, like distant galaxies)


Columns are as follows:

Name:    | dtype  | feature/target | Description

ext_ID   | str    | n/a            | external catalogue ID.  For XXL, this is XXL_ID.  For MaNGA, MANGAID.  For non AGN, this is either 'quiescent' or 'starforming'.
objID    | str    | n/a            | SDSS photometric object ID
z        | float  | feature        | Redshift
u_mag    | float  | feature        | SDSS U-band magnitude
g_mag    | float  | feature        | SDSS G-band magnitude
r_mag    | float  | feature        | SDSS R-band magnitude
i_mag    | float  | feature        | SDSS I-band magnitude
z_mag    | float  | feature        | SDSS Z-band magnitude
w1mpro   | float  | feature        | WISE w1-band magnitude
w2mpro   | float  | feature        | WISE w2-band magnitude
w3mpro   | float  | feature        | WISE w3-band magnitude
w4mpro   | float  | feature        | WISE w4-band magnitude
u-g      | float  | feature        | SDSS u-g color
u-r      | float  | feature        | SDSS u-r color
u-i      | float  | feature        | SDSS u-i color
u-z      | float  | feature        | SDSS u-z color
g-r      | float  | feature        | SDSS g-r color
g-i      | float  | feature        | SDSS g-i color
g-z      | float  | feature        | SDSS g-z color
r-i      | float  | feature        | SDSS r-i color
r-z      | float  | feature        | SDSS r-z color
i-z      | float  | feature        | SDSS i-z color
w1-w2    | float  | feature        | WISE w1-w2 color
w1-w3    | float  | feature        | WISE w1-w3 color
w1-w4    | float  | feature        | WISE w1-w4 color
w2-w3    | float  | feature        | WISE w2-w3 color
w2-w4    | float  | feature        | WISE w2-w4 color
w3-w4    | float  | feature        | WISE w3-w4 color
o3_hB    | float  | feature        | oiii / h beta emission line flux ratio
n2_hA    | float  | feature        | nii / h alpha emission line flux ratio
s2_hA    | float  | feature        | sii / h alpha emission line flux ratio
n2_hA    | float  | feature        | nii / h alpha emission line flux ratio
o1_hA    | float  | feature        | oi / h alpha emission line flux ratio
o3_o2    | float  | feature        | oiii / oii emission line flux ratio
ne3_o2   | float  | feature        | Neiii / oii emission line flux ratio
is_AGN   | float  | target         | AGN indicator: 0=non AGN, 1=AGN
which_AGN| float  | target         | binary variable indicating which band an AGN was detected in: 0=non AGN, 1=radio, 2=infrared, 4=optical, 8=x-ray (can be combined to indicate multiple bands)


test_dataset.csv

This dataset is composed of 42,814 galaxies selected from SDSS to have good data quality.
This dataset will be relevant once we have trained various models on train_dataset.csv and selected the best performing models.
The models will be applied to this dataset to see how many galaxies are classified as AGN vs non AGN.  
This classification will be cross referenced against the SDSS DR12 quasar catalog to see evaluate performance and potential for novel AGN discoveries.

The dataset possesses the exact same columns as train_dataset.csv, except is_AGN and which_AGN.




CODE EXPLANATION

MLProjectDataCuration

This jupyter notebook contains the workflow for curating the test and train datasets.
It is not necessarily a "curate all in one place", notebook, as many SQL queries also went into the data curation; however, it is able to read in the raw csv files, compute features, and print out ready-to-use test and train datasets.








