# Credit Card Fraud Detection

So, in this project, the main goal was to figure out if we could identify fraudulent credit card transactions. The dataset we worked with had about 284,807 transactions, and only 492 of those were fraud. That’s less than 0.2%, so we were dealing with a very imbalanced dataset, which was the first big challenge.

## How I Approached It

### Understanding the Data

First, I took a closer look at the data. It had features like Time (the number of seconds since the first transaction), Amount (transaction value), and V1 to V28 (these are PCA-transformed features, so they’re a bit abstract but useful for modeling). The target variable, Class, told us whether a transaction was legitimate (0) or fraudulent (1).

The class distribution was heavily skewed toward legitimate transactions. To make sure this didn’t bias the model, I needed to address it during preprocessing.

### Exploratory Data Analysis (EDA)

For the analysis part, I focused on spotting trends or differences between legitimate and fraudulent transactions:

**1. Transaction Amounts:**
Fraudulent transactions tended to have smaller amounts, with most below $100. In contrast, legitimate transactions had a wider range.

**2. Transaction Timing:**
There didn’t seem to be any clear pattern in fraud based on the time of day or the timeline overall.

**3. Class Distribution:**
Legitimate transactions absolutely dominated, so balancing the data was clearly going to be a key step.

### Data Preprocessing

To handle the imbalance, I used under-sampling, where I randomly sampled legitimate transactions to match the number of fraudulent ones. This gave me a balanced dataset of 984 transactions (492 fraud and 492 legitimate).

Next, I split the data into training and testing sets (80/20 split). I also ensured the split was stratified, so both sets had the same proportion of fraud and legitimate transactions.

### Building the Model

For the modeling, I started with Logistic Regression. It’s a simple and interpretable model, and it’s a good first step to understand how well the data works for classification. After training, I checked the accuracy on both the training and testing sets:

- Training Accuracy: ~93.8%
- Testing Accuracy: ~91.9%

### Model Performance

The model did a good job overall. Here’s a breakdown:

- It correctly identified 94 fraudulent transactions out of 100 in the test set (88% recall).
- It also flagged 3 legitimate transactions as fraud, which isn’t perfect but is acceptable for a first attempt.

The precision and recall scores were balanced, so it wasn’t overly focused on either avoiding false positives or false negatives.

## Key Takeaways

**1. Fraud Patterns:** Fraudulent transactions generally involved lower amounts, which aligns with what we’d expect—fraudsters often try smaller amounts to avoid detection.

**2. Balancing the Data:** Under-sampling made a big difference in ensuring the model wasn’t biased toward predicting "legitimate" all the time. Without it, the model would have achieved high accuracy simply by ignoring fraud entirely.

**3. Simple Models Can Work:** Logistic Regression handled the task pretty well for a first attempt. However, it’s worth trying more advanced models for better results.

## Limitations

One limitation of under-sampling is that it discards a lot of legitimate transactions, which might cause us to lose valuable insights. Another point is that logistic regression might not capture complex patterns in the data. Something like Random Forests or Gradient Boosting would likely perform better.

## What I’d Do Next
1. Try more advanced models like Random Forest or XGBoost to see if we can improve precision and recall further.

2. Use oversampling techniques like SMOTE instead of under-sampling, so we don’t lose any legitimate data.
3. Add features like transaction frequency or merchant categories to give the model more context—it’s possible that these could improve detection.

## Final Thoughts

Overall, the project was a success. We’ve built a baseline model that does a good job identifying fraud, and there’s a clear path forward for improving it. It’s an important problem to solve since even a small percentage of fraudulent transactions can add up to significant financial losses. This was a solid first step, and with more work, we could deploy this in a real-world system for monitoring transactions in real time.
