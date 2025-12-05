Tutorial 4: Monitoring Crop Health in Wimmera, Victoria with Sentinel-2 and NDVI
====================================================
Tutorial by

**Utpal Singh¹**, **Satyam Pratap Singh¹**, **Sourabh Motiani²** 

¹ School of Geosciences, University of Sydney

² Department of Earth Sciences, Indian Institute of Technology Roorkee

------------------------------------------------

This tutorial demonstrates how to **monitor crop health** in the **Wimmera region of Victoria** using **Kalpa**. We will use the **vyom plugin** to download satellite data and use kalpa's Data Sampling and Vector Calculator to compute the **Normalized Difference Vegetation Index (NDVI)** from satellite data.

Dataset Overview
----------------

For this task, we use:
Sentinel-2 Bands: Multispectral bands (4 and 8) for the duration of April to August for year 2023 and 2024.

Workflow
--------

Step 1: Create a Bounding Box
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Start by creating a bounding box of the region.

1. Navigate to **Tools → Vector → Bounding Box**.  

      .. image:: /_static/images/Tut_4_1.png
            :alt: Please refresh the page or check your internet connection.
            :align: center

2. Set the X and Y range for the Wimmera region in Victoria.


Step 2: Download Satellite Data Using Vyom
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Navigate to **Plugins → Vyom → Download Satellite Data**.

      .. image:: /_static/images/Tut_4_2.png
            :alt: Please refresh the page or check your internet connection.
            :align: center

2. Select the satellite and enter the time period for which data is required. 
3. Select the resolution and maximum percentage of cloud cover for the data to be downloaded. 

      .. image:: /_static/images/Tut_4_3.png
            :alt: Please refresh the page or check your internet connection.
            :align: center
  
4. Click **Next**.
5. Choose from the available dates within the selected time period and select **B04** and **B08**.

      .. image:: /_static/images/Tut_4_4.png
            :alt: Please refresh the page or check your internet connection.
            :align: center

6. Click **Download**.

      .. image:: /_static/images/Tut_4_5.png
            :alt: Please refresh the page or check your internet connection.
            :align: center

7. Visualize and save the satellite data.  

      .. image:: /_static/images/Tut_4_6.png
            :alt: Please refresh the page or check your internet connection.
            :align: center

8. Repeat the process to download the satellite data for other months of 2023 and 2024.

      .. image:: /_static/images/Tut_4_7.png
            :alt: Please refresh the page or check your internet connection.
            :align: center

Step 3: Calculate NDVI
~~~~~~~~~~~~~~~~~~~~~~~     

1. Navigate to **Tools → Data Sampling**.
2. AOI (Area of Interest): **Bounding Box**.
3. Select the downloaded Sentinel-2 bands (B04 and B08) for all dates of 2023 and 2024.
4. Select **Regular** sampling method with same resolution as the satellite data.
5. Click **Create**.

      .. image:: /_static/images/Tut_4_8.png
            :alt: Please refresh the page or check your internet connection.
            :align: center

6. save as ``processed_dataset.gpkg``.

        .. image:: /_static/images/Tut_4_9.png
                :alt: Please refresh the page or check your internet connection.
                :align: center

7. Navigate to **Tools → Vector → Vector Calculator**.
8. Select the ``processed_dataset.gpkg`` layer.
9. In the expression box, enter the NDVI formula with the respective band names.
10. Click **Apply** and save as ``NDVI_2023_04_2018_calculated.gpkg``.

      .. image:: /_static/images/Tut_4_10.png
            :alt: Please refresh the page or check your internet connection.
            :align: center

      .. image:: /_static/images/Tut_4_11.png
            :alt: Please refresh the page or check your internet connection.
            :align: center

11. Repeat the process to calculate NDVI for other months in 2023 and 2024.

      .. image:: /_static/images/Tut_4_12.png
            :alt: Please refresh the page or check your internet connection.
            :align: center

- **Note**: The same process of calculating NDVI can also be performed using Vyom's Satellite Indices feature, but this workflow could be useful in case of calculating other satellite indices which are not available in Vyom's Satellite Indices feature. 

Step 4: Visualize NDVI Results
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Visualize the NDVI results for different months to monitor crop health.

      .. image:: /_static/images/Tut_4_fin.jpeg
            :alt: Please refresh the page or check your internet connection.
            :align: center
