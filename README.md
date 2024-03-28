**Author**: [Mike Dezube](https://www.linkedin.com/in/mikedezube/) on behalf of [Charles River Data](https://www.charlesriverdata.com/)
**Contact**: inquiries@charlesriverdata.com

# Overview

Following the sections below, you'll be able to install all dependencies and download all requisite files needed to follow along with the workshop described in the [Understanding and Exploring the Data](#understanding-and-exploring-the-data) section.

<div style="width:100%; text-align:center">
  <img src="screenshots/Avg%20Home%20Value%20by%20Town.png" alt="Average Home Value by Town in Massachusetts" style="max-height:600px; margin:auto"/>
  <p style="font-weight:bold">Average Home Value by Town in Massachusetts</p>
</div>

# Articles and Talks

In lieu of running the code, you can check out our [article on MA home prices](https://medium.com/@odsc/harnessing-the-power-of-gis-and-python-for-property-value-analysis-at-scale-24266ba8c02a) with a walkthrough and screenshots, or attend the [ODSC talk](https://odsc.com/speakers/unlocking-insights-in-home-values-a-multimillion-row-journey-with-polars/).


# Getting Started
  ### Start here if you're part of the ODSC workshop

  1. Follow the [Installation](#installation) steps below to get your environment set up.
  2. Download the data following the instructions in [Data Sources](#data-sources)
     * After downloading the CSV assessments, in the jupyter notebook `polars-gis-demo.ipynb` update the variable `MA_HOME_PRICES_CSV_PATH` and point it to the CSV.  Used for easy access to all tax assessments.
     * After downloading the GDB parcel boundaries update `PARCEL_BOUNDARIES_GDB` in the same notebook to point to this new file.  Used for town boundaries.
     * After downloading the SHP parcel boundaries update `PARCEL_BOUNDARIES_EAST_SHP` in the same notebook to point to this new file.  Used for property boundaries.

  3. The notebook `polars-gis-demo.ipynb` should now run in full, give it a shot!

# Installation

## Environment and dependencies

Using the commands below, you can set up a new conda environment named `geo_expolorer` install the dependencies, and get it registered for use in jupyter-lab.

```
conda create -n geo_explorer python=3.11
conda activate geo_explorer
conda install geopandas jupyter pyogrio itables pyarrow seaborn plotly polars --channel conda-forge
pip install jupyter-black
python -m ipykernel install --user --name=geo_explorer
```

Pro-tip, want conda installations to run at 10x? (not required for this workshop)
```
# Install a much better solver for Conda’s base to keep it running faster
conda update -n base conda
conda install -n base conda-libmamba-solver
conda config --set solver libmamba
```

## Data sources

All data comes from the [Massachusetts Government Tax Assessments](https://www.mass.gov/info-details/massgis-data-property-tax-parcels)
 * This site however only provides the assessment data embedded within GIS files (`.shp` and `.gdb`) as such I'm making available a [.csv extract of parcel data](https://drive.google.com/file/d/1h8sZ3U2nmurJ5BxfngAdhQfb0U13ladB/view?usp=drive_link) (as of 2023) via Google Drive created via `ogr2ogr`.  This file format is easy to work with, and most of the notebook leverages it.
 * Later parts of the notebook get into GIS analysis and thus need property and town boundary definitions along with the assessments
   * The full file of parcel boundaries can be downloaded directly from mass.gov at https://www.mass.gov/forms/massgis-request-statewide-parcel-data
   * The notebook as written requires the `.shp` file and the `.gdb` files.  In theory only one is needed, but due to a corrpution in the `L3_TAXPAR_POLY` layer in `.gdb` directly from the gov't we can't use it.
     * You'll notice the `.shp` file is split into Western and Eastern MA, you can download both, we'll just use Eastern for now though.


#### Related Files

These files aren't necessary to run the code, but will offer more context on the data.

1. [Property Type Classification Codes](https://www.mass.gov/files/documents/2016/08/wr/classificationcodebook.pdf) also included in this repo.  Necessary to understand `use codes` in the data e.g. residential, multifamily, agriculture, apartments, etc.
2. [MassGIS standard for digital parcels and related data sets](https://www.mass.gov/info-details/massgis-standard-for-digital-parcels-and-related-data-sets) also included in this repo.  Helpful to understand all of the columns and fields.



# Understanding and Exploring the Data

This repo supports the ODSC Talk/Workshop [Unlocking Insights in Home Values: A Multimillion-Row Journey with Polars](https://odsc.com/speakers/unlocking-insights-in-home-values-a-multimillion-row-journey-with-polars/), and the [written Medium article](https://medium.com/@odsc/harnessing-the-power-of-gis-and-python-for-property-value-analysis-at-scale-24266ba8c02a) so check those out for a nice walkthrough of this data.  Not required though, you can also dive on in by opening up `polars-gis-demo.ipynb`