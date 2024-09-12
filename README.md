# Brazil-E-commerce-Olist-Business-Analysis 

## Project Overview:
The Olist dataset comprises data on 100k orders spanning from 2016 to 2018, originating from various marketplaces in Brazil. The dataset's attributes enable comprehensive analysis of orders across multiple facets, encompassing order status, pricing, payment and shipping dynamics, customer location details, product characteristics, and customer reviews.

The primary objectives of this analysis include:

- Understanding customer demographics and purchasing behaviors.
- Analyzing product demand and performance.
- Evaluating Olist's business performance.
- Offering data-driven recommendations to enhance operational efficiency.

## Data Schema (2016.09-2018.09)
![image](https://github.com/user-attachments/assets/898e386e-7466-4c14-b56c-03f53d6a6025)



## Features
- Automated Multilingual Data Translation: Incorporates the GoogleTranslator library to seamlessly translate datasets from Portuguese to English, facilitating analysis and insights.
- Advanced Segment Analysis with Hupping Face: Utilizes the Hupping Face library for in-depth segment analysis to explore customer satisfaction with Olist shopping and drive improvements.
- Python-based Data Analysis and Computation: Employs Python for preliminary dataset analysis and computation, enhancing data processing capabilities.
- Interactive Data Visualization with Power BI: Enables data visualization and exploration through Power BI, providing dynamic and insightful representations of the analyzed data.

## Data Analysis (Python)
```python

# Merge tables and count customers with shopping records
merge = pd.merge(customers, orders, on='customer_id', how='inner')
num_customers = len(merge['customer_id'].unique())
print("Customers with shopping records: ", num_customers)

# Counting Customers with Duplicate Purchases
merge = orders.merge(customers, on='customer_id', how='inner')
duplicate_customers = merge[merge.duplicated(subset='customer_unique_id')]
num_duplicate_customers = len(duplicate_customers['customer_unique_id'].unique())
print("Duplicate Purchasing Customers Count: ", num_duplicate_customers)


# Identifying Customers with Duplicate Purchases
duplicate_customers = merge[merge.duplicated(subset='customer_unique_id', keep=False)]
num_duplicate_orders = len(duplicate_customers)
print("Count of Orders with Duplicate Purchases: ", num_duplicate_orders)

```

Preprocess data in Python for efficient handling of large datasets and complex calculations before visualizing in Power BI, ensuring organized, optimized data for enhanced analysis and visualization workflows.




## Sentiment Analysis (Hugging Face)
```python
import pandas as pd
from transformers import pipeline
from tqdm import tqdm

Load the CSV file into a DataFrame
df = pd.read_csv(r"C:\Users\genhk\Desktop\Gen\final project\csv\order_reviews_dataset.csv", encoding='latin1')

Select the columns for sentiment analysis
data = df[["Eng_review_comment_title", "Eng_review_comment_message"]]

Initialize the sentiment analysis pipeline
sentiment_pipeline = pipeline("sentiment-analysis")

Convert all values to strings
data = data.astype(str)

Perform sentiment analysis on the selected columns
sentiment_results = []
total_samples = len(data)
with tqdm(total=total_samples, desc="Sentiment Analysis") as pbar:
for _, row in data.iterrows():
sentence = ' '.join(row)
result = sentiment_pipeline(sentence)[0]
sentiment_results.append(result)
pbar.update(1)

Create new columns to store the sentiment scores and labels
df["Sentiment Score"] = [result["score"] for result in sentiment_results]
df["Sentiment Label"] = [result["label"] for result in sentiment_results]

Save the updated DataFrame to a new CSV file
df.to_csv("order_review_sentiment.csv", index=False)
```


Hugging Face, a popular NLP library and platform, is used to analyze sentiments in reviews due to discrepancies between review scores and text content. The library assigns scores to classify sentiments as negative, positive, or neutral. For instance, a sentiment labeled as "positive" with a score of 0.999 is categorized as positive, while a score of 0.72 leans towards neutral.




## Overview
![image](https://github.com/user-attachments/assets/25e15b0d-ec23-4168-89db-43f000edc99a)


This page offers a comprehensive view of seller performance metrics, detailing individual seller review scores and category-specific review scores. By examining the review ratings of each seller and the aggregated scores for distinct product categories, businesses can evaluate seller and category performance in relation to customer satisfaction. This analysis enables the identification of top-performing sellers, areas for enhancement, and popular categories based on customer feedback. By facilitating data-driven decisions, this dashboard empowers businesses to optimize seller performance and enhance the overall customer experience.


## Revenue Performance 
![image](https://github.com/user-attachments/assets/46b70c26-5458-40a9-88fd-4dec578141a8)

These key performance indicators (KPIs) offer a comprehensive view of revenue performance across various dimensions: they track the total and average revenue per state, provide insights into revenue distribution among product categories, analyze revenue trends by month, and offer perspective on average freight values in relation to revenue, helping to assess regional sales, product performance, seasonal trends, and cost efficiencies.





## Cancellation Analysis
![image](https://github.com/user-attachments/assets/7505c138-146d-4bad-a00c-ab1ceee8ad4b)

It provides insights into various aspects of order management and customer behavior. It includes a review score distribution to understand customer sentiment, the number of canceled orders by sellers to identify potential issues in fulfillment, analysis of cancellation rates and total canceled orders to gauge overall order health, and a breakdown of canceled orders by product category to pinpoint areas of concern. These metrics collectively offer a comprehensive view of order management efficiency, seller performance, and customer satisfaction levels, aiding in decision-making to improve operational processes and reduce cancellation rates.



## Recency Frequency Monetary
![image](https://github.com/user-attachments/assets/46a11c49-02f3-4bc4-8373-1f291da20f38)

This page focuses on customer segmentation and behavior analysis using Recency, Frequency, and Monetary (RFM) metrics. It includes insights such as average recency, average frequency, and average monetary value of customer transactions. Additionally, it provides details on the number of items per order, customer labels for segmentation, and the distribution of customers across different segments. By leveraging RFM analysis and customer segmentation, businesses can better understand customer behavior, tailor marketing strategies, and enhance customer relationships for improved engagement and retention.



## Return Customer
![image](https://github.com/user-attachments/assets/de78e7c4-a122-45f2-b6b7-ae7b1028df85)

 It shows a comprehensive view of customer-related metrics to drive business decisions and enhance customer experience. It includes analysis on return customers to gauge loyalty, distribution of customers across cities for targeted marketing strategies, total count of return customers for retention efforts, customer type distribution for personalized services, top 10 product categories for inventory optimization, payment value trends over different periods for financial planning, and total revenue figures for overall business performance assessment. These insights collectively offer a holistic view of customer behavior, preferences, and financial performance, aiding in strategic decision-making and customer-centric business strategies.


## Customer Purchase Behavior
![image](https://github.com/user-attachments/assets/a3adeb5a-1f40-4696-8bd0-343908fc7b0d)

This dashboard provides a detailed analysis of customer purchase patterns and delivery metrics to optimize operations and enhance customer satisfaction. It includes the count of repeat purchases to understand customer loyalty, the total average delivery time for efficiency assessment, average delivery time per repeat purchase for segment-specific insights, sum of average repeat purchases by repeat purchase frequency for targeted marketing, count and sum of payment values by product category for strategic inventory management, average days between repeat purchases for customer retention strategies. These metrics collectively offer a comprehensive view of customer behavior, delivery efficiency, and purchasing trends, enabling data-driven decisions to improve operational processes and customer engagement.



## Performance Monitoring Dashboard
![image](https://github.com/user-attachments/assets/10fcdc77-4568-4f19-af28-44b69bf8c90f)

This dashboard provides a detailed breakdown of performance metrics, including order processing time, fulfillment rates, and more, presented through graphs and charts to showcase trends, comparisons, and benchmarks. The analysis interprets this data, identifying areas of strength and weakness to drive informed decision-making and enhance operational performance.

## Delay Analysis and Resolution 
![image](https://github.com/user-attachments/assets/53ff8dbe-dac1-4cea-a7c6-2089f874ed86)

This section focuses on a comprehensive analysis of delay causes within the order processing workflow. It includes root cause examinations of specific workflow segments, exploration of factors contributing to delays such as days, geolocations, product categories, and sellers, visual representations through charts or diagrams to highlight delay points, and actionable recommendations for resolving delays based on identified root causes.


## Sentiment Analysis and Product Feedback 
![image](https://github.com/user-attachments/assets/9d4c5939-45bb-477a-8c40-7eb551447128)

This page provides a visual timeline of negative and positive customer comments to track sentiment trends over time. Additionally, it highlights the top positive and negative products based on customer feedback. By analyzing sentiment changes and identifying key products driving positive and negative feedback, this dashboard enables businesses to understand customer sentiment dynamics and make informed decisions to improve product offerings and customer satisfaction.

## Customer Review Score Analysis
![image](https://github.com/user-attachments/assets/568a37c6-be15-4ee3-807f-8bb1b370a999)

This dashboard focuses on analyzing customer review scores based on order locations and product categories to determine the satisfaction levels associated with different locations and categories. By examining customer sentiment in reviews across various locations and categories, businesses can gain insights into which locations and categories are performing well in terms of customer satisfaction and which areas may require improvement. This analysis enables businesses to identify strengths and weaknesses in specific locations and categories, allowing for targeted strategies to enhance customer satisfaction, product offerings, and overall service quality.


## Seller Performance
![image](https://github.com/user-attachments/assets/03693a96-59a1-4407-beef-0ae03eae9a81)

This page provides an overview of seller performance metrics, including individual seller review scores and category-specific review scores. By analyzing the review scores of each seller and the aggregated review scores for different product categories, businesses can assess the performance of sellers and categories in terms of customer satisfaction. This dashboard enables businesses to identify top-performing sellers, areas for improvement, and popular categories based on customer feedback, facilitating data-driven decisions to enhance seller performance and customer experience.

## Summary
- Shopping Insights:
The peak shopping hours are between 12:00 to 18:00, indicating the most active shopping period.
Sao Paulo has the highest number of shoppers, suggesting a significant customer base in that location.
January records the highest number of purchases, indicating a peak in sales during that month.

- Order Management:
The order cancellation rate is relatively low, with only 625 out of 9941 orders being canceled.
Return customers are limited, with only 2997 individuals, and most customers make single purchases, contributing to 93.62% of revenue.
- Customer Retention:
Customers who make repeat purchases have an average delivery time of 12.32 days, with an average of 50 days between purchases.
There is a low rate of customer retention, indicating a need for strategies to encourage repeat purchases.
Factors Affecting Delays:
Delays in delivery may be influenced by specific days, geolocation, product category, and seller, suggesting areas for improvement in logistics and operations.
- Customer Sentiment:
Approximately 60% of comments are positive, indicating room for improvement in addressing customer concerns and enhancing overall satisfaction levels.
This analysis provides valuable insights into customer behavior, shopping patterns, order management, customer retention, delivery efficiency, and customer sentiment. Leveraging these insights can help optimize operations, enhance customer experience, and drive business growth.
