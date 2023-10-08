Step 1. Import the necessary librariesPermalink
import pandas as pd
Step 2. Import the dataset from this address.Permalink
Step 3. Assign it to a variable called chipo.Permalink
url = 'https://raw.githubusercontent.com/justmarkham/DAT8/master/data/chipotle.tsv'
    
chipo = pd.read_csv(url, sep = '\t')
Step 4. See the first 10 entriesPermalink
chipo.head(10)
 	order_id	quantity	item_name	choice_description	item_price
0	1	1	Chips and Fresh Tomato Salsa	nan	$2.39
1	1	1	Izze	[Clementine]	$3.39
2	1	1	Nantucket Nectar	[Apple]	$3.39
3	1	1	Chips and Tomatillo-Green Chili Salsa	nan	$2.39
4	2	2	Chicken Bowl	[Tomatillo-Red Chili Salsa (Hot), [Black Beans, Rice, Cheese, Sour Cream]]	$16.98
5	3	1	Chicken Bowl	[Fresh Tomato Salsa (Mild), [Rice, Cheese, Sour Cream, Guacamole, Lettuce]]	$10.98
6	3	1	Side of Chips	nan	$1.69
7	4	1	Steak Burrito	[Tomatillo Red Chili Salsa, [Fajita Vegetables, Black Beans, Pinto Beans, Cheese, Sour Cream, Guacamole, Lettuce]]	$11.75
8	4	1	Steak Soft Tacos	[Tomatillo Green Chili Salsa, [Pinto Beans, Cheese, Sour Cream, Lettuce]]	$9.25
9	5	1	Steak Burrito	[Fresh Tomato Salsa, [Rice, Black Beans, Pinto Beans, Cheese, Sour Cream, Lettuce]]	$9.25
Step 5. What is the number of observations in the dataset?Permalink
chipo.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 4622 entries, 0 to 4621
Data columns (total 5 columns):
order_id              4622 non-null int64
quantity              4622 non-null int64
item_name             4622 non-null object
choice_description    3376 non-null object
item_price            4622 non-null object
dtypes: int64(2), object(3)
memory usage: 180.6+ KB
Step 6. What is the number of columns in the dataset?Permalink
chipo.shape[1]
5
Step 7. Print the name of all the columns.Permalink
chipo.columns
Index([u'order_id', u'quantity', u'item_name', u'choice_description',
       u'item_price'],
      dtype='object')
Step 8. How is the dataset indexed?Permalink
chipo.index
RangeIndex(start=0, stop=4622, step=1)
Step 9. Which was the most-ordered item?Permalink
chipo.groupby(['item_name']).count().sort_values(['quantity'], ascending = False).head(1).reset_index()['item_name']
0    Chicken Bowl
Name: item_name, dtype: object
Step 10. For the most-ordered item, how many items were ordered?Permalink
chipo.groupby(['item_name']).sum().sort_values(['quantity'], ascending = False).head(1)['quantity']
Step 11. What was the most ordered item in the choice_description column?Permalink
chipo.groupby(['choice_description']).sum().sort_values(['quantity'], ascending = False).head(1)
| choice_description | order_id | quantity | | :—————– | ——-: | ——-: | | [Diet Coke] | 123455 | 159 |

Step 12. How many items were orderd in total?Permalink
chipo['quantity'].sum()
4972
Step 13. Turn the item price into a floatPermalink
Step 13.a. Check the item price typePermalink
chipo['item_price'].dtype
dtype('O')
Step 13.b. Create a lambda function and change the type of item pricePermalink
chipo['item_price'] = chipo['item_price'].apply(lambda x : float(x[1:-1])) 
Step 13.c. Check the item price typePermalink
chipo['item_price'].dtype
dtype('float64')
Step 14. How much was the revenue for the period in the dataset?Permalink
chipo['item_price'].sum()
34500.16
Step 15. How many orders were made in the period?Permalink
len(chipo['order_id'].unique())
1834
Step 16. What is the average revenue amount per order?Permalink
chipo['revenue'] = chipo['quantity'] * chipo['item_price']
order_grouped = chipo.groupby(by=['order_id']).sum()
order_grouped.mean()['revenue']
21.394231188658654
Step 17. How many different items are sold?Permalink
chipo['item_name'].value_counts().count()
50
