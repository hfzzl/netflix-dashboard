# Netflix Dashboard

This project involves cleaning and preprocessing a dataset from Netflix. The dataset contains information about Netflix titles, including movies and TV shows, with attributes such as cast, country, director, and release date. The goal is to prepare the data for further analysis.

---

## **Project Overview**

This script handles tasks such as checking for missing values, replacing or removing them as needed, formatting date columns, and creating new features to aid in analysis.

---

## **Requirements**

Ensure you have the following Python libraries installed:
- `pandas`
- `numpy`
- `datetime`

You can install these packages using:
```bash
pip install pandas numpy
```

---

## **Code Workflow**

1. **Importing Libraries**  
   The script uses the following libraries:  
   ```python
   import numpy as np
   import pandas as pd
   import datetime as dt
   ```

2. **Loading the Dataset**  
   The Netflix dataset is loaded into a Pandas DataFrame:  
   ```python
   filename = '/path/to/netflix.csv'
   data = pd.read_csv(filename)
   ```

3. **Data Inspection**  
   The script previews the dataset and checks for duplicates and missing values:  
   ```python
   data.head(5)
   data.duplicated().sum()
   data.isnull().sum()
   ```

4. **Handling Missing Values**  
   - For columns with missing values, the percentage of missing data is calculated:  
     ```python
     for i in data.columns:
         null_rate = data[i].isna().sum() / len(data) * 100
         if null_rate > 0:
             print(f"{i} null rate: {round(null_rate, 2)}%")
     ```
   - Missing values in the `country` column are replaced with the most frequent value:  
     ```python
     data['country'] = data['country'].fillna(data['country'].mode()[0])
     ```
   - Missing values in `cast` and `director` are replaced with `"No Data"`:  
     ```python
     data['cast'] = data['cast'].fillna('No Data')
     data['director'] = data['director'].fillna('No Data')
     ```
   - Other rows with missing values are dropped:  
     ```python
     data.dropna(inplace=True)
     ```

5. **Data Formatting**  
   - The `date_added` column is converted to `datetime` format:  
     ```python
     data['date_added'] = pd.to_datetime(data['date_added'].str.strip())
     ```
   - New columns for `month_added` and `year_added` are created:  
     ```python
     data['month_added'] = data['date_added'].dt.month_name()
     data['year_added'] = data['date_added'].dt.year
     ```

6. **Saving the Cleaned Dataset**  
   The cleaned dataset is saved as a new CSV file:  
   ```python
   data.to_csv('netflix.csv', index=False)
   ```

---

## **Usage**

1. Replace the `filename` path with the actual file path for your Netflix dataset.
2. Run the script to clean and preprocess the data.
3. Use the cleaned `netflix.csv` file for further analysis or visualization.

---

## **Outputs**


- **Link:** https://public.tableau.com/views/Netflix_17327484411120/Dashboard1?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link
![Dashboard 1 (1)](https://github.com/user-attachments/assets/2b21ca19-6bf6-400b-b637-c45c115b2f45)

