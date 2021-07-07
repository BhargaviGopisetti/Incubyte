# Incubyte Assessment

# Problem Statement:

I own a Multi-Specialty Hospital chain with locations all across the world. My hospital is famous for Vaccination. Patients who come to my hospital (across the globe) will be given a User Card with which they can access any of my hospital in the world. 

Current Status: We maintain all customers in one database. There are heaps of customers with user cards to my hospital. So, I decided to split up the customers based on the country and load them into corresponding country tables.

To pull the customers as perCountry, my developers should know what are all the places the Customer Data is available. So, the data extracting will be done by our Source System. They will pull the all the relevant customer data and will give us a Data file. 

# Steps in workflow:

1. Read data for each country from source.
2. Create text files.
3. Read text files.
4. Write data from each file to target tables in database.

# Answers:
```
# Query to list the countries

SELECT 
    DISTINCT country
FROM source_table;

# Query to pull each country’s data

SELECT 
    *
FROM source_table
WHERE country =’country_name’;


# Query to create the table for each country

CREATE TABLE table_{country_name} (
    Customer_Name VARCHAR(255) NOT NULL,
    Customer_Id ARCHAR(18) NOT NULL,
    Open_Date DATE NOT NULL,
    Last_Consulted_Date DATE,
    Vaccination_Id CHAR(5),
    Dr_Name CHAR(255),
    State CHAR(5),
    Country CHAR(5),
    Post_Code INT,
    DOB DATE,
    Is_Active CHAR(1),
    PRIMARY KEY (Customer_Name)
);
```

# Python Program to read the data from file:

```
# Import required libraries
import pandas as pd
import numpy as np
from sqlalchemy import create_engine

# Read File to Pandas dataframe
df = pd.read_csv("File_Name",sep='|')

# Review data
df.columns
df

# Remove NULL column from pandas dataframe
df = df.loc[:, ~df.columns.str.contains('^Unnamed')]
df.columns

# Column: Post_code is missing in file. So an empty column is added to the dataframe.

df.insert(9, 'Post_Code', np.nan)
df

# Sample Python code to store Pandas dataframe to database
sqlEngine = create_engine("Connection credentials")
dbConnection = sqlEngine.connect()
tableName = "table_name"
frame = dataFrame.to_sql(tableName, dbConnection);


