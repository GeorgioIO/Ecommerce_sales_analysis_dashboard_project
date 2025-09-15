# Store Sales Analysis (Formulas + Functions)

![Project 1 Photo](/images/project_1_photo.png)

# Introduction

This Part of the project showcase my abilities in answering different analytical questions from the owner using **Formulas** and **Functions** in **Excel**.

## Analysis File

My Final analysis file is in [Project_1_analysis](/Project_1_analysis/Project_analysis_formulas.xlsx)

## Questions to Analyze

To understand the data of the bookstore , I asked the following ?

1. What are the peak days in sales ?
2. What category make up the most in sales contribution ?
3. How does the sales varies in each month for each country ?
4. What is the most used payment method in each country ?
5. What book sells the most in the store ?

## Excel Skills Used

In this specific part of the project i focused on showcasing my skills in using different excel formulas :

- 🧮 **Formulas and Functions**
- ❎ **Data Validation**
- 🔍 **LOOKUPS Functions**
- 🎛️ **Conditional Formatting**

# 1️⃣ What are the peak days in sales ?

![question 1 table](/images/question_1_table.png)
![question 1 photo](/images/question_1_analysis.png)

#### Steps

- First of all i extracted all the orders days , then we can sort them using **Custom Sort**. then for the two columns **Orders Count** , **Total Sales** i used the following formulas :

- **Orders Count**

```excel
=COUNTIF(orders[OrderDay],B4)
```

_i basically counted the number of orders from **orders** table , and checked if they are equal to value B4 which is the day_

- **Total Sales**

```excel
=SUMIF(orders[OrderDay],B4,orders[TotalSales])
```

_i sumed all **TotalSales** the values in **orders** table **OrderDay** column where the day is equal to the wanted day_

## 🤔 Insights

As we can see the peakest day of the year is **Monday** with nearly **37k** in sales , while the lowest is **Tuesday** with **32k** with small difference with the others.

# 2️⃣ What category make up the most in sales contribution ? ?

![question 2 table](/images/question_2_table.png)
![question 2 photo](/images/question_2_analysis.png)

#### Steps

- First of all i extracted all the categories in our data using `UNIQUE(orders[Category]))` , then i created 7 _columns_ to analyse , the most important one is _Contribution In sales_ :

- **Contribution in sales :**

```excel
=(D4/$D$8) * 100
```

- **Avg Sales :**

```excel
=AVERAGEIF(orders[Category],B4,orders[TotalSales])
```

_Here i calculated the average of **Sales** Where **Category** is equal to the equivalent **Category** on **B4**._

- **Median Sales :**

```excel
=MEDIAN(IF( orders[Category]=B4,orders[TotalSales]))
```

_Here i wanted to get the median sales for each category , since **MEDIAN()** doesn't have **MEDIANIF()** , so i nested MEDIAN WITH IF_.

- _Max Sales + Min Sales :_

```excel
=MINIFS(orders[TotalSales],orders[Category],B4)
```

```excel
=MAXIFS(orders[TotalSales],orders[Category],B4)
```

## Look up

![question 2 lookup](/images/question_2_lookup_last.png)

In this table i want to use **Excel LOOKUP Functions** to find out what Category have the highest sale , and the lowest.

```excel
=XLOOKUP(
        MAX(orders[TotalSales]),
        orders[TotalSales],
        orders[Category]
        )
```

```excel
=XLOOKUP(
        MIN(orders[TotalSales]),
        orders[TotalSales],
        orders[Category]
        )
```

## 🤔 Insights

By only looking at the chart we can determine that **Fiction** contribute the most between all the categories in sales with **33%** while **Comics** is the lowest with **17%**.

# 3️⃣ How does the sales varies in each month for each country ?

![question 3 table](/images/question_3_table.png)
![question 3 photo](/images/question_3_analysis.png)

- First of all the countries we have from our table and we transform them to horizental form using **`TRANSPOSE()`**, and then for each cell we apply **`SUMIFS()`** , and lastly i used **sparkline** to have quick insight to know the highest month for each country:

```excel
=TRANSPOSE(B3#)
```

```excel
=SUMIFS(orders[TotalSales],orders[Country],$C$13,orders[OrderMonth],$B14)
```

![question 3 second table](</images/question_3_(2)_table.png>)

_I also created this table to show the best month for each country using **`INDEX()`**:_

```excel
=INDEX(
        $B$14:$B$25,
        MATCH(MAX(C$14:C$25),C$14:C$25,0)
        )
```

- `$B$14:$B$25` Represents the months column in the first table **which will be our reference value that we want to initially extract**
- `MATCH(MAX(C$14:C$25),C$14:C$25,0)` here we are looking the max value `MAX(C$14:C$25)` in the given country column `C$14:C$25` Canada for example , and it will return the max value from it , with exact match `0`.
- This will lookup the max value of each column and get our **reference value** from months column.

## 🤔 Insights

As we can see countries like **France** , **Germany** both have october as their highest month , while country in the middle east like **Lebanon** have March as the highest month.

# 4️⃣ What is the most used payment method in each country ?

![question 4 photo](/images/question_4_analysis_last_2.png)

- First of all i extracted the payment methods of my dataset as using the spilling operator `B4#` and then placed the countries horizentally using `TRANSPOSE()` , and to get the **COUNT** of how many time each payment method is used in a country i used `SUMPRODUCT()`, and lastly i used conditional formatting **Data Bar** to visualize the data.

```excel
=TRANSPOSE(UNIQUE(orders[Country]))
```

```excel
=SUMPRODUCT((orders[PaymentMethod]=G4)*(orders[Country]=H$3))
```

- Here basically we will check in our dataset , if **Payment Method** equal the given one , and **Country** equal also the given one , it will return 1 because TRUE _ TRUE = 1 _ 1 = 1, and then we sums all the ones we have to get the **count** of payment method usage per country

## 🤔 Insights

As we can see **Voucher** overall is the least used payment method in all the countries even hitting 0 in **Italy** and **Spain** , while the most used payment method is **Credit Card** Averaging 144 usage per country.

# 5️⃣ What book sells the most in the store ?

![question 5 table](</images/question_5_(2)_table.png>)
![question 5 table](/images/question_5_table.png)
![question 5 photo](/images/question_5_analysis.png)

First of all on the side i extracted for the main dataset table the uniques books title and sorted them alphabetically using `SORT(UNIQUE())` and for each country summed the total sales `SUMIF()` and counted the total orders count `COUNTIF()`, then to create the second table to take only the top 10 i used `TAKE(SORT())` nested with `SORT()` to sort them based on Total Sales.

```excel
=SORT(UNIQUE(orders[BookTitle]))
```

```excel
=SUMIF(orders[BookTitle],B2,orders[TotalSales])
```

```excel
=COUNTIF(orders[BookTitle],B2)
```

```
=TAKE(SORT(B2:D1177,2,-1),10)
```

## Bonus

![question 5 data validation](/images/question_5_gif.gif)

Here i created a tiny tool with **Data validation** , it allow to lookup different statistical stats for a specific book title in the dataset by using `MAXIFS()` , `MINIFS()` , `SUMIF()` , `COUNTIF()`.

## 🤔 Insights

As we can demonstrate Table huge seems to be one of the most demanded books in the store at the same time being the top book in sales hitting **1k**.

# Conclusion

In this section i empowered my skills in **Excel** different features such as **Formulas** , **Functions** , **Conditional Formatting** , **Charts** , **Sparklines**...
