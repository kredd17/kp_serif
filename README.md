

### 1. Exploratory Data Analysis
While reviewing the tic dataset and doing some research on publicly available sources, the following were observed:
- for the same procedure at the same hospital there were different rates for the same provider (NPI)
- the same NPI had different rates for the same PFS_FACILITY id as well
- there was a wide distribution of rates and doing an average would have skewed the data due to **outliers**
- A key decision made was to take the **median** of the rate to account for outliers
- The tic dataset was **flattened** converting the cms baseline schedule values (post grouping into facility, non-facility, etc) into columns


### 2. Data Cleaning
##### Matching the hospital
- The tic dataset has the tax identifier column 'ein', but the same is not explicitly available in the hpt dataset. The source_file_name column int he hpt dataset has the ein for the hospital embedded in the values. The values is obtained by removing "-" and parsing the first 9 characters to create the 'key_ein' column.

#### Matching the payer
- the hpt dataset also had free form list for different payers which was cleaned up to create another key to join the datasets on
- Reason for not filtering for PPO in plan names in the hpt dataset: The tic dataset is supposed to have only PPO negotiated rates. I was not sure if text based filtering for PPO was ok. I tried it, but found the record count drop to be high. Once I get more familiar with the healthcare payments area, may think differently

#### Matching the billing code
- hpt dataset needed a minor clean up to remove string values coming in the code


### 3. Data Modeling
The hpt dataset was left joined with the flattened tic dataset on ein, abbreviated payer name and codes


### 4. How to run the code
- I used simple python libraries numpy and pandas for this exercise. Given the low volume of data and the rough prototype nature of the work, I chose a combination of tableau for data exploration and python for the data modeling.
- the jupyter notebook titled Data_model.ipynb can be run to re-generate the final merged_data.csv


### 5 For production
- come up with a better way to identify payers in the hpt data rather than text based parsing
- gain a better understanding for the different types of billing so as to trim down the measure columns to only the relevant ones 







