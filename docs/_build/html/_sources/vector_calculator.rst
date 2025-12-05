Vector Calculator
=================

The **Vector Calculator** feature in **Kalpa** allows you to perform advanced calculations on the columns of a vector dataset (GeoDataFrame) and save the results as a new column. This is particularly useful for **geospatial data engineering**, **statistical analysis**, and **feature generation** for machine learning.

Using the **VectorLayerCalculator** operation, you can define **custom operations** to compute new columns based on existing data in a vector layer. This chapter guides you through the process of using the Vector Calculator, including **practical examples**.

How to Use the Vector Calculator
--------------------------------

To compute new columns in your vector data, follow these steps:

1. **Load the Dataset**  
   Ensure that the vector dataset is loaded into **Kalpa**.

2. **Define the New Column Name**  
   Choose a **descriptive name** for the column that will store the calculated values.

3. **Write the Operation Code**  
   Use **Python expressions** to define the calculation. Examples:  

   - ``row['column1'] + row['column2']``
   - ``row['column1'] * 1.5``
   - ``len(row['city_name'])``

4. **Save the Result**  
   After defining the operation, execute and save the results directly into the dataset.

Using the GUI
~~~~~~~~~~~~~

When using Kalpa’s **Graphical User Interface (GUI)**, you will be prompted to provide the following:

- **Select Layer**: Choose the vector layer to apply the calculation.
- **New Column Name**: Specify the name of the column to store the result.
- **Condition**: Write the operation code (Python expression) that defines how to compute the new column.

Examples
--------

1. **Basic Arithmetic Operation**  
Add two columns ``col1`` and ``col2`` to create a new column ``sum_col``:

::

    sum_col
    row['col1'] + row['col2']

2. **Scaling a Column**  
Multiply a column value by a constant factor:

::

    scaled_value
    row['value'] * 1.5

3. **String Length Calculation**  
Create a column representing the length of strings in ``city_name``:

::

    city_name_length
    len(row['city_name'])

4. **Conditional Calculation**  
Create a binary column ``high_population`` based on a threshold:

::

    high_population
    1 if row['population'] > 1000 else 0

5. **Combining String Values**  
Merge ``city`` and ``state`` into a single ``Location`` column:

::

    Location
    f"{row['city']}, {row['state']}"

6. **Calculating Distance to a Reference Point**  
Calculate the distance of each geometry to a reference point:

::

    distance_to_point
    row['geometry'].distance(reference_point)

7. **Geometric Area Calculation**  
Compute the area of each geometry (for polygons):

::

    area
    row['geometry'].area

8. **Custom Transformations**  
Apply a logarithmic transformation to a numeric column:

::

    log_value
    math.log(row['value'])

Using the Results
-----------------

Once calculations are completed, you can:

- **Visualize** the new column directly in **Kalpa's** interface.
- Use the updated vector layer for further **geospatial or statistical analysis**.
- **Export** the enriched dataset as a **GeoPackage (.gpkg)** file or other supported formats using Kalpa’s export options.

Best Practices
--------------

1. **Column Names**  
   Use **clear and descriptive names** for new columns to keep the dataset understandable.

2. **Error Handling**  
   Check your Python expressions for **syntax errors** or **invalid column references** before applying them.

3. **Performance**  
   Avoid overly complex computations on large datasets to maintain **good performance**.

4. **Documentation**  
   Keep a record of all applied transformations for **reproducibility** and future reference.
