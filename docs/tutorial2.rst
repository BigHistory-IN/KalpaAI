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
================

The dataset can be downloaded here.

Geophysical Data
----------------

**Gravity Data:**

- Observed Gravity
- Theoretical Gravity
- Bouguer Anomaly
- Upward Continued Bouguer Anomaly
- Directional Derivatives of Bouguer Anomaly

**Magnetic Data:**

- Observed Magnetism
- IGRF
- Magnetic Anomaly
- Upward Continued Magnetic Anomaly
- Directional Derivatives of Magnetic Anomaly

Geological Data
---------------

- Tectonic Age
- Folds
- Faults
- Lineaments

Satellite Data
--------------

**LANDSAT8 Bands:**

- Multispectral bands (3 to 8) as NetCDF files

**SRTM Elevation Data:**

- Elevation values from the Shuttle Radar Topography Mission (SRTM)

**ASTER Data:**

- Multispectral bands (1 to 14) as NetCDF files

**Mineral Occurrences:**

- The dataset includes 96 known occurrences of mineral deposits.  
  For this tutorial, we focus on copper deposits.

Workflow
========

Step 1: Loading Data and Visualization
--------------------------------------

1. Start Kalpa and choose Cartesian coordinates as the working coordinate system.
2. Create a new folder named ``MineralProspectivity`` to save the dataset, figures, etc.

**Import Vector Data:**

- Navigate to: ``File -> Import -> Vector``  
- Load the following files:
  
  - ``ShapeFiles/Fault_Tectonic.shp``
  - ``ShapeFiles/Fold_Tectonic.shp``
  - ``ShapeFiles/Lineament_Tectonic.shp``
  - ``ShapeFiles/Tectonic_Framework.shp``
  - ``Deposits/Deposits.shp``

- Adjust colormap, feature width, and range as needed.


    .. image:: /_static/images/tut2_01.png
        :alt: Welcome Window
        :align: center

**Import Raster Data:**

- Navigate to: ``File -> Import -> Raster``  
- Load the following files:

  - ``GeophysicalProcessed/Raster/BOUGUER_AN_Kriging.nc``
  - ``GeophysicalProcessed/Raster/MAGNETIC_A_Kriging.nc``
  - ``GeophysicalProcessed/Raster/Grad_Gravity/*``
  - ``GeophysicalProcessed/Raster/Grad_Magnetic/*``
  - ``GeophysicalProcessed/Raster/UC_Gravity/*``
  - ``GeophysicalProcessed/Raster/UC_Magnetic/*``
  - ``SatelliteData/SRTM/SRTM_Raj_India.nc``
  - ``SatelliteData/LANDSAT/Band_3_LANDSAT.nc`` to ``Band_8_LANDSAT.nc``


    .. image:: /_static/images/tut2_02.png
        :alt: Welcome Window
        :align: center



Step 2: Feature Generation
--------------------------

1. **Generate Positive Labels from Known Deposits:**

   - Go to: ``Plugins -> MPM -> Feature Generation``
   - AOI/ROI: ``Deposits``
   - Select all layers *except* Tectonic Framework and Deposits

   **Layer Config:**

   - **Euclidean Distance** for vectors:
     - Fault_Tectonic
     - Fold_Tectonic
     - Lineament_Tectonic

   - **Band Value** for rasters:
     - BOUGUER_AN_Kriging.nc
     - MAGNETIC_A_Kriging.nc
     - Grad_Gravity/*
     - Grad_Magnetic/*
     - UC_Gravity/*
     - UC_Magnetic/*

   - Sampling method: ``regular`` with 100 seed points


    .. image:: /_static/images/tut2_03.png
        :alt: Welcome Window
        :align: center


    .. image:: /_static/images/tut2_04.png
        :alt: Welcome Window
        :align: center



   - Click **Generate** → Save as: ``deposit_sampled.gpkg``


    .. image:: /_static/images/tut2_05.png
        :alt: Welcome Window
        :align: center



2. **Generate Label Column:**

   - Go to: ``Tools -> Vector Calculator``
   - Layer: ``deposit_sampled``
   - Condition: ``== 1``
   - New column: ``Label``
       .. image:: /_static/images/tut2_05.png
        :alt: Welcome Window
        :align: center
   - Click **Apply** → Save as: ``deposit_positive_label.gpkg``


    .. image:: /_static/images/tut2_07.png
        :alt: Welcome Window
        :align: center



3. **Create Bounding Box:**

   - From ``Create Bounding Box``, choose layer: ``BOUGUER_AN_Kriging``

    .. image:: /_static/images/tut2_08.png
        :alt: Welcome Window
        :align: center


   - Click **Create** → Save as: ``bounding_box.gpkg``

    .. image:: /_static/images/tut2_09.png
        :alt: Welcome Window
        :align: center



4. **Generate Unlabelled (Random) Features:**

   - AOI: ``bounding_box``
   - Method: ``Random``, 1000 seed points

   **Layer Config:**

   - **Euclidean Distance** for:
     - Fault_Tectonic
     - Fold_Tectonic
     - Lineament_Tectonic

   - **Band Value** for:
     - BOUGUER_AN_Kriging.nc
     - MAGNETIC_A_Kriging.nc
     - Grad_Gravity/*
     - Grad_Magnetic/*
     - UC_Gravity/*
     - UC_Magnetic/*

    .. image:: /_static/images/tut2_10.png
        :alt: Welcome Window
        :align: center
    .. image:: /_static/images/tut2_11.png
        :alt: Welcome Window
        :align: center
    .. image:: /_static/images/tut2_12.png
        :alt: Welcome Window
        :align: center

   - Click **Generate** → Save as: ``randomly_sampled.gpkg``

    .. image:: /_static/images/tut2_13.png
        :alt: Welcome Window
        :align: center
This workflow now generates randomly sampled data which in this workflow, the width is set to 1 for visualisation and positive samples as thicker dots with width 3

    .. image:: /_static/images/tut2_14.png
        :alt: Welcome Window
        :align: center

5. **Label Random Features as 0:**

   - Go to: ``Vector Calculator``
   - Layer: ``randomly_sampled``
   - Condition: ``== 0``
   - Column name: ``Label``
   - Save as: ``deposits_unlabelled.gpkg``

    .. image:: /_static/images/tut2_15.png
        :alt: Welcome Window
        :align: center

6. **Merge Positive and Unlabelled Datasets:**

   - Remove ``deposit_sampled`` and ``randomly_sampled`` layers (optional)
   - Go to: ``Merge Layers``
      .. image:: /_static/images/tut2_16.png
         :alt: Welcome Window
         :align: center

   - Merge: ``deposits_positive_label`` + ``deposits_unlabelled``
   - Save as: ``training_data.gpkg``
   - Visualization tip: Set positive samples (label = 1) with width 3, others with width 1

Now you can see that the positive (1) are in green color and unlabelled in brown. You may edit this in cmap

    .. image:: /_static/images/tut2_17.png
        :alt: Welcome Window
        :align: center


Step 3: Create PU Bagging Model
-------------------------------

1. Go to: ``Plugins -> MPM -> Models -> PU Bagging -> Create New Model``

      .. image:: /_static/images/tut2_18.png
         :alt: Welcome Window
         :align: center

2. Training data: ``training_data.gpkg``
      .. image:: /_static/images/tut2_19.png
         :alt: Welcome Window
         :align: center
3. (Optional) Generate correlation report to examine feature correlation
      .. image:: /_static/images/tut2_20.png
         :alt: Welcome Window
         :align: center

   Click close
4. Target feature: ``Label``
5. Select all other features as training features (except ``Label``)
      .. image:: /_static/images/tut2_21.png
         :alt: Welcome Window
         :align: center
      .. image:: /_static/images/tut2_22.png
         :alt: Welcome Window
         :align: center
6. Enable: ``scaled probabilities``
7. Click **Start Training**
8. Save model as: ``PU Model``
      .. image:: /_static/images/tut2_23.png
         :alt: Welcome Window
         :align: center
9. Go to: ``Plugins -> MPM -> Feature Generation -> Bounding Box``
      .. image:: /_static/images/tut2_24.png
         :alt: Welcome Window
         :align: center
      .. image:: /_static/images/tut2_25.png
         :alt: Welcome Window
         :align: center
10. Select all layers *except*:
    
    - Tectonic Framework  
    - Deposit  
    - deposits_positive_label  
    - bounding_box  
    - deposits_unlabelled  
    - training_data

      .. image:: /_static/images/tut2_26.png
         :alt: Welcome Window
         :align: center

11. Repeat selection of **Band Value** for rasters and **Euclidean Distance** for vectors
12. Set resolution to: ``0.005 degrees``. This may be of your choice
13. Click **Generate** → Save as: ``predicted_dataset.gpkg``. This may take a while depending on resolution and hardware specs.
      .. image:: /_static/images/tut2_27.png
         :alt: Welcome Window
         :align: center

      .. image:: /_static/images/tut2_28.png
         :alt: Welcome Window
         :align: center
      
14. Go to: ``Plugins -> MPM -> Models -> PU Bagging -> Existing Model``
15. Choose: ``predicted_dataset.gpkg`` as prediction input
      .. image:: /_static/images/tut2_29.png
         :alt: Welcome Window
         :align: center
16. Click **Predict**

**Voila!** You now have your PU Bagging prediction.
      .. image:: /_static/images/tut2_30.png
         :alt: Welcome Window
         :align: center

Final Step: Select a colormap of your choice for visualizing predictions.

      .. image:: /_static/images/tut2_30.png
         :alt: Welcome Window
         :align: center

      .. image:: /_static/images/tut2_31.png
         :alt: Welcome Window
         :align: center

      .. image:: /_static/images/tut2_32.png
         :alt: Welcome Window
         :align: center

