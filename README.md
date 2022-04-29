[<img src="https://img.shields.io/badge/Linkedin-%230A66C2.svg?&sflat&logo=linkedin&logoColor=white" alt="Linkedin profile link button" height="20" width="70" />](https://www.linkedin.com/in/melodyyip/) &emsp;[<img src="https://img.shields.io/badge/Medium-12100E?style=flat&logo=medium&logoColor=white" alt="View in Medium" height="20" width="70" />](https://medium.com/@melodyyip515_/rfm-customer-segmentation-using-python-1a1865c6e7cb) &emsp;[<img src="https://img.shields.io/badge/Tableau-%23ff4d4d.svg?&sflat&logo=tableau&logoColor=white" alt="Tableau profile link button" height="20" width="70" >](https://public.tableau.com/app/profile/yip.hoi.ching#!/?newProfile=&activeTab=0) &emsp; [<img src="https://img.shields.io/badge/Github Blog-%23181717.svg?&style=flat&logo=github&logoColor=white" alt="Github profile link button" height="20" width="90" alt="Github Blog Button"/>](https://melodyyip.github.io/RFM_UCLonlineStore/) 


# RFM Customer Segmentation using Python
Analyzing Customer Segmentation in Online Retail Datasets with Python, including cohort analysis, understanding purchase patterns, and cluster analysis with RFM.

![alt text](https://d35fo82fjcw0y8.cloudfront.net/2018/03/01013239/Header-e1551869702205.png)

Getting started
In the following analysis, I am going to use the Online Retail Data Set, which was obtained from the UCI Machine Learning repository. The link to the data can be found here.
In this article, I am going to write about how to carry out customer segmentation and RFM analysis on online retail data using python.
Data
This data set contains all of the transactions recorded for an online retailer based and registered in the UK between 2009–12–01 and 2011–12–09. The retailer specializes in all-occasion gift items. Most of the retailer’s customers are wholesalers.
Column Descriptions

<br> 

| Column Name | Description | Data Type |
|:--|:--|:--|
| InvoiceNo | Invoice number.If this code starts with letter 'c', it indicates a cancellation. | Nominal, a 6-digit integral number uniquely assigned to each transaction |
| StockCode | Product (item) code | Nominal, a 5-digit integral number uniquely assigned to each distinct product |
| Description | Product (item) name. | Nominal |
| Quantity | The quantities of each product (item) per transaction. | Numeric |
| InvoiceDate | Invice Date and time | Numeric, the day and time when each transaction was generated |
| UnitPrice | Unit price | Numeric, Product price per unit in sterling  |
| CustomerID | Customer number | Nominal, a 5-digit integral number uniquely assigned to each customer |
| Country | Country name | Nominal, the name of the country where each customer reside |


<br>

### Plan
1. Reading data and preprocessing
2. Create Recency Frequency Monetary (RFM) table
3. Model — Clustering with K-means algorithm
4. Interpret the result

### Step 1: Reading data and preprocessing

After downloading the csv file, we can load it into a Pandas dataframe using the pandas.read_csv function.
We need to make sure the data is clean before starting your analysis. As a reminder, we should check for:
- Duplicate records
- Consistent formatting
- Missing values
- Obviously wrong values

I am not going to show the step here, you can check my GitHub for this part.
Check my GitHub to took a look at all my projects🍀

### Step 2: Create Recency Frequency Monetary (RFM) table
![alt text](https://d35fo82fjcw0y8.cloudfront.net/2018/03/01013508/Incontent_image.png)

RFM is a basic customer segmentation algorithm based on their purchasing behavior. The behavior is identified by using only three customer data points:

Recency: the recency of purchase/ How many days ago was their last purchase?

Frequency: the frequency of purchases/ total number of purchases/How many times has the customer purchased from our store?

Monetary: the mean monetary value of each purchase/the amount they have spent/How much has this customer spent? Again limit to last two years — or take all time

The RFM Analysis will help the businesses to segment their customer base into different homogenous groups so that they can engage with each group with different targeted marketing strategies. Sometime RMF is also used to identify the High-Value Customers (HVCs).

Before we get into the process, I will give you a brief on what kind of steps we will get.

![alt text](https://miro.medium.com/max/690/1*x5miJTjJqo5t1FORrU8fIg.png)

#### Manage Skewness and Scaling
We have to make sure that the data meet these assumptions:

The data should meet assumptions where the variables are not skewed and have the same mean and variance.

Because of that, we have to manage the skewness of the variables.Here are the visualizations of each variable.

![alt text](https://miro.medium.com/max/1400/1*uCn2Tjun3qaXy2iaD7qY4Q.png)

As we can see from above, we have to transform the data, so it has a more symmetrical form. There are some methods that we can use to manage the skewness:
- log transformation
- square root transformation
- box-cox transformation Note: We can use the transformation if and only if the variable only has positive values.

![alt text](https://miro.medium.com/max/1400/1*l1kSlI8M-gvpeSBc-GfSEg.png)

Based on that calculation, we will utilize variables that use box-cox transformations. Except for the MonetaryValue variable because the variable includes negative values. To handle this variable, we can use cubic root transformation to the data.


![alt text](https://miro.medium.com/max/1256/1*QkO5FSr3uQuOdYFN37czrQ.png)

Each variable don’t have the same mean and variance. We have to normalize it. To normalize, we can use StandardScaler object from scikit-learn library to do it.

![alt text](https://miro.medium.com/max/456/1*k8h-YDVDumN8NGZBQ-g9Tg.png)

Finally, we can do clustering using that data.

### Step 3 Model — Clustering with K-means algorithm
To make segmentation from the data, we can use the K-Means algorithm to do this.
K-Means algorithm is an unsupervised learning algorithm that uses the geometrical principle to determine which cluster belongs to the data. By determine each centroid, we calculate the distance to each centroid. Each data belongs to a centroid if it has the smallest distance from the other. It repeats until the next total of the distance doesn’t have significant changes than before.

#### Determine the Optimal K
To make our clustering reach its maximum performance, we have to determine which hyperparameter fits to the data. To determine which hyperparameter is the best for our model and data, we can use the elbow method to decide.


![alt text](https://miro.medium.com/max/1400/1*Pz95GIu7kA_XWZ6epIcwWg.png)

The x-axis is the value of the k, and the y-axis is the SSE value of the data. We will take the best parameter by looking at where the k-value will have a linear trend on the next consecutive k. From the above plot, the k-value of 4 is the best hyperparameter for our model because the next k-value tend to have a linear trend.

### Fit the model

![alt text](https://miro.medium.com/max/582/1*qRuoB2-3xusETy0wlOMgVg.png)

### Check the full project here [<img src="https://img.shields.io/badge/Medium-12100E?style=flat&logo=medium&logoColor=white" alt="View in Medium" height="20" width="70" />](https://medium.com/@melodyyip515_/rfm-customer-segmentation-using-python-1a1865c6e7cb)  [<img src="https://img.shields.io/badge/Github Blog-%23181717.svg?&style=flat&logo=github&logoColor=white" alt="Github profile link button" height="20" width="90" alt="Github Blog Button"/>](https://melodyyip.github.io/RFM_UCLonlineStore/) 

### Interpret the result

![alt text](https://miro.medium.com/max/700/1*8lbXMy6fpCL5mS1_xqmD8Q.png)

