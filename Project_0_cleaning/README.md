# Dataset cleaning (Power Query

![Project 2 Photo](/images/project_2_photo.png)

# Introduction

This Part of the project is specified to clean the messy data so it become ready to be analyzed.

## Analysis File

My final file is in [Project_0_cleaning](/Project_0_cleaning/Project_cleaning.xlsx)

## Excel Skills Used

In the first part of the project the goal is to improve my skills in :

- **Power Query**

# Cleaning

## Order Date Column

![OrderDate Column](/images/date_column.png)
_Dataset Before_

Decisions :

- Change its type to **date** to unify the column values
- Remove error rows
- **Extract order month\*** as new column
- **Extract order day** as new column
- **Extract order year** as a new column
- **Reorder** columns

![OrderDate Column](/images/date_column_after.png)
_Dataset After_

## Customer Name Column

Decisions :

- **Replace** nulls with 'not mentioned'

## Category Column

![Category Column](/images/category_column.png)
_Dataset Before_

Decisions :

- **Fix** typos
- **Capitalize** column
- **Remove** rows with empty category

![Category Column](/images/category_column_after.png)
_Dataset After_

## Payment Method Column

![Payment Method Column](/images/payment_method_column.png)
_Dataset Before_

Decisions :

- **Lowercase** column to unify values
- **Trim** column to remove whitespaces
- **Fix** typos
- **Capitalize** column
- **Filter** to remove nulls

![Category Column](/images/payment_method_column_after.png)
_Dataset After_

## Country Column

![Payment Method Column](/images/country_column.png)
_Dataset Before_

Decisions :

- **Lowercase** column to unify values
- **Trim** column to remove whitespaces
- **Fix** typos
- **Capitalize** column
- **Remove** nulls

![Category Column](/images/country_column_after.png)
_Dataset After_

## Quantity + Sales + Price Columns

Decisions :

- **Filter** to remove nulls.

# Conclusion

Now after cleaning the dataset , it is ready for the deep analysis.
