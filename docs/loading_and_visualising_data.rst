Loading and visualising data
============================
Kalpa is designed to handle and visualize various types of geospatial data. This chapter provides an overview of the supported data formats, loading instructions, and customization options to optimize your workflow.

----------------------------------------------------------------

Types of Geospatial Data
------------------------
Kalpa primarily supports two types of geospatial data:

1. Raster Data
----------------
Raster data represents information as a grid of values. Each pixel in the grid corresponds to a specific geographic location and contains a value representing a characteristic of that location (e.g., elevation, temperature, or satellite imagery).
•	Continuous Raster Data: Values vary smoothly across space (e.g., elevation or temperature).
•	Categorical Raster Data: Discrete values representing classes (e.g., land use or vegetation type).
Currently, Kalpa supports raster data in the NetCDF format with a single layer of data per file.

2. Vector Data
----------------
Vector data describes geographic features using geometries like points, lines, and polygons. Attributes are associated with these features, representing their characteristics (e.g., faults, subduction zones, geological features, roads, rivers).
•	Supported Formats: ESRI shapefiles (.shp) and GeoPackage (.gpkg).
•	Geometries Supported: Points, lines, polygons, and multipolygons.
•	Note: For large datasets with complex geometries, Kalpa may display simplified points for faster rendering. This does not alter the underlying data, which is used for processing and workflows.

----------------------------------------------------------------

Loading and Configuring Raster Data
-----------------------------------
Loading Raster Data
-------------------
1.	Navigate to File > Raster.
2.	Select one or more NetCDF files (hold Shift for multiple selections) and click Open.
3.	A Layer Window will appear, displaying the loaded layers.

    .. image:: /_static/images/loading_and_configuring_raster_data_1.png
        :alt: Welcome Window
        :align: center

4.	To visualise the legend. Click on the legend icon in the toolbar.

    .. image:: /_static/images/loading_and_configuring_raster_data_2.png
        :alt: Welcome Window
        :align: center

Managing Layers
---------------
•	Toggle the visibility of a layer using the eye icon next to the layer name.

Customizing Layer Properties
-----------------------------

1.	Click the colored rectangle next to the layer name in the Layer Window to open the settings.

    .. image:: /_static/images/loading_and_configuring_raster_data_3.png
        :alt: Welcome Window
        :align: center

2.	Configure the following properties:

    .. image:: /_static/images/loading_and_configuring_raster_data_4.png
        :alt: Welcome Window
        :align: center

*Color Maps (cmaps)*

•	Kalpa supports over 50 colormaps, including those from matplotlib and Crameri's scientific colormaps.
•	Example colormaps:
o	Sequential: 'viridis', 'plasma', 'magma', etc.
o	Diverging: 'coolwarm', 'seismic', etc.
o	Scientific: 'batlow', 'roma', 'berlin', etc.

*Data Range*
•	By default, the colormap range is set to the minimum and maximum values of the dataset.
•	You can manually specify the minimum and maximum values for better control over the visualization.


====================================
Loading and Configuring Vector Data
====================================

Loading Vector Data
-------------------

1. Navigate to **File > Vector**.
2. Select one or more ``.shp`` or ``.gpkg`` files (hold **Shift** for multiple selections) and click **Open**.
3. The **Layer Window** will display the loaded vector layers.

    .. image:: /_static/images/loading_and_configuring_raster_data_5.png
        :alt: Welcome Window
        :align: center

Managing Layers
---------------

- Toggle the visibility of a layer using the **eye icon** next to the layer name.

Customizing Layer Properties
----------------------------

1. Click the **colored rectangle** next to the layer name in the **Layer Window** to open the settings.
2. Configure the following properties:

    .. image:: /_static/images/loading_and_configuring_raster_data_6.png
        :alt: Welcome Window
        :align: center

Geometry Display
~~~~~~~~~~~~~~~~
- By default, geometries are displayed in a single color. Use the **color picker** to change the outline color.

    .. image:: /_static/images/loading_and_configuring_raster_data_7.png
        :alt: Welcome Window
        :align: center

Attribute-Based Coloring
~~~~~~~~~~~~~~~~~~~~~~~~
- Select a column from the vector data's **attribute table** to activate colormap-based visualization.
- Assign different colormaps or ranges to represent specific attributes.

Fill Options
~~~~~~~~~~~~
- Choose between filling the geometry outline with a single color or using a colormap.

    .. image:: /_static/images/loading_and_configuring_raster_data_8.png
        :alt: Welcome Window
        :align: center

Size and Opacity
~~~~~~~~~~~~~~~~
- Adjust the **size/width** and **opacity** of the geometries for better visualization.

Legends
~~~~~~~
- To visualize a **legend or label**, click on the **legend icon**.

Future Features
---------------

Time-Dependent Data
~~~~~~~~~~~~~~~~~~~
- **Raster and Vector Data**: Enhanced functionality for visualizing and analyzing time-dependent geospatial datasets.

Volume Raster Data
~~~~~~~~~~~~~~~~~~
- Support for volumetric raster data will be introduced, enabling **3D visualization of subsurface features**.

Time-Dependent Volume Raster
~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Upcoming versions will include the ability to handle **dynamic volumetric data**.


