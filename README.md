# Bond-Yields-Intererst-Rate
This project looked to examine the historical relationship between Canada's bond yield spread and the overnight interest rates. 

Data for the analysis was downloaded in .csv format from https://www150.statcan.gc.ca/t1/tbl1/en/tv.action?pid=1010013901 as seen in the file "105statCan_download".
The variables selected for download were "Reference period","Overnight rate","bond yields, 2 year","bond yields, 10 year". The reference period (dates) span from January 11th, 2000 to present (June 15th, 2023). 
First a database and table (bonds2000) were created using the following names and variables for each column:

Reference period = ref_period, varchar(50)
Overnight rate = overnight_rate, float(10,5)
bond yields, 2 year = two_yr_bond, float(10,5)
bond yields, 10 year = ten_yr_bond, float(10,5)

The .csv file was imported in the bonds2000 table using the table import wizard, dropping rows with empty values (days on the weekends were included but had no data)

ref_period was set as a varchar as the date was provided in the format "January 11th, 2000". To convert the dates to a more optimal variable, a new column was created called new_date_column with the DATE format. 
The original ref_period values were converted and placed in the new_date_column with the following code: 

UPDATE my_table
SET new_date_column = STR_TO_DATE(date_column, '%M %d, %Y')

The original ref_period column was dropped. A new column acting as the primary key was added with the name "id" using 'int' variable to populate the fields. 

A new column (two_ten_spread) was created to present the spread (difference) between the short and long term bond yields, with the following code:

UPDATE bonds2000 SET two_ten_spread = ten_yr_bond - two_yr_bond;


The final table that was exported as a json file using the table export wizard was as seen below:

FIELD, TYPE, NULL, KEY
'overnight_rate', 'float(10,5)', 'YES'
'two_yr_bond', 'float(10,5)', 'YES'
'ten_yr_bond', 'float(10,5)', 'YES''
'new_date_column', 'date', 'YES'
'id', 'int', 'NO', 'PRI'
'two_ten_spread', 'float(10,4)', 'YES'

This data was then imported into my Tableau Public account and visualized here:
https://public.tableau.com/app/profile/patrickritsma/viz/2000-2023CanadianBondYieldSpreadInterestRate/BondSpreadVs_InterestRate

