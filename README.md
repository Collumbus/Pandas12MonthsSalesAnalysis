# Pandas Data Science Analysis
Set of real world data science tasks completed using the Python Pandas library.

## Background Information:

In this project we use Python Pandas & Python Matplotlib to analyze and answer business questions about 12 months worth of sales data. The data contains hundreds of thousands of electronics store purchases broken down by month, product type, cost, purchase address, etc.

We start by cleaning our data. Tasks during this section include:
- Drop NaN values from DataFrame
- Removing rows based on a condition
- Change the type of columns (to_numeric, to_datetime, astype)

Once we have cleaned up our data a bit, we move the data exploration section. In this section we explore 5 high level business questions related to our data:
- What was the best month for sales? How much was earned that month?
- What city sold the most product?
- What time should we display advertisemens to maximize the likelihood of customer’s buying product?
- What products are most often sold together?
- What product sold the most? Why do you think it sold the most?

To answer these questions we walk through many different pandas & matplotlib methods. They include:
- Concatenating multiple csvs together to create a new DataFrame (pd.concat)
- Adding columns
- Parsing cells as strings to make new columns (.str)
- Using the .apply() method
- Using groupby to perform aggregate analysis
- Plotting bar charts and lines graphs to visualize our results
- Labeling our graphs







#### Data wrangling.

df.head()


|    |   Order ID | Product                    |   Quantity Ordered |   Price Each |   Sales | Order Date          |   Month | Purchase Address                     | City             |
|---:|-----------:|:---------------------------|-------------------:|-------------:|--------:|:--------------------|--------:|:-------------------------------------|:-----------------|
|  0 |     176558 | USB-C Charging Cable       |                  2 |        11.95 |   23.9  | 2019-04-19 08:46:00 |       4 | 917 1st St, Dallas, TX 75001         | Dallas (TX)      |
|  2 |     176559 | Bose SoundSport Headphones |                  1 |        99.99 |   99.99 | 2019-04-07 22:30:00 |       4 | 682 Chestnut St, Boston, MA 02215    | Boston (MA)      |
|  3 |     176560 | Google Phone               |                  1 |       600    |  600    | 2019-04-12 14:38:00 |       4 | 669 Spruce St, Los Angeles, CA 90001 | Los Angeles (CA) |
|  4 |     176560 | Wired Headphones           |                  1 |        11.99 |   11.99 | 2019-04-12 14:38:00 |       4 | 669 Spruce St, Los Angeles, CA 90001 | Los Angeles (CA) |
|  5 |     176561 | Wired Headphones           |                  1 |        11.99 |   11.99 | 2019-04-30 09:27:00 |       4 | 333 8th St, Los Angeles, CA 90001    | Los Angeles (CA) |




#### Question 1: What was the best month for sales? How much was earned that month?

|   Month |   Quantity Ordered |   Price Each |       Sales |
|--------:|-------------------:|-------------:|------------:|
|      12 |              28114 |  4.58842e+06 | 4.61344e+06 |
|      10 |              22703 |  3.71555e+06 | 3.73673e+06 |
|       4 |              20558 |  3.36767e+06 | 3.39067e+06 |
|      11 |              19798 |  3.1806e+06  | 3.1996e+06  |
|       5 |              18667 |  3.13513e+06 | 3.15261e+06 |
|       3 |              17005 |  2.79121e+06 | 2.8071e+06  |
|       7 |              16072 |  2.63254e+06 | 2.64778e+06 |
|       6 |              15253 |  2.56203e+06 | 2.5778e+06  |
|       8 |              13448 |  2.23035e+06 | 2.24447e+06 |
|       2 |              13449 |  2.18888e+06 | 2.20202e+06 |
|       9 |              13109 |  2.08499e+06 | 2.09756e+06 |
|       1 |              10903 |  1.81177e+06 | 1.82226e+06 |

![Question 1 screenshot](/SalesAnalysis/Plots/1.1.png)

### Question 2: What city had the highest number of sales?
| City               |   Quantity Ordered |       Price Each |            Sales |   Month |
|:-------------------|-------------------:|-----------------:|-----------------:|--------:|
| San Francisco (CA) |              50239 |      8.21146e+06 |      8.2622e+06  |  315520 |
| Los Angeles (CA)   |              33289 |      5.42144e+06 |      5.45257e+06 |  208325 |
| New York City (NY) |              27932 |      4.63537e+06 |      4.66432e+06 |  175741 |
| Boston (MA)        |              22528 |      3.63741e+06 |      3.66164e+06 |  141112 |
| Dallas (TX)        |              16730 |      2.75263e+06 |      2.76798e+06 |  104620 |
| Atlanta (GA)       |              16602 |      2.77991e+06 |      2.7955e+06  |  104794 |
| Seattle (WA)       |              16553 |      2.7333e+06  |      2.74776e+06 |  104941 |
| Portland (OR)      |              11303 |      1.86056e+06 |      1.87073e+06 |   70621 |
| Austin (TX)        |              11153 |      1.80987e+06 |      1.81958e+06 |   69829 |
| Portland (ME)      |               2750 | 447189           | 449758           |   17144 |

![Question 2 screenshot](/SalesAnalysis/Plots/2.1.png)

sales_df.head()

### Question 3: What time should we display advertisements to maximize likelihood of customer's buying product?
|    |   Order ID | Product                    |   Quantity Ordered |   Price Each |   Sales | Order Date          |   Month | Purchase Address                     | City             |
|---:|-----------:|:---------------------------|-------------------:|-------------:|--------:|:--------------------|--------:|:-------------------------------------|:-----------------|
|  0 |     176558 | USB-C Charging Cable       |                  2 |        11.95 |   23.9  | 2019-04-19 08:46:00 |       4 | 917 1st St, Dallas, TX 75001         | Dallas (TX)      |
|  2 |     176559 | Bose SoundSport Headphones |                  1 |        99.99 |   99.99 | 2019-04-07 22:30:00 |       4 | 682 Chestnut St, Boston, MA 02215    | Boston (MA)      |
|  3 |     176560 | Google Phone               |                  1 |       600    |  600    | 2019-04-12 14:38:00 |       4 | 669 Spruce St, Los Angeles, CA 90001 | Los Angeles (CA) |
|  4 |     176560 | Wired Headphones           |                  1 |        11.99 |   11.99 | 2019-04-12 14:38:00 |       4 | 669 Spruce St, Los Angeles, CA 90001 | Los Angeles (CA) |
|  5 |     176561 | Wired Headphones           |                  1 |        11.99 |   11.99 | 2019-04-30 09:27:00 |       4 | 333 8th St, Los Angeles, CA 90001    | Los Angeles (CA) |

![Question 3 screenshot](/SalesAnalysis/Plots/3.1.png)

Above we can see that we have 2 peaks of orders, on 12pm and 19pm. So my recommendation is around 11 am and/or 18am.

### Question 4: What products are most sold together?
|     |   Order ID | Grouped                                               |
|----:|-----------:|:------------------------------------------------------|
|   3 |     176560 | Google Phone,Wired Headphones                         |
|  18 |     176574 | Google Phone,USB-C Charging Cable                     |
|  30 |     176585 | Bose SoundSport Headphones,Bose SoundSport Headphones |
|  32 |     176586 | AAA Batteries (4-pack),Google Phone                   |
| 119 |     176672 | Lightning Charging Cable,USB-C Charging Cable         |


### Question 5: What product sold the most? Why do you think it sold the most?
|Product                      |Quantity Ordered|
|:----------------------------|:--------------:|
|20in Monitor                 |   4129         |
|27in 4K Gaming Monitor       |   6244         |
|27in FHD Monitor             |   7550         |
|34in Ultrawide Monitor       |   6199         |
|AA Batteries (4-pack)        |  27635         |
|AAA Batteries (4-pack)       |  31017         |
|Apple Airpods Headphones     |  15661         |
|Bose SoundSport Headphones   |  13457         |
|Flatscreen TV                |   4819         |
|Google Phone                 |   5532         |
|LG Dryer                     |    646         |
|LG Washing Machine           |    666         |
|Lightning Charging Cable     |  23217         |
|Macbook Pro Laptop           |   4728         |
|ThinkPad Laptop              |   4130         |
|USB-C Charging Cable         |  23975         |
|Vareebadd Phone              |   2068         |
|Wired Headphones             |  20557         |
|iPhone                       |   6849         |

![Question 5 screenshot](/SalesAnalysis/Plots/5.1.png)

|Product                      | Mean Prices    |
|:----------------------------|:--------------:|
|20in Monitor                 |  109.99        |
|27in FHD Monitor             |  149.99        |
|27in 4K Gaming Monitor       |  389.99        |
|34in Ultrawide Monitor       |  379.99        |
|AA Batteries (4-pack)        |    3.84        |
|AAA Batteries (4-pack)       |    2.99        |
|Apple Airpods Headphones     |  150.00        |
|Bose SoundSport Headphones   |   99.99        |
|Flatscreen TV                |  300.00        |
|Google Phone                 |  600.00        |
|LG Dryer                     |  600.00        |
|LG Washing Machine           |  600.00        |
|Lightning Charging Cable     |   14.95        |
|Macbook Pro Laptop           | 1700.00        |
|ThinkPad Laptop              |  999.99        |
|USB-C Charging Cable         |   11.95        |
|Vareebadd Phone              |  400.00        |
|Wired Headphones             |   11.99        |
|iPhone                       |  700.00        |

![Question 5 screenshot](/SalesAnalysis/Plots/5.2.png)

The products that sold the most were AA and AAA Batteries (4-pack).

I think it happened because the batteries are very cheap and used a lot in many devices.
