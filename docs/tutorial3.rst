Tutorial 3: Creating Mineral Index Maps using Kalpa
====================================================

This tutorial demonstrates how to create mineral index maps using Kalpa. We will calculate specific mineral indices such as the Green Normalized Difference Vegetation Index (GNDVI) and the Ferrous Silicate Index using satellite data.

Dataset Overview
----------------

For this task, we use:
- LANDSAT8 Bands: Multispectral bands (1 to 11) as NetCDF files.

Accessing the Dataset
---------------------

The tutorial dataset is available here.

Workflow
--------

Step 1: Load Raster Files
^^^^^^^^^^^^^^^^^^^^^^^^^

Start by loading the required raster datasets:
- All LANDSAT8 bands (Band 1 to Band 11).

Step 2: Define a Region of Interest (ROI)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Create a bounding box to define the study area:
- Generate a bounding box using the LANDSAT8 bands.
- Save the bounding box as **bounding_box.gpkg**.

    .. image:: /_static/images/tut3_01.png
        :alt: Welcome Window
        :align: center

Step 3: Sample Raster Data
^^^^^^^^^^^^^^^^^^^^^^^^^^

Sample the raster data within the defined ROI:
- Sample at a regular grid interval.
- Save the sampled dataset as **sampled_bands.gpkg**.

Step 4: Compute Mineral Indices
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Green Normalized Difference Vegetation Index (GNDVI):
- Formula: (Band5 - Band3) / (Band5 + Band3)
- Use the vector calculator in Kalpa to compute the GNDVI.
- Save the result as **GNDVI_calculated.gpkg**.


    .. image:: /_static/images/tut3_02.png
        :alt: Welcome Window
        :align: center


Step 5: Visualize Results
^^^^^^^^^^^^^^^^^^^^^^^^^

- Open the calculated index layers in Kalpa.
- Adjust the color maps to enhance visualization.
- Analyze the spatial distribution of mineral indices.

    .. image:: /_static/images/tut3_03.png
        :alt: Welcome Window
        :align: center


    .. image:: /_static/images/tut3_04.png
        :alt: Welcome Window
        :align: center


Ferrous Silicate Index:
- Formula: Band7 / Band6
- Use the vector calculator in Kalpa to compute the Ferrous Silicate Index.
- Save the result as **Ferrous_Silicate_calculated.gpkg**.

Visualize Results
^^^^^^^^^^^^^^^^^^^^^^^^^


    .. image:: /_static/images/tut3_05.png
        :alt: Welcome Window
        :align: center


    .. image:: /_static/images/tut3_06.png
        :alt: Welcome Window
        :align: center



Enjoy!!!