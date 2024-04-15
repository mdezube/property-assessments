**Author**: [Mike Dezube](https://www.linkedin.com/in/mikedezube/) on behalf of [Charles River Data](https://www.charlesriverdata.com/)
**Contact**: inquiries@charlesriverdata.com


# Read Me

Supports the [ODSC Talk/Workshop Unlocking Insights in Home Values: A Multimillion-Row Journey with Polars](https://odsc.com/speakers/unlocking-insights-in-home-values-a-multimillion-row-journey-with-polars/) and the associated [article on Medium](https://medium.com/@odsc/harnessing-the-power-of-gis-and-python-for-property-value-analysis-at-scale-24266ba8c02a). If you intend the dive in straight into the python notebook, you can open `polars-gis-demo.ipynb`

# Overview

Following the sections below, you'll be able to install all dependencies and download all requisite files needed to follow along with the workshop described in the medium article [Harnessing the Power of GIS and Python for Property Value Analysis at Scale](https://odsc.medium.com/harnessing-the-power-of-gis-and-python-for-property-value-analysis-at-scale-24266ba8c02a)

<div style="width:100%; text-align:center">
  <img src="screenshots/Avg%20Home%20Value%20by%20Town.png" alt="Average Home Value by Town in Massachusetts" style="max-height:600px; margin:auto"/>
  <p style="font-weight:bold">Average Home Value by Town in Massachusetts</p>
</div>

<hr/>

# Setting Up Your Environment

  1. Follow the [Installation](#installation) steps below to get your environment set up.
  2. Download the data following the instructions in [Data Sources](#data-sources)
  3. Update variables in the notebook to point to your new files (you'll see instructions in the 2nd cell of the notebook)
  4. The notebook `polars-gis-demo.ipynb` should now run in full, give it a shot!

## Environment and dependencies

Using the commands below, you can set up a new conda environment to hold your python dependencies named `geo_explorer`, and get it registered for use in jupyter-lab.  Don't have conda yet?  Download it [here](https://www.anaconda.com/download).  Once installed, pop open terminal (or the equivalent on Windows, there are a number of options) and follow along below.

Conda can sometimes be slow to resolve dependencies, so at Charles River Data we like to use the [libmamba solver](https://www.anaconda.com/blog/a-faster-conda-for-a-growing-community) for ~10X speed boost.
```
# Not required (but recommended) for today's demo, install a much better solver
# for Conda’s base to keep insallations running quickly:
conda update -n base conda
conda install -n base conda-libmamba-solver
conda config --set solver libmamba
```

```
# Create a new conda environment and activate it.
conda create -n geo_explorer python=3.11
conda activate geo_explorer

# Install the dependencies you'll need to work with this data.
conda install geopandas jupyter pyogrio itables pyarrow seaborn plotly polars --channel conda-forge
pip install jupyter-black

# Register the new conda environment with jupyter.
python -m ipykernel install --user --name=geo_explorer
```

## Data sources

All data comes from the [Massachusetts Government Tax Assessments](https://www.mass.gov/info-details/massgis-data-property-tax-parcels)
 * **Home Values as a CSV** The gov't site above only provides the assessment data embedded within GIS files (`.shp` and `.gdb`) as such I'm making available a [.csv extract of parcel data](https://drive.google.com/file/d/1h8sZ3U2nmurJ5BxfngAdhQfb0U13ladB/view?usp=drive_link) (as of 2023) via Google Drive created via `ogr2ogr`.  This file format is easy to work with, and most of the notebook leverages it.
 * **Diving deeper with GIS**: Later parts of the notebook get into GIS analysis and thus need property and town boundary definitions along with the assessments
   * The full file of parcel boundaries can be downloaded directly from mass.gov at https://www.mass.gov/forms/massgis-request-statewide-parcel-data it's best to download it here so the gov't knows it gets heavy usage and supports it, but if you run into any issues I'm providing direct links as well:
     * [Parcels as .gdb](https://drive.google.com/file/d/1_NTjM6hAY7k68-jd8qVsP9sSkvZii4wc/view?usp=drive_link), used in this notebook for town boundaries.  Property boundaries are corrupted in this distribution.
     * [Eastern parcels as .shp](https://drive.google.com/file/d/1KaGz7oj_26Twn9Cf80SCciUcoHGUqCZ6/view?usp=drive_link) Property boundaries of Eastern MA, used in the notebook.
     * [Western parcels as .shp](https://drive.google.com/file/d/17QIKohh91XW43-Y0msS2V-yjmO-z1VyG/view?usp=drive_link) Property boundaries of Western MA, not used in the notebook, but good to have.
  
  **Technical note**
  The notebook as written requires the `.shp` file and the `.gdb` files.  In theory only one is needed, but due to a corrpution in the `L3_TAXPAR_POLY` layer in `.gdb` directly from the gov't we can't use it.


## (Optional) Related Files

To fully grasp the nuances of this data and enrich your analysis, consider exploring these supplementary files

1. [Property Type Classification Codes](https://www.mass.gov/files/documents/2016/08/wr/classificationcodebook.pdf) also included in this repo.  Includes a breakdown of codes defining property types (residential, multifamily, agriculture, apartments, etc.). Understanding these codes is essential for interpreting our data's "use codes."
2. [MassGIS standard for digital parcels and related data sets](https://www.mass.gov/info-details/massgis-standard-for-digital-parcels-and-related-data-sets) also included in this repo.  This documentation offers a detailed explanation of the dataset columns and fields, thus providing deeper insights into the geographical data.