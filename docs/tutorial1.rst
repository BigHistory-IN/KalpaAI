Tutorial 1: Classifying Lithology Types in the Ladakh Region Using Kalpa
=======================================================================

This tutorial demonstrates how to **classify lithology types** in the **Ladakh region** using **Kalpa**.  
We will employ a **supervised machine learning** method, **Random Forest**, to train a model using **satellite data** and known lithology types.  
Once trained, this model will be used to **predict lithology across the entire region**.  

Dataset Overview
----------------

For this classification task, we use:  

- **LANDSAT8 Bands**: Multispectral bands (1 to 8) as NetCDF files.  
- **SRTM Elevation Data**: Elevation values from the Shuttle Radar Topography Mission (SRTM).  

**Accessing the Dataset**
The tutorial dataset is available *[provide link here]*.  

Workflow
--------

Step 1: Load Raster Files
~~~~~~~~~~~~~~~~~~~~~~~~~

Start by loading the required raster datasets:  

- All **LANDSAT8 bands** (Band 1 to Band 8).  
- **SRTM Elevation** data.  

    .. image:: /_static/images/tut1_01.png
        :alt: Welcome Window
        :align: center

To save on RAM storage unsee the bands

    .. image:: /_static/images/tut1_02.png
        :alt: Welcome Window
        :align: center

Step 2: Load and Merge Label Files
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Next, load the shapefiles containing **known lithology types**.  
These shapefiles represent **17 lithology classes**, stored in the **CLASS_NAME** column:  

- Alluvium  
- Chert Jasper Metasediments  
- Dunite  
- Fluvial Channel  
- Gabbro  
- Ice  
- Indus Formation  
- Kargil Formation  
- Ladakh Plutonic Complex  
- Lake  
- Lian  
- Pyroxenite  
- Serpentinized Peridotite  
- Tso Morari Complex  
- Volcanics  
- Water  
- Zildat Ophiolite Melange  

    .. image:: /_static/images/tut1_03.png
        :alt: Welcome Window
        :align: center

**Merge** these shapefiles into a single **GeoPackage file** named **All_Classes.gpkg** using the **"Merge Vector"** functionality in Kalpa.  

    .. image:: /_static/images/tut1_04.png
        :alt: Welcome Window
        :align: center

    .. image:: /_static/images/tut1_05.png
        :alt: Welcome Window
        :align: center

These datasets are written in Row format, for a different dataset written columnwise, use column

After merging the data you may remove the individual layers classes since all are merged in all_classes.gpkg

    .. image:: /_static/images/tut1_06.png
        :alt: Welcome Window
        :align: center

Step 3: Sample Training Data
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Randomly **sample the raster data** (LANDSAT8 bands, SRTM Elevation) and **lithology classes** (CLASS_NAME) to create a **training dataset**:  

- Select **100,000 data points**.  
- Save the resulting file as **Training_Dataset.gpkg**. 

    .. image:: /_static/images/tut1_07.png
        :alt: Welcome Window
        :align: center

Hit create, this may take few time depending on system specifications. Save the dataset as training_dataset.gpkg

Step 4: Build a Random Forest Classifier
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

What is Random Forest?
^^^^^^^^^^^^^^^^^^^^^^

**Random Forest** is an **ensemble learning method** that constructs **multiple decision trees** during training and outputs the **mode of the classes** for classification tasks.  
It is **robust**, handles **high-dimensional data** well, and is **resistant to overfitting**.  

Key Parameters:
^^^^^^^^^^^^^^^

- **n_estimators**: Number of trees in the forest (e.g., 100).  
- **criterion**: Function to measure split quality (e.g., `"gini"` for Gini impurity).  
- **max_depth**: Maximum depth of a tree (`None` allows full growth).  
- **min_samples_split**: Minimum samples required to split a node.  
- **min_samples_leaf**: Minimum samples required at a leaf node.  
- **max_features**: Number of features to consider for the best split (e.g., `"sqrt"`).  
- **bootstrap**: Whether bootstrap samples are used to build trees (True/False).  

Training the Model:
^^^^^^^^^^^^^^^^^^^

1. Navigate to **Model → Random Forest Classifier → Create New Model**.  
2. Load **Training_Dataset.gpkg**.  
3. Set the **training features** (Band1 to Band8, SRTM Elevation).  
4. Set the **target feature** (CLASS_NAME).  
5. Configure the **Random Forest parameters** as needed.  
6. **Train the model** and **save it** for future use.  

    .. image:: /_static/images/tut1_08.png
        :alt: Welcome Window
        :align: center

Hit start training after chosing your parameters. For simplicity in this tutorial we are proceeding with default values

    .. image:: /_static/images/tut1_09.png
        :alt: Welcome Window
        :align: center

After training save model as Model. This will create a folder named Model in the project directory

    .. image:: /_static/images/tut1_10.png
        :alt: Welcome Window
        :align: center


Step 5: Predict Lithology for the Entire Region
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Step 5.1: Prepare the Prediction Dataset
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Define the **area of interest/region of interest** using a **bounding box** or a **shapefile**.  For this tutorial, we are training for the entire region, so we make the shapefile/ROI for the entire region

    .. image:: /_static/images/tut1_11.png
        :alt: Welcome Window
        :align: center

You may chose any of the bands to extract the region in this tutorial, since they all represent the same region

    .. image:: /_static/images/tut1_12.png
        :alt: Welcome Window
        :align: center

Click create after chosing the bands and save as bounding_box.gpkg


2. **Sample raster data** at **regular grid intervals**. Exclude picking any classes since it will be predicted later using ML models. Select AOI as bounding_box which was produced earlier. Define resolution you want in degrees, not in m or km. For eg. 0.05 degree is approx 0.001km or 10m

    .. image:: /_static/images/tut1_13.png
        :alt: Welcome Window
        :align: center

Hit create. This will take a few moment, and save the sampled dataset as predition_dataset.gpkg

3. Save the sampled dataset as **Prediction_Dataset.gpkg**.  

Step 5.2: Perform Prediction
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Navigate to **Models → Random Forest Classifier → Existing Model**.  
2. **Load** the trained model.  

    .. image:: /_static/images/tut1_14.png
        :alt: Welcome Window
        :align: center

3. Select **Prediction_Dataset.gpkg** for prediction.  

    .. image:: /_static/images/tut1_15.png
        :alt: Welcome Window
        :align: center

Click Predict and save as predicted_dataset.gpkg

4. **Save** and **visualize** the **predicted lithology layer**.  

Navigate to Predicted_CLASS_NAME from the predicted_dataset layer

    .. image:: /_static/images/tut1_16.png
        :alt: Welcome Window
        :align: center

Enjoy!!!

    .. image:: /_static/images/tut1_17.png
        :alt: Welcome Window
        :align: center
