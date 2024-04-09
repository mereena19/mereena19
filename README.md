WALMART sales analysis using python.

I used the data from kaggle and analyze the data using juypter notebook.

# Walmart sales Analysis
import pandas as pd

import numpy as np

import matplotlib.pyplot as plt

import seaborn as sns

data=pd.read_csv('WalmartSalesData.csv')

data.head(5)

columns_to_drop = ['Tax 5%','cogs']

data.drop(columns_to_drop,axis=1,inplace=True)

data.head(5)

data.shape

data.info

data.dtypes

#converting date datatype

data['Date']=pd.to_datetime(data['Date'])

#Which branch have the maximum sales?


#Groupby 'Branch' and calculate total sales

Branch_sales=data.groupby('Branch')['Total'].sum()


#Find the branch with maximum sales

max_sales_branch=Branch_sales.idxmax()

print(f"The branch with maximum sales is: {max_sales_branch}")

#which branch has the highest standard deviation?

#Groupby 'Branch' and calculate standard deviation

branch_std=data.groupby('Branch')['Total'].std()

#Find the highest standard deviation

branch_with_high_std=branch_std.idxmax()

print(f"The branch with highest standard deviation in sales is:{branch_with_high_std}")

#calculate the coefficient of variation for sales across branches?

#groupby branch and calculate mean and std deviation

branch_stats=data.groupby('Branch')['Total'].agg(['mean','std'])

#calculate coefficient of variation

branch_stats['CV']=(branch_stats['std']/branch_stats['mean'])*100

print(branch_stats)

#which city has highest sales?

#Groupby city and calculate total sales

groupby_city= data.groupby('City')['Total'].sum()

city_with_highest_sales=groupby_city.idxmax()

print(f"The city with highest_sales is :{city_with_highest_sales}")

#which city has lowest sales?

city_with_lowest_sales=groupby_city.idxmin()

print(f"The city with lowest_sales is: {city_with_lowest_sales}")

#Find weekly sales

#Groupby data by week and calculate weekly sales

grouped_week_sales=data.groupby(pd.Grouper(key='Date',freq='W'))['Total'].sum()


print(f'weekly sales is:{grouped_week_sales}')

#Find Monthly sales

#groupby month and calculate monthly sales

grouped_month=data.groupby(data['Date'].dt.to_period('M'))['Total'].sum()

print(f'Monthly sales is:{grouped_month}')

#Bar graph of monthly sales


grouped_month=data.groupby(data['Date'].dt.to_period('M'))['Total'].sum().plot(kind='bar',legend=False)

plt.title('Monthly_sales')

#Find Yearly sales

#group by year and calculate yearly sales

grouped_year=data.groupby(data['Date'].dt.year)['Total'].sum()

print(f'Yearly sales is:{grouped_year}')

#which product line have highest sales?

plt.bar(data['Product line'],data['Total'],color='blue',width=0.4)

plt.xlabel('Product line')

plt.ylabel('Total sales')

plt.title('Product line sales')

plt.xticks(rotation=45)

plt.show()

#Gender Percentage

gender_counts=data['Gender'].value_counts()

gender_counts.plot(kind='pie',autopct='%1.1f%%',colors=['skyblue','salmon'])

plt.title('Gender distribution')

plt.show()

#which payment method does people opt most?

#count payment methods

payment_counts=data['Payment'].value_counts()

#Calculate Percentage

total_payments=len(data)

payment_percentage= (payment_counts/total_payments)*100

#create piechart

plt.figure(figsize=(8,6))

plt.pie(payment_percentage,labels=payment_counts.index,autopct='%1.1f%%', startangle=90)

plt.title('payment method distribution')

plt.axis('equal')

plt.show()

Conclusion:
    
    From above analysis,branch C has highest sales and shows significant variability.
    The city with highest_sales is :Naypyitaw
    The city with lowest_sales is: Mandalay
    January is the month with highest number of sales.
    Product line sales is almost same for all categories.
    Number of female and male is almost same in purchasing.
    Payment method is almost same for all mode of payments.
