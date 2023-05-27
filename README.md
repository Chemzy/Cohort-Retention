# Cohort-Retention
The provided SQL code seems to be performing a retention cohort analysis on an online retail dataset. Here's a breakdown of the code and its steps:

The initial part of the code cleans the data by removing records with invalid CustomerID values and filtering out records with non-positive quantities or unit prices.

The "dup_check" CTE is used to identify and remove duplicate records based on the combination of InvoiceNo, StockCode, Quantity, and InvoiceDate. Only the records with a "dup_flag" of 1 (indicating no duplicates) are selected into the temporary table "#online_retail_main".

The next step involves creating a cohort analysis by determining the unique identifiers (CustomerID), the first purchase date (min(InvoiceDate)), and the cohort date (the first day of the month of the first purchase). This information is stored in the temporary table "#cohort".

A cohort index is created by calculating the number of months between the invoice date and the cohort date. This is done in the "#cohort_retention" CTE. The result is stored in the temporary table "#cohort_pivot".

Finally, a pivot table is created using dynamic SQL to display the cohort analysis results. The pivot table shows the count of unique customers for each cohort index (month) relative to the first cohort index. The dynamic SQL is constructed using the cohort indexes obtained from the "#cohort_retention" table.

The code produces the cohort analysis results in a tabular format with columns representing the cohort indexes (months) and rows representing the cohort dates. Each cell in the table represents the percentage of customers retained from the initial cohort for each subsequent month.

Note: The code also includes a commented section labeled "DYNAMIC SQL TO CREATE PIVOT TABLE," which demonstrates an alternative method to dynamically generate the pivot table based on the available cohort indexes. However, this section is not executed in the code provided.
