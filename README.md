# Kalpa


Kalpa is a powerful and versatile software suite designed to cater to the needs of professionals in geology, GIS, and related fields. Leveraging advanced visualization and processing capabilities, Kalpa bridges the gap between geospatial data and actionable insights.

---

## Key Advantage

One of Kalpa's biggest advantages is that it is written in Python. This enables seamless integration of any Python script as a plugin, making it especially suitable for machine learning workflows and custom geospatial data processing tasks.

---

## Features

### **Project Management**
- **Project Creation**: Easily create and manage projects in a specific folder location to keep your work organized.

---

### **Data Visualization**

#### **Raster Data Visualization**
- **Supported Formats**: Visualize raster data from diverse sources, including:
  - Satellite Imagery: Sentinel-2, Landsat (5, 7, 8), ASTER, Hyperion, WorldView-3, AVIRIS, and HyMap.
  - UAV Data: UAV imagery for lithological and structural analysis.
  - Geophysical Models: Topography, crustal and lithospheric thickness, seismic tomography, Geodynamics models, etc.
- **Export Options**: Generate publication-ready figures in formats such as `.svg`, `.eps`, `.ps`, `.pdf`, `.tex`, `.png`, `.jpeg`, and `.jpg`.

#### **Vector Data Visualization**
- **Supported Formats**: Load and visualize vector data in shapefile and GPKG formats, including points, lines, and polygons.
- **Applications**: Geological maps, geochemical data, structural data, lithological maps, and more.

#### **Customization Options**
- **Raster Layers**:
  - Adjust color maps using over 50 scientific colormaps for enhanced data interpretation.
- **Vector Layers**:
  - Visualize specific vector data columns with custom settings for size, width, opacity, fill, and color.
  - Apply scalar data visualization using scientific colormaps.
- **Grid Settings**:
  - Add latitude and longitude grids with customizable size, width, opacity, and color to create publication-ready visuals.

---

### **Data Processing**

#### **Data Sampling**
- Extract raster and vector data within a specified area of interest, shapefile, or bounding region to create machine-trainable datasets for geospatial machine learning, geostatistics, and modeling.
- Generate grids for sampling:
  - **Random Grid**: Define a specified number of points.
  - **Regular Grid**: Set a specific resolution.
- Perform operations:
  - Sample raster data onto grids.
  - Sample specific vector data columns and calculate distances to nearby vector features.

#### **GIS-Style Vector Processing**
- **Merge Layers**: Combine multiple vector layers row-wise or column-wise.
- **Bounding Box Creation**: Generate bounding box layers from raster or vector data for sampling.
- **Data Filtering**: Apply Python-style conditions to filter geospatial data.
- **Calculator Tool**:
  - Perform Python-style calculations on layers for diverse applications:
    - **Satellite Data**: Calculate band ratios and remote sensing indices.
    - **Geophysical Data**: Apply complex potential field filters.
    - **Image Processing**: Develop filters for structural analysis, fault mapping, and more.

---

### **Machine Learning**
Kalpa integrates cutting-edge machine learning models to support supervised and unsupervised tasks:

- **Supported Models**:
  - Random Forest Regressor and Classifier.
  - Positive Labeled Enabled Bagging (PU-enabled RF).
  - K-means Clustering and DBSCAN.
  - More models coming soon.
- **Applications**:
  - **Geological Insights**:
    - Predict paleotopography, crustal thickness, and lithosphere thickness.
  - **Mineral Exploration**:
    - Analyze lithological units, alteration types, and mineral distributions.
    - Create prospectivity maps of minerals such as Cu, Au, Pb, Zn, and Fe.
  - **Natural Hazards**:
    - Predict landslides, floods, and forest fires.
  - **Agriculture**:
    - Enhance agricultural productivity using geospatial data.
- **Model Sharing**:
  - Save trained models for reuse and share them with others.
  - Apply trained models to new regions for insights.

---

### **Utilities**
- **Resource Monitoring**: Display current RAM utilization.
- **Coordinate Tracking**: View precise coordinates of the cursor.

---

## Why Choose Kalpa?
Kalpa is not just a tool; it is your gateway to unlocking the full potential of geospatial data. Whether you are an ArcGIS or QGIS user or exploring geospatial data for the first time, Kalpa equips you with the features and flexibility to achieve your goals effortlessly.

---

## License
[MIT License](LICENSE)



## Contributing
We welcome contributions from the community! Please read our [Contributing Guide](CONTRIBUTING.md) for more details.

---

## Contact
For support or inquiries, please contact [Satyam Pratap Singh](singhsatyampratap@gmail.com).

---


Happy Mapping with Kalpa!
