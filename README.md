## Point Data Extraction from the AI4SH Datacube

_Latest update: 7 December 2025_

### Overview
The Jupyter Notebook _Extract_AI4SH_datacube_points_, extracts static environmental values from the [AI4SoilHealth (AI4SH) Datacube](https://github.com/AI4SoilHealth/SoilHealthDataCube) for specified in-situ point locations. It reads coordinate points from an Excel file, samples raster layers hosted on the EcoDataCube S3 server, and exports the results to a CSV file.

### Purpose
The notebook enables researchers to:
- Load AI4SH in-situ coordinate points from an Excel file
- Convert point data to a GeoDataFrame with proper coordinate reference systems
- Extract values from multiple static raster values (terrain derivatives, crop types, etc.)
- Handle coordinate reprojection automatically when needed
- Save the enriched point data with extracted values

### Workflow
1. **Environment Setup**: Load required Python libraries
2. **Data Loading**: Read in-situ coordinate points from Excel file
3. **Spatial Data Preparation**: Convert points to GeoDataFrame with EPSG:4326 CRS
4. **Covariate Selection**: Define list of raster layer URLs from AI4SH Datacube
5. **Value Extraction**: Loop through each layer and sample values at point locations
6. **Data Export**: Save results to CSV file with all extracted values

### Python Package Requirements
The Notebook requires the following third party Python packages:
- pandas
- geopandas
- rasterio
- numpy
- openpyxl
- gdal
The terminal command for installing these packages with [Anaconda](https://www.anaconda.com) is:
```
conda create -n ai4sh_datacube_access_312 -c conda-forge  pandas geopandas rasterio numpy openpyxl gdal python=3.12
```

### Input Requirements
- **Excel file**: `AI4SH_in-situ_coordinate_points.xlsx` containing columns for `longitude` and `latitude`
- **Directory structure**: Excel file should be located in `../AI4SH_point_locations/` relative to notebook

### Output
- **CSV file**: `AI4SH_in-situ_points_with_static_values.csv` saved to `../AI4SH_point_data/`
- Contains original point data plus columns for each extracted value

### Data Sources
Static values are accessed from the [AI4SoilHealth SoilHealthDataCube](https://github.com/AI4SoilHealth/SoilHealthDataCube) via HTTPS, including:
- Terrain derivatives (slope, curvature, hillshade, TWI, etc.)
- Geomorphological features (geomorphons, openness indices)
- Topographic indices (LS-factor, shape index)
- Land cover/crop type data

### Dependencies
- Python 3.12
- pandas: Data manipulation and Excel/CSV I/O
- geopandas: Spatial data operations and coordinate transformations
- rasterio: Raster data reading and sampling
- numpy: Numerical operations and handling missing values
- openpyxl: Excel file reading support
- gdal: supports rasterio geo-data processing

### Notes
- The notebook handles coordinate reprojection automatically when raster CRS differs from point CRS
- NoData values are converted to NaN for proper handling in pandas
- Progress messages indicate which value is currently being processed
- Internet connection required to access remote raster data from S3 server

### Licenses
The data is provided under the following licenses:

- Data License: Creative Commons Attribution license (**CC-BY**)
- Code License: Massachusetts Institute of Technology License ()**MIT License**)

### Acknowledgments and Funding
This work is part of the AI4SoilHealth project, funded by the European Union's Horizon Europe Research and Innovation Programme under Grant Agreement No. 101086179.

_Funded by the European Union. The views expressed are those of the authors and do not necessarily reflect those of the European Union or the European Research Executive Agency._
