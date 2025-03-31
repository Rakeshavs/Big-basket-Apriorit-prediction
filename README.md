
🛒 Apriori Algorithm - Program Explanation
📌 Overview
The Apriori Algorithm is used for Market Basket Analysis, helping businesses understand which products are frequently bought together. This program processes transaction data, applies the Apriori algorithm, and extracts useful association rules.

🔄 Step-by-Step Explanation of the Code
1️⃣ Importing Required Libraries 📚
python
Copy
Edit
import pandas as pd
from mlxtend.frequent_patterns import apriori, association_rules
✔ pandas – Handles and processes data
✔ mlxtend – Provides functions for Apriori & association rules

2️⃣ Loading the Dataset 📂
python
Copy
Edit
data = pd.read_csv("big_basket_transactions.csv")
✔ Loads the dataset containing transactions where each row represents a purchase.

Example dataset:

Transaction ID	Item
1	Milk
1	Bread
2	Milk
2	Cookies
3	Bread
3	Butter
3️⃣ Transforming Data for Apriori 🏗️
python
Copy
Edit
basket = data.pivot_table(index='Transaction ID', columns='Item', aggfunc=lambda x: 1, fill_value=0)
✔ Converts data into a one-hot encoded format where:

1 means the item was bought

0 means it wasn’t

Example transformed data:

Transaction ID	Milk	Bread	Cookies	Butter
1	1	1	0	0
2	1	0	1	0
3	0	1	0	1
4️⃣ Applying the Apriori Algorithm 🔍
python
Copy
Edit
frequent_itemsets = apriori(basket, min_support=0.1, use_colnames=True)
✔ Finds frequent itemsets with a minimum support of 10%.

Example Output:

Items	Support
{Milk}	0.66
{Bread}	0.66
{Milk, Bread}	0.33
5️⃣ Extracting Association Rules 📊
python
Copy
Edit
rules = association_rules(frequent_itemsets, metric="lift", min_threshold=1)
✔ Generates rules based on Lift metric (strength of the association).

Example Output:

Antecedent	Consequent	Support	Confidence	Lift
Milk	Bread	0.33	0.50	1.5
Bread	Butter	0.33	0.50	2.0
Confidence (0.50) → If a customer buys Milk, there’s a 50% chance they also buy Bread.

Lift (1.5) → Buying Milk increases the likelihood of buying Bread by 1.5 times.

6️⃣ Displaying the Final Results 📑
python
Copy
Edit
print(rules[['antecedents', 'consequents', 'support', 'confidence', 'lift']])
✔ Shows the best rules for product recommendations!

🎯 Summary
✅ Loads the transaction dataset
✅ Transforms data into a structured format
✅ Applies Apriori to find frequent itemsets
✅ Extracts rules to understand product associations
✅ Helps businesses make data-driven decisions 📊
