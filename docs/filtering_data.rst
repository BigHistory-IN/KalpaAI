.. _filtering_data:

==============
Filtering Data
==============

In geospatial analysis, filtering vector data is a common task to refine datasets based on specific conditions. Kalpa offers a powerful and flexible filtering mechanism using Python's Pandas-style operations. This chapter demonstrates how to filter vector data using conditions on one or multiple columns, enabling you to create tailored datasets for your analysis.

Vector Filtering
----------------

The ``VectorLayerFiltering`` function allows you to filter a vector layer or a file containing vector data (``.gpkg``/``.shp``) using custom conditions written in Python's Pandas-style operations.

Function Overview
~~~~~~~~~~~~~~~~~
The ``VectorLayerFiltering`` function applies a condition to filter rows in a vector dataset and returns the filtered result.

**Key Arguments:**

- A file path to a vector dataset or selection of a layer (e.g., ``.gpkg``, ``.shp``).
- ``filter_condition``: A Python condition for filtering rows. The condition uses the format:

  ``row['column_name'] <condition> value``

  You can combine multiple conditions using logical operators like ``and``, ``or``, and ``not``.

Examples
--------

**Single-Column Based Filtering**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- **Scenario**: Filter all rows where the ``Population`` column is greater than 1,000.
- **Condition String**: ``row['Population'] > 1000``

**Multi-Column Based Filtering**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- **Scenario**: Filter rows where the ``Population`` is greater than 1,000 and the ``City`` starts with the letter 'C'.
- **Condition String**: ``row['Population'] > 1000 and row['City'].startswith('C')``

**Filtering Using Equality Conditions**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- **Scenario**: Filter rows where the ``City`` column is equal to 'B'.
- **Condition String**: ``row['City'] == 'B'``

**Combining Conditions with OR**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- **Scenario**: Filter rows where the ``Population`` is less than 1,000 or the ``City`` starts with 'A'.
- **Condition String**: ``row['Population'] < 1000 or row['City'].startswith('A')``

**Filtering by Distance (Geospatial Attributes)**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- **Scenario**: Filter rows where the distance to a fault line is less than 5 km.
- **Condition String**: ``row['Fault_Dist'] < 5``

**Filtering Rows with Numerical Ranges**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- **Scenario**: Filter rows where ``Population`` is between 500 and 1,500.
- **Condition String**: ``500 <= row['Population'] <= 1500``

**Filtering Rows Based on String Patterns**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- **Scenario**: Filter rows where the ``City`` name contains the letter 'a' (case-insensitive).
- **Condition String**: ``row['City'].str.contains('a', case=False)``

**Filtering Rows with Missing or Null Values**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- **Scenario**: Filter rows where the ``geometry`` column is ``None`` (missing).
- **Condition String**: ``row['geometry'] is None``

**Filtering Rows Based on Multiple Conditions (Advanced)**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- **Scenario**: Filter rows where ``Population`` is greater than 1,000, and the ``City`` does not start with 'A'.
- **Condition String**: ``row['Population'] > 1000 and not row['City'].startswith('A')``

**Filtering Rows Using Custom Functions**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- **Scenario**: Use a custom function to filter rows where the ``City`` name length is greater than 1 character.
- **Condition String**: ``len(row['City']) > 1``

**Filtering Geospatial Data by Attribute and Proximity**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- **Scenario**: Filter rows where faults are older than 50 million years and within 10 km of the grid points.
- **Condition String**: ``row['Fault_Age'] > 50 and row['Fault_Dist'] < 10``

**Filtering Using Logical OR Conditions**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- **Scenario**: Filter rows where the ``City`` is either 'A' or 'C'.
- **Condition String**: ``row['City'] in ['A', 'C']``

**Filtering by Area or Length Attributes**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
For vector datasets with polygons or lines, you can filter by geometric properties such as area or length.

- **Scenario**: Filter polygons where the area is greater than 1,000 square meters.
  - **Condition String**: ``row['geometry'].area > 1000``

- **Scenario**: Filter line features where the length is less than 500 meters.
  - **Condition String**: ``row['geometry'].length < 500``

Tips for Writing Filtering Conditions
-------------------------------------
1. **Use Logical Operators**: Combine conditions with ``and``, ``or``, or ``not`` to create complex queries.
2. **Check Data Types**: Ensure your column data types match the condition. Numeric values should not be compared to strings.
3. **Handle Missing Values**: Use Pandas-style operations like ``row['column'].notnull()`` to filter out rows with missing data.
4. **Validate Columns**: Ensure the columns used in filtering exist in the dataset.
5. **Optimize Conditions**: Use simple, efficient conditions to avoid unnecessary computational overhead.
6. **Test Conditions**: Before applying complex filters, test them on a small subset of data to ensure correctness.
7. **Export Results**: Save filtered datasets for further analysis or visualization.


