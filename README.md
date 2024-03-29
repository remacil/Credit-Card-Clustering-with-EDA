# Credit Card Customer Segmentation with Agglomerative, K-Means, and K-Medoids

by [Aditya Nugraha](https://github.com/dyt08/), [Dwi Pamuji Bagaskara](https://github.com/DwiPamuji), [Randy Irawani](https://github.com/remacil)

![179932257-b83cf081-d2fa-46cd-9e7e-43ac3ba496a7](https://user-images.githubusercontent.com/99951561/179932968-b78ac0da-50f8-4b23-aa63-a06098dcd804.jpg)


*Image Source: https://www.freepik.com/photos/card-machine*

## Contents

1. [Business Understanding](#business-understanding)
1. [Data Understanding](#data-understanding)
1. [Data Preprocessing](#data-preprocessing)
1. [Modeling](#modeling)
1. [Conclusion & Recommendation](#conclusion-recommendation)

## <a id="business-understanding">Business Understanding</a> 

### Context

Marketing can help businesses increase brand awareness, engagement and sales with promotional campaigns. No matter what area a business focuses on, they can take advantage of all the benefits marketing can offer and expand their reach.

One of method for the marketing team to understand their customer, is by dividing their customer by their characteristic which is called customer segmentation. Customer segmentation is the process by which you divide your customers up based on common characteristics – such as demographics or behaviours, so you can market to those customers more effectively.

In addition, if data about the customers is available, the data science team can help performing a customer segmentation.

### Problem Statement and Goals

The competitive in financial industries are getting harder in the next decade. One of this industry main source of revenue are Interest Income which they could get by giving loan or credit payment facilities to customer. Therefore, the more the credit are given, the more interest they get.

Since the data are collected by every credit activities, the company hope they could get some insight by processing the data. This time, we have a data contains summary of the usage behavior of about 9000 active credit card holders during the last 6 months. We will process this data using unsupervised learning methodology to segmentize the customer by finding a certain pattern in hope we could find some characteristic between each customer segment.

Then we will analyze each segment and plan the marketing approach that work best with each segment. We also give some recommendation for the next if we want to update the model or strategies.

### Analytical Approach

We will do explanatory data analysis and finding some insight from the data. Then we will cluster the data using unsupervised learning with K-Means. After the data is segmented, we will decide the marketing approach for each segment.

### Clustering Method

We will decide the numbers of cluster by using Elbow Method and Silhouette Method. Where in Elbow Method, the number of clusters are decided when the addition of one cluster does not provide significant change in the level of similarity, while in silhouette method, the number of cluster is decided by how close each point in one cluster is to points in the neighboring clusters.

## <a id="data-understanding">Data Understanding</a>

Dataset are obtained from: https://www.kaggle.com/datasets/arjunbhasin2013/ccdata

> "The sample Dataset summarizes the usage behavior of about 9000 active credit card holders during the last 6 months. The file is at a customer level with 18 behavioral variables." 

### Attributes Information

| **Attribute** | **Data Type** | **Description** |
| --- | --- | --- |
| cust_id | Object | Identification of Credit Card holder (Categorical) |
| balance | Float | balance amount left in their account to make purchases |
| balance_frequency | Float | How frequently the balance is updated, score between 0 and 1 (1 = frequently updated, 0 = not frequently updated) |
| purchases | Float | Amount of purchases made from account (oneoff_PURCHASE+installments_purchases) |
| oneoff_purchases | Float | Maximum purchase amount done in one-go |
| installments_purchases | Float | Amount of purchase done in installment |
| cash_advance | Float | Cash in advance given by the user |
| purchases_frequency | Float | How frequently the purchases are being made, score between 0 and 1 (1 = frequently purchased, 0 = not frequently purchased) |
| oneoff_purchases_frequency | Float | How frequently purchases are happening in one-go (1 = frequently purchased, 0 = not frequently purchased) |
| purchases_installments_frequency | Float | How frequently purchases in installments are being done (1 = frequently done, 0 = not frequently done) |
| cash_advance_frequency | Float | How frequently the cash in advance being paid |
| cash_advance_trx | Integer | Number of Transactions made with "Cash in Advanced" |
| purchases_trx | Integer | Number of purchase transactions made |
| credit_limit | Float | Limit of Credit Card for user |
| payments | Float | Amount of payment done by user |
| minimum_payments | Float | minimum amount of payments made by user |
| prc_full_payment | Float | Percent of full payment paid by user |
| tenure | Integer | tenure of credit card service for user in years |

## <a id="data-preprocessing">Data Preprocessing</a>

One of the most important preprocessing steps in a Data Science project. Some of the things we do in this project are as follows:
- Identify outlier, anomaly, duplicates, and missing value. 
- Handling Missing values with the Iterative Imputer. 
- Drop unused attributes such as cust_id, balance, purchases, cash_advance, cash_advance_trx, purchases_trx, credit_limit, payments, minimum_payments, tenure.
- Perform processing on purchases, oneoff_purchases, installments_purchases to get the proportion of each attribute mentioned.

## <a id="modeling">Modeling</a>

### Principal Component Analysis

For the modeling, we decided to use PCA before we clustering. Since PCA could help to reduce the number of feature for easier interpretation and simplify the complex pattern in modeling.

![newplot](https://user-images.githubusercontent.com/99951561/179933192-9d2cbd2e-d6e9-4452-85c6-5398e9cece52.png)

Because 2 features have a significant increase variance with a score of 74.25%, We will use this value in the future so that the feature that was 8 will be reduced to 2.

### Clustering

After that, we will cluster the new feature with several model like Agglomerative Clustering(Ward, Average, and Complete), K-Means (Euclidean), and K-Medoids(Euclidean, Manhattan, Cosine) then compare the result based on some metrics and the number of clusters.

To determine the optimal number of cluster we will use some metrics:
- Elbow Method, for K-Means and K-Medoids only (Which decreased significantly)
- Silhouette Score (Closer to 1 is better)
- Davies Bouldin Score (Closer to 0 is better)
- Calinski Harabasz Score (a high score is desirable)

#### Agglomerative

**Agglomerative** is clustering strategic in hierarchy clustering (clustering techniques form a hierarchy or are based on a certain level so that it resembles a tree structure) starting with each object in a separate cluster and then forming an increasing large clustering.
we use 3 Linkage in Agglomerative : 
 1. **Ward Linkage (sum of square from 2 cluster)** : 
 Instead of measuring the distance directly, Ward analyzes the cluster variance. Ward's is said to be the most suitable method for quantitative variables.
 2. **Average linkage (sum of average or average link)**
Technique is combines clusters according to the average distance of each pair of members in the set between two clusters.
 3.  **Complete linkage (max distance or complete link)**
Technique is combines clusters according to the distance between the furthest members between two clusters.

**Silhouette, Davies Bouldin, and Calinski Harabasz Score:**

![newplot (2)](https://user-images.githubusercontent.com/99951561/179992621-37a2b83e-6318-4e25-99f6-21c4d10c1705.png)

in the plot above we can see the results of the metrics that we use, each of which has the highest value:

**Silhouette Score:**
- Ward: 0.59 on Cluster 8
- Average: 0.61 on Cluster 7
- Complete: 0.57 on Cluster 7

**Davies Bouldin Score:**
- Ward: 0.61 on Cluster 3
- Average: 0.61 on Cluster 3
- Complete: 0.70 on Cluster 4
 
**Calinski Harabasz Score:**
- Ward: 19239 on Cluster 8
- Average: 20532 on Cluster 8
- Complete: 16579 on Cluster 7

#### K-Means

**K-Means** is a partitioning clustering method to separates data into defferent clusters. by itterative partitioning, its clustering is able to minimize the average of distance of each data to its cluster (MacQueen, 1967).

**Elbow Method:**

![newplot (3)](https://user-images.githubusercontent.com/99951561/179992678-0a0b7851-f76e-42ff-8617-344230cba072.png)


At first glance we can segment with 4 or 5 clusters because it is the most significant decrease, this method is very objective so it will use our perspective by also comparing it with other metrics.

**Silhouette, Davies Bouldin, and Calinski Harabasz Score:**

![newplot (4)](https://user-images.githubusercontent.com/99951561/179992759-62bc0973-a89c-4415-a05c-8cda512bf4bd.png)


In this case we decided to use 4 clusters with the assumption that there is a gradual decrease in the more gentle elbow method, the Silhouete score and Calinski Harabasz score are not the highest but sufficient because 4 is the point where the score increases significantly, when viewed from the Boudin Davies score it also becomes the highest scorer of the others.

Each score for the 4 clusters is:
- Elbow Method: 0.279
- Silhouette: 0.59
- Davies Bouldin: 0.60
- Calinski Harabasz: 15797

#### K-Medoids

**K-Medoids**, also known as Partitioning Around Medoids (PAM), is a variant of the K-Means method. It is based on the use of a medoid instead of observations held by each cluster, with the aim of reducing the sensitivity of the resulting partition with respect to the extreme values ​​present in the dataset (Vercellis, 2009).

We use 3 distance metrics : 
1. **Cosine Similarity**: measure of similarity between two sequences of numbers.
1. **Euclidean Distance or Euclidean**: metric is the familiar and straightforward line between two elements or the minimum distance between two objects 
1. **Manhattan Distance**: the distance between two points is the sum of the absolute differences of their Cartesian coordinates. Simply it is the sum of the difference between the x-coordinates and y-coordinates. 

**Elbow Method:**

![newplot (5)](https://user-images.githubusercontent.com/99951561/179992831-9d0a1464-448d-4c4d-b248-53aa7baac130.png)


At first glance we can segment with 3 or 4 clusters  on all distance metrics because this is the most significant decrease, once again note that this method is very objective so will use our perspective by also comparing it to other metrics.

**Silhouette, Davies Bouldin, and Calinski Harabasz Score:**

![newplot (6)](https://user-images.githubusercontent.com/99951561/179992855-554f2d49-f54b-42df-8055-553584d4d12d.png)


Same as kmeans, in this case we decided to use 4 clusters for all distance metrics with the respective assumptions:
- Cosine: it can be seen that the silhouete score is not stable in the 3rd to 7th clusters so we look for the right point before there is instability, namely in 4 clusters, on Davies Bouldin itself is the lowest score compared to others, Calinski Harabasz also looks unstable like in the silhouette score
- Euclidean: on the silhouette, the score that increased the most significantly was in cluster 3 or 4 objectively, on Davies Bouldin the lowest score was in 5 clusters but the decline was very gentle compared to from 3 to 4 clusters. The most significant increase in the score for Calinski Harabasz was also found in 4 clusters.
- Manhattan: on Davies Bouldin it is clear that there is a significant decrease in 3 clusters, but if we look at other metrics, especially on the silhouete, we can also use 4 clusters for this metric.

Scores in 4 clusters for each distance metric will be described below:

Cosine:
- Elbow Method: 0.061
- Silhouette Score: 0.79
- Davies Bouldin Score: 0.60
- Calinski Harabasz Score: 15759

Euclidean:
- Elbow Method: 0.262
- Silhouette Score: 0.59
- Davies Bouldin Score: 0.60
- Calinski Harabasz Score: 15759
 
Manhattan:
- Elbow Method: 0.335
- Silhouette Score: 0.58
- Davies Bouldin Score: 0.61
- Calinski Harabasz Score: 15139

### Final Model

for the end of this project we decided to choose K-Medoids with 4 clusters and metric distance using Cosine because it is the best score compared to others.

![newplot (7)](https://user-images.githubusercontent.com/99951561/179992950-64457a87-5d3c-4a3a-aa4e-d4a91ed5bb2f.png)


Seen in the scatter plot above, the division is done quite neatly with the centroids almost all approaching the busiest group in each cluster.

#### Behavior Cluster Analysis

At this stage, we analyze the behavior of credit card users who are divided based on the clusters that we have obtained in the previous modeling process.

## <a id="conclusion-recommendation">Conclusion and Recommendation</a>

### Cluster 0 (Balance Spender)
#### Characteristic:

- Balance up to 5500
- Love to spend
- Made purchase up to 7200, from total purchases, 72% of it contains one off purchase and 28% of it contains installment purchase
- Have Credit Limit Mosly up to 16000
- Oneoff purchase up to 4900
- Installment purchase up to 2374
- Using cash advance up to 800

#### Analysis:
    
Users in this cluster are users who like to shop using the one-time payment method (one off purchases), we assume users in this cluster use a credit card to make monthly routine payments like as paying for electricity bill, monthly consumption, or other monthly needs. So users in this cluster tend to use credit cards only to delay payment, not to pay in installments. And and our assumption is that users in this cluster also collect credit card points. We assume in customer profil in this cluster is a adults have families.

#### Strategy:
    
1. Since our strategy is made them to use more purchase using installment, we could give some benefit like if they made purchase using credit rather than one off payment, they could obtain some discount, increase their credit card membership level, etc
1. Provide auto debit facilities to users, and provide bonus points or cashback for users who register their auto debit.
1. Collaborating  with service providers or monthly necessities so that they can provide discounts or additional special points for users who make payments using credit cards. For example, working with Perusahaan Listrik Negara (PLN) to provide discounts for monthly electricity bills or purchasing electricity tokens using a credit card
1. Collaborating with service providers or monthly necessities to create a program to pay a lump sum for a certain period which is certainly cheaper than paying monthly with a credit card that can be paid in installments with 0% interest. For example, Collaborating with PLN, for electricity payments, assuming the monthly payment is 1 million. if the payment is direct or lump sum for a period of 1 year only need to pay 11 million. And users can using the lump sum payment installment facility (one off purchases) into installments in 6 months or 12 months with 0% interest
1. Provide the facility of changing from full payment (one off purchases) to installment without additional fees
 
### Cluster 1 (Money Hoarders)

#### Characteristic:

- Balance up to 6000
- Rarely spends money
- Using cash advance up to 5900
- Have Credit limit up to 12750
- Made payments up to 3600

#### Analysis:

This user mostly have a high balance but almost never spends it whether using credit card or not. We could assume this kind of users use their money mostly for investing activities or as saving account.

#### Strategy:

1. This could give marketing team a lead like survey the characteristic of the customer like age(since the more mature they are, usually they rarely spends money) or why they put their money in this account.
1. Collaborating with platforms or securities investment service providers to provide features to top up using a credit card, and provide bonus points or cashback when the user tops up with his credit card.
 
### Cluster 2 (Potential Whale)

#### Characteristics:
- Have Balance up to 4600
- Made purchase up to 2000, 95% of it contains One off purchase
- Using cash advance up to 2500
- Spends alot on One Off purchase rather than installment
- Have credit limit 12300
- Made Payments up to 3400

#### Analysis:

Users in this cluster are users who have moderate belance, users don't like shopping, and users are more dominant using one-off purchases. Our assumption is that users in this cluster are users who have just started setting aside money for investment or securing their assets but still use some of their money to make purchases.
    
#### Strategy:

1. Provide the facility of changing from full payment (one off purchases) to installment without additional fees.
1. This could lead marketing team to check the customer profile whether this type of customer doesn't use the credit facilities due to high interest or any specific reason 

### Cluster 3 (Credit Lovers)

#### Characteristics:

- Have balance up to 3000
- Made purchase up to 2000, 80% of it contains installment purchase
- Made one off purchase up to 120
- Made Installment purchase up to 1800
- Rarely using cash advance
- Have credit limit up to 10000
- Made payment up to 3000

#### Analysis: 

Users in this cluster are users who have a low balance and have a small credit limit. users in this cluster are very fond of shopping and use installment payments, and rarely use full payments. Our assumption is that the users in this cluster are fresh graduate users and just have a credit card, so they have a relatively small limit.

#### Strategy: 

1. Collaborating with various shopping platforms such as several e-commerce platforms by holding a 0% installment program and cashback with a low monimum payments like 50 dollar, to attract the user's attention
2. Collaborating with big fashion brands such as Nike Adidas or Zara, to provide promos for users who use credit cards with installment payments
3. Consider increase the credit limit for customer who already using the credit limit to its fullest but have a good payment and balance.
4. This could lead the marketing team to check the customer profile to check whether the payments are smooth or not.

### Development Recommendations

#### For the Data:

1. Add more data to the dataset for better modeling.
2. We could use realtime dataset for better result.
3. Add more feature related like Credit Card Type(Silver, Gold, Plat), the date they made the transaction (for trend analysis), customer profile (students, worker, etc), age, income user, work experience.

#### For modeling:

1. The cluster result also could be used as a feature or target.
2. The feature we added like (oneoff_proportion, installment purchase, etc) could be used for SPL(Supervices Learneing) Regression to predict a credit limit for new user and SPL Classification for categorize new user to which cluster they are.
