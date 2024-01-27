# Property Value Analytics in Massachusetts: A Data Driven Exploration

This repo will be built up over time as an exploration demo is built out to be shared at Mass General Brigham, https://odsc.com/boston/ and to any other interested users.

**Data Source:** [Massachusetts Government Tax Assessments](https://www.mass.gov/info-details/massgis-data-property-tax-parcels)
 * This site however only provides the assessment data embedded within GIS files (.shp and .gdb) as such I'm making available a [.csv extract of parcel data](https://drive.google.com/file/d/1h8sZ3U2nmurJ5BxfngAdhQfb0U13ladB/view?usp=drive_link) (as of 2023) via Google Drive created via `ogr2ogr`.
 * The full file inclusive of parcel boundaries can be downloaded directly from mass.gov at https://www.mass.gov/forms/massgis-request-statewide-parcel-data
   * It is recommended to download the `.shp` as the `.gdb` file has some invalid geometries that cause issues in python loading.  The `.shp` file is sharded by East/West but just download both and we'll focus on East for now.
   * The code does include an example of using this file and visualizing parcel level data.

# Assessment Exploration

A v1 of this is complete and in the adjacent notebook, but it will continue to grow.

**Title:** Unlocking Insights in Home Values: A Multimillion-Row Journey with Polars

**Related Files**

1. [Property Type Classification Codes](https://www.mass.gov/files/documents/2016/08/wr/classificationcodebook.pdf) also included in this repo.  Necessary to understand `use codes` in the data e.g. residential, multifamily, agriculture, apartments, etc.
2. [MassGIS standard for digital parcels and related data sets](https://www.mass.gov/info-details/massgis-standard-for-digital-parcels-and-related-data-sets) also included in this repo.  Helpful to understand all of the columns and fields.

**Abstract:**

Hands-on data adventure exploring hidden insights and nuances across all home and building values in Massachusetts. With a dataset containing 2.5 million rows, this workshop will showcase the incredible capabilities of  Polars, a data manipulation library which partners well with Pandas, in handling extensive data with a clean API, high performance and a low memory footprint, all on your local machine.

Throughout the session, we'll demonstrate how Polars empowers users to perform nuanced analyses, such as pinpointing the most expensive homes in every town and on every street in Massachusetts, or unraveling the factors influencing home prices such as style, location, acreage, year built, square footage, etc.

Whether you're a data enthusiast, analyst, or someone intrigued by the power of data analysis, this interactive workshop will leave you equipped to harness Polars' full potential for your own data exploration endeavors.  Plus you’ll have a fun dataset of all home and building values (per tax assessment) at your fingertips. Time permitting, we’ll also do some GIS analysis on the dataset.  Don't miss this opportunity to discover the stories hidden within the numbers and elevate your data analysis skills to new heights.  Come prepared to write code in a jupyter notebook/jupyter lab, and leave with a working model and the full dataset.

# Screenshots

In lieu of running the code, you can see some select visuals of what it generates in [screenshots](screenshots/).
