Tutorial 2: Simple Mineral Prospectivity Maps with Kalpa
========================================================

In this tutorial, we will use **Kalpa** to build a **mineral prospectivity map**.  
The process utilizes three types of datasets:  

- **Geophysical data** (e.g., Bouguer Gravity Anomaly, Magnetic Anomaly)  
- **Geological data** (e.g., geological age, folds, faults, lineaments)  
- **Satellite data** (e.g., ASTER, SRTM, and LANDSAT)  

The goal is to create **prospectivity maps for copper deposits** based on the known occurrences of **96 mineral deposits** in the study region.  

We will sample various datasets at the locations of **known copper occurrences**, create an **unlabeled dataset** for contrast, and use **Random Forest (RF)** classifier and regressor to label and map prospectivity.

Dataset Overview
----------------

**Dataset can be downloaded here** *[insert dataset link]*  

Geophysical Data:
~~~~~~~~~~~~~~~~~

- **Gravity Data**:
  - Observed Gravity
  - Theoretical Gravity
  - Bouguer Anomaly
  - Upward Continued Bouguer Anomaly
  - Directional Derivatives of Bouguer Anomaly

- **Magnetic Data**:
  - Observed Magnetism
  - IGRF
  - Magnetic Anomaly
  - Upward Continued Magnetic Anomaly
  - Directional Derivatives of Magnetic Anomaly

Geological Data:
~~~~~~~~~~~~~~~~

- Tectonic Age  
- Folds  
- Faults  
- Lineaments  

Satellite Data:
~~~~~~~~~~~~~~~

- **LANDSAT8 Bands**:
  - Multispectral bands (3 to 8) as NetCDF files  
- **SRTM Elevation Data**:
  - Elevation from Shuttle Radar Topography Mission (SRTM)  
- **ASTER Data**:
  - Multispectral bands (1 to 14) as NetCDF files  

Mineral Occurrences:
~~~~~~~~~~~~~~~~~~~~

The dataset includes **96 known mineral deposits**, focusing on **copper deposits** for this tutorial.

Workflow
--------

Step 1: Loading Data and Visualization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Start Kalpa and choose **Cartesian coordinates** as the working system.  
2. Create a folder named **"MineralProspectivity"** to organize data and outputs.  
3. Import raster data:  
   - Go to **File → Import → Raster** and load:
     - SatelliteData/SRTM/SRTM_Raj_India.nc
     - SatelliteData/ASTER/Band_1_ASTER.nc to Band_14_ASTER.nc
     - SatelliteData/LANDSAT/Band_3_LANDSAT.nc to Band_8_LANDSAT.nc  
   - Adjust **colormap (cmap)** and ranges as needed.  
4. Import vector data:  
   - Go to **File → Import → Vector** and load:
     - ShapeFiles/Fault_Tectonic.shp
     - ShapeFiles/Fold_Tectonic.shp
     - ShapeFiles/Lineament_Tectonic.shp
     - ShapeFiles/Tectonic_Framework.shp
     - GeophysicalData/Gravity.shp
     - GeophysicalData/Magnetic.shp
     - Deposits/Deposits.shp  
5. Customize visualization:
   - Adjust **color and width** of faults, folds, and lineaments.
   - Apply **AGE** column and colormap to Tectonic_Framework.
   - Set **BOUGUER_AN** and **MAGNETIC_A** with diverging colormaps and ranges.
   - Increase **Deposit points** size for clarity.

Step 2: Processing and Filtering Data
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. **Filter out NaN values**:  
   - Go to **Data Processing → Vector → Filtering**.  
   - For Gravity: `pd.notna(row['BOUGUER_AN'])` → save as **gravity_filtered.gpkg**.  
   - For Magnetic: `pd.notna(row['MAGNETIC_A'])`.  
2. **Filter copper deposits**:  
   - Condition: `'Cu' in row['MINERAL_OR']`.

Step 3: Extract Data at Known Occurrences
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. **Sample data**:
   - Go to **Data Processing → Data Sampling**.  
   - Use **Deposits.shp** as AOI.  
   - Sample layers/columns:
     - Gravity: Observed_G, Theoretical_G, BOUGUER_AN  
     - Magnetic: Observed_M, IGRF, MAGNETIC_A  
     - Folds, Faults, Lineaments: generate distance columns (column_name_cdist).  
   - Add a **LABEL column = 1** using Vector Calculator.  
   - Save as **Sampled_Deposit_with_Label**.

Step 4: Create Unlabeled Data
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. **Generate bounding box and random points**:  
   - Use **Bounding Box utility** to define study area.  
   - Generate random points within the box and sample data as in Step 3.  
2. **Filter points by distance**:
   - Filter condition: `row['BOUGUER_AN_cdist'] < 0.01`.  
   - Assign **LABEL = 0**.  
   - Save as **Sampled_Unlabelled_Points**.

Step 5: Build Random Forest Classifier
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. **Prepare training data**:  
   - Merge **Sampled_Deposit_with_Label** and **Sampled_Unlabelled_Points** → **PU_Data**.  
2. **Train RF classifier**:  
   - Go to **Models → Random Forest Classifier → Create New Model**.  
   - Input dataset: **PU_Data.gpkg**, target: **LABEL**.  
   - Select all features, set RF parameters.  
   - Train and save model.

Step 6: Filter Negative Samples
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. **Predict labels**:  
   - Apply trained RF model to **PU_Data.gpkg** → save as **PU_Prediction.gpkg**.  
2. **Filter negatives**:
   - Condition: `row['Predicted_LABEL'] < 0.05`.  
   - Assign **LABEL_Pros = -1**, save as **Negative_Sample_with_Label**.

Step 7: Build Prospectivity Model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. **Merge training data**:
   - Combine positive and negative samples → **Prospectivity_Training_Data**.  
2. **Train RF regressor**:  
   - Input: **Prospectivity_Training_Data**, target: **LABEL_Pros**.  
   - Train model and save as **Prospector**.

Step 8: Generate Prospectivity Map
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. **Prepare data**:
   - Create grid, sample data (as in Step 3) → save as **AOI_whole_region**.  
2. **Predict prospectivity**:
   - Apply **Prospector model** to **AOI_whole_region.gpkg**.  
   - Save as **Prospectivity_Maps**.  
3. **Visualize**:
   - Display column **Predicted_LABEL_Pros** to show prospectivity map.