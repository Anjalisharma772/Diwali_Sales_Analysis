import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
df=pd.read_csv(r'Diwali Sales Data.csv')
print(df.head())
df.info()
df.shape
#drop unrelated/blank columns
df.drop(['Status','unnamed1'],axis=1,inplace=True)
df.shape

pd.isnull(df)
pd.isnull(df).sum()
df.shape

#drop null values
df.dropna(inplace=True)
df.shape
#change data type
df['Amount']= df['Amount'].astype('int')
df['Amount'].dtypes
df.columns
#rename column
df.rename(columns={'Marital_Status':'Shaadi'})
#use describe() method returns discription of dataframes (i.e. count,std,mean,etc)
df.describe
#use decribe for specific columns
df[['Age','Orders','Amount']].describe()
                                     #***************Exploratory Data Analysis****************************#

                                                              ##GENDER##


df.columns
ax=sns.countplot(x='Gender',data=df)
for bars in ax.containers:
    ax.bar_label(bars)

df.groupby(['Gender'],as_index=False)['Amount'].sum().sort_values(by='Amount',ascending=False)

sales_gen=df.groupby(['Gender'],as_index=False)['Amount'].sum().sort_values(by='Amount',ascending=False)
sns.barplot(x='Gender',y='Amount',data=sales_gen)


#From the above graphs we can see that buyers are females and even the purchasing power of feemales are greater than men
                                                     ##AGE##
ax=sns.countplot(data=df,x='Age Group',hue='Gender')
for bars in ax.containers:
    ax.bar_label(bars)

#Frrom the graph we can se that most of the buyers are of age group between 26-35 years female 
                                                              ##STATE##

#total number of Orders from top 10 states

sales_state=df.groupby(['State'],as_index=False)['Orders'].sum().sort_values(by='Orders',ascending=False).head(10)

sns.set(rc={'figure.figsize':(15,5)})
sns.barplot(data=sales_state,x='State',y='Orders')

#total number of amount/sales  from top 10 states

sales_state=df.groupby(['State'],as_index=False)['Amount'].sum().sort_values(by='Amount',ascending=False).head(10)

sns.set(rc={'figure.figsize':(15,5)})
sns.barplot(data=sales_state,x='State',y='Amount')
#from the above graphs we can see that unexpectedly most of the orders are from Uttar Pradesh,Maharashtra and Karnataka respectively. 
                                              ##MARITAL STATUS##  

ax=sns.countplot(data=df,x='Marital_Status')
sns.set(rc={'figure.figsize':(7,5)})

for bars in ax.containers:
    ax.bar_label(bars)
    sales_state=df.groupby(['Marital_Status','Gender'],as_index=False)['Amount'].sum().sort_values(by='Amount',ascending=False)
sns.set(rc={'figure.figsize':(6,5)})
sns.barplot(data=sales_state,x='Marital_Status', y='Amount',hue='Gender')
#From the above we can see that most of the buyers are married(womens) and they have high purchasing power.
                                                          ##OCCUPATION##

sns.set(rc={'figure.figsize':(20,5)})
ax=sns.countplot(data=df,x='Occupation')

for bars in ax.containers:
    ax.bar_label(bars)
    sales_state=df.groupby(['Occupation'],as_index=False)['Amount'].sum().sort_values(by='Amount',ascending=False)
sns.set(rc={'figure.figsize':(20,5)})
sns.barplot(data=sales_state,x='Occupation', y='Amount')
#from the above graph we can see that most of the buyers are grom IT,Healthcare and Acviation.
df.columns
                                                          ##PRODUCT CATEGORY##


sns.set(rc={'figure.figsize':(20,5)})
ax=sns.countplot(data=df,x='Product_Category')

for bars in ax.containers:
    ax.bar_label(bars)

    ales_state=df.groupby(['Product_Category'],as_index=False)['Amount'].sum().sort_values(by='Amount',ascending=False).head(10)
sns.set(rc={'figure.figsize':(22,8)})
sns.barplot(data=sales_state,x='Product_Category', y='Amount')
#From the above graph we can see that most of the sold products are from food ,clothing and Electronic Category.
                                                #***************CONCLUSION****************#


#Married Women of Age group 26-35 Years From  UP, Maharashtra and Karnataka ,Working in IT,HealthCare and Aviation are more likely to buy Products from Food,Clothing and Electronic Category.

                                             
