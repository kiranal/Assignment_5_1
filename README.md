# Coupon Acceptance Analysis

## Problem statement 
What factors influece a driver to accept a coupon while driving. Identify patterns, understand what factors influence the driver to accept the coupons.

## Code organization 

### Assignment_5_1          
Git hub repository (https://github.com/kiranal/Assignment_5_1)
### Data/                   
Origninal dataset  from the UCI Machine Learning Repository and was collected via a survey on Amazon Mechanical Turk. coupons.csv 
### Images/                
Visualization of coupon insights
### README.md               
Project overview and documentation
### prompt.ipynb            
Source code 

## Data for analysis
###  Preparation
The dataset was thoroughly examined to ensure its quality and relevance for analysis. Dataset consists of 12685 rows and 26 columns
The data preparation process involved checking for missing values, examining unique values for each column, and removing rows with inconsistent or missing values that could impact the analysis.
Code snippet to analyze the data :
```
for column in data.columns:
    print(f"\nUnique Values in {column}:")
    print(data[column].unique())
```

###  Cleaning
The data cleaning process focused on ensuring the accuracy and consistency of the data. 
Rows with missing values in critical columns were removed to prevent potential biases in the analysis. 
1. Following columns considered for cleaning null values. - 'Bar', 'CoffeeHouse', 'RestaurantLessThan20', 'Restaurant20To50'
2. Removed the car column which is not helping wiht analysis
3. removed the duplicate rows 


### Data for Analysis
The final dataset used for analysis consists of 12115 rows and 25 columns. The data has been cleaned and prepared to ensure its consistency and accuracy for the analysis.

## Analysis 

To understand what influences drivers to accept bar coupons, I conducted a focused analysis using three key visualizations. The goal was to explore how age, bar-going behavior, passenger type, and marital status impact coupon acceptance. Here's how the analysis was conducted:

### Age and bar frequency interaction
I created a heatmap using a cross-tab (bar_cross_tab) between driver age and bar visit frequency, displaying the average coupon acceptance rate in each group.

The heatmap allowed me to visually identify which age groups and bar-going habits were associated with higher acceptance.

![alt text]( https://github.com/kiranal/Assignment_5_1/blob/main/Images/AgeAndFreq.png)

**code snippet**
```
# Create a crosstab of bar frequency vs age group for accepted coupons
bar_cross_tab = pd.crosstab(
    index=bar_coupons[bar_coupons['Y'] == 1]['age'],
    columns=bar_coupons[bar_coupons['Y'] == 1]['Bar']
)

#heat map for age & freq of visit patterns for accepting bar coupons
sns.heatmap(bar_cross_tab, annot=True, cmap='YlGnBu', square=True)

```


### Passenger 
I used a bar plot to compare acceptance rates across different types of passengers: Alone, Partner, Friend(s), and Kid(s).
By calculating the mean acceptance for each group, this plot helped evaluate the role of Passenger in coupon decisions.

![alt text]( https://github.com/kiranal/Assignment_5_1/blob/main/Images/PassangerType.png )

**code snippet**
```
sns.barplot(data=bar_coupons, x='passanger', y='Y', order=['Alone', 'Partner', 'Friend(s)', 'Kid(s)'])
```


### Marital status
A second bar plot was used to visualize acceptance rates across different marital status groups, including Single, Married Partner, Unmarried Partner, Divorced, and Widowed.
![alt text]( https://github.com/kiranal/Assignment_5_1/blob/main/Images/PassangerType.png )

**code snippet**
```
sns.barplot(data=bar_coupons, x='maritalStatus', y='Y', estimator=np.mean)
```
## Hypothesize

Based on the above analysis and visualizations, we can generate the following hypotheses regarding driver behavior and bar coupon acceptance:

1. Drivers who go to bars more than once a month and are under the age of 30 show the highest acceptance rates, suggesting that younger, socially active individuals are more responsive to bar-related offers.
2. In general, frequent bar-goers, regardless of age, are more likely to accept bar coupons compared to those who rarely or never visit bars.
3. Drivers accompanied by friends are more likely to accept bar coupons, indicating that social companionship plays a role in influencing the decision to make spontaneous stops.
4. Single drivers and those in unmarried partnerships tend to accept bar coupons more often than those who are married or widowed, possibly reflecting differences in lifestyle and flexibility.

### Next steps
1. Build a machine learning model to predict coupon acceptance
2. Create an AI agent to push personalized coupons in real-time



