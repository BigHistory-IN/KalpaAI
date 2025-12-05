Tutorial 3: Mapping Deforestation in South Andaman Island Using Vyom
=======================================================================
Tutorial by

**Sourabh Motiani¹**, **Utpal Singh²**, **Satyam Pratap Singh²** 

¹ Department of Earth Sciences, Indian Institute of Technology Roorkee

² School of Geosciences, University of Sydney 
 

-------------------------------------------------

This tutorial demonstrates how to **map deforestation** in the **South Andaman region** using **Kalpa**. We will use the **vyom plugin** to calculate the **Normalized Difference Vegetation Index (NDVI)** from satellite data.

Workflow
--------

Step 1: Create a Bounding Box
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Start by creating a bounding box of the region.

1. Navigate to **Tools → Vector → Bounding Box**.  

      .. image:: /_static/images/TutAnd_3_1.png
            :alt: Please refresh the page or check your internet connection.
            :align: center

2. Set the X and Y range for the South Andaman region.

Step 2: Download Satellite Data and Calculate NDVI Using Vyom
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Navigate to **Plugins → Vyom → Satellite Indices**.

      .. image:: /_static/images/TutAnd_3_2.png
            :alt: Please refresh the page or check your internet connection.
            :align: center

2. Select the satellite and enter the time period for which data is required. 

      .. image:: /_static/images/TutAnd_3_3.png
            :alt: Please refresh the page or check your internet connection.
            :align: center
 
3. Select the resolution and maximum percentage of cloud cover for the data to be downloaded.  
4. Click **Next**.

      .. image:: /_static/images/TutAnd_3_4.png
            :alt: Please refresh the page or check your internet connection.
            :align: center

5. Choose from the available dates within the selected time period and select the **NDVI index**.  
6. Click **Calculate**.

      .. image:: /_static/images/TutAnd_3_5.png
            :alt: Please refresh the page or check your internet connection.
            :align: center

7. Visualize and save the NDVI raster for the year 2025.  

      .. image:: /_static/images/TutAnd_3_6.png
            :alt: Please refresh the page or check your internet connection.
            :align: center

      .. image:: /_static/images/TutAnd_3_7.png
            :alt: Please refresh the page or check your internet connection.
            :align: center

8. Repeat the process to calculate the NDVI for the year 2018.

      .. image:: /_static/images/TutAnd_3_8.png
            :alt: Please refresh the page or check your internet connection.
            :align: center

      .. image:: /_static/images/TutAnd_3_9.png
            :alt: Please refresh the page or check your internet connection.
            :align: center

9. Visualize and save the NDVI raster for the year 2018.  

      .. image:: /_static/images/TutAnd_3_10.png
            :alt: NDVI Visualization 2018
            :align: center

      .. image:: /_static/images/TutAnd_3_11.png
            :alt: Please refresh the page or check your internet connection.
            :align: center


Step 3: Change Detection
~~~~~~~~~~~~~~~~~~~~~~~~~

Compare the two NDVI layers to identify regions of vegetation loss.  

    .. image:: /_static/images/TutAnd_3_12.png
        :alt: Please refresh the page or check your internet connection.
        :align: center
