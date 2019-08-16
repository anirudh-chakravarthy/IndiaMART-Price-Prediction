# Price Range Prediction
**Problem**: Provide a working prototype solution to gauge the appropriate unit wise price range for the 3 categories in the dataset.

**Language**: Python (as a Jupyter notebook)

By:
1. Anirudh Chakravarthy
2. Divyam Goel

## Idea
Since the problem statement requires an accurate average price range for each good, we decided to eliminate the extreme points i.e outliers. For each unit of measurement for the good, outliers are detected in it's distribution. After removing the outliers, we are now left with the "*average*" points centered about the mean, which give us a better representation of the data and help us get an accurate estimate.

## Algorithm Used
General outlier detection algorithms use a Z-score based approach. This is a very common approach, but this is known to be misleading as desribed [here](https://www.itl.nist.gov/div898/handbook/eda/section3/eda35h.htm). The Modified Z-score, on the other hand, is known to be a more robust statistic for outlier detection. It gives a more resilient measure despite the presence of outliers, making it easier to isolate these points.

```
Modified Z score = 0.6745 * (xi − x̃ ) / MAD
where x̃ denotes the median and MAD denotes the median absolute deviation.
```

We examined 3 measures: Z-score, Trimmed Z-score and Modified Z-score, where points have a score greater than a pre-defined threshold are identified as outliers and removed.. With the given data, we observed that the modified Z-score enforces a stricter condition for a point to be classified as an outlier. If a more lenient condition is required, the trimmed Z-score is preferable. Our outlier detection algorithm is based on the **Modified Z-score**.

## Methodology
For each unit of measurement, a list is maintained. The similar entries were manually identified and were added to the corresponding lists. This task is extremely tedious for large dataset, and can be scaled using Natural Language Processing (NLP) based applications. Common lists are maintained for all items for each unit of measurement encountered. Across each measurement unit, the outlers are identified using the modified Z-score calculation, and removed. The remaining data represent the average for the category, and the maximum and minimum are extracted from these values.

When we will have to apply our model in a real-world situation, the Z-score based approach may not be the most effective. For large datasets involving a lot of noise, this approach will not work well. Instead, we will then adopt a Machine Learning based approach. For this unsupervised outlier detection task, we are considering the use [Density-based spatial clustering of applications with noise (DBSCAN) Clustering](https://towardsdatascience.com/how-dbscan-works-and-why-should-i-use-it-443b4a191c80) algorithm. This approach is density based, making it better for scaling.

Our target is to create a user-friendly interface where the customer, after choosing the desired item, can choose from a list of available units. The user will then be shown the price range of the product in the selected unit, which will help in making more informed purchases based on the relative pricing and quality. As a leader in the e-commerce market, this feature will help IndiaMART consolidate its position over competitors by giving customers insights.

## Assumptions
Few assumptions which we made were:

1. The price distribution is assumed to be roughly normal. This was made after plotting the price distribution as a Boxplot, in which majority of entries were mean-centric. Z-score based algorithms tend to work better under these conditions.
2. 'Onwards' is regarded one piece, 'Pair piece' is treated under as a pair and '10-10000' is assumed to be sold as 10 pieces.
3. Prices listed in the unit of measurement are ignored. For example, price for '1000 per unit' is listed as 1300. Nevertheless, we add it in the 'Unit' list of measures and 1300 is the price used for outlier detection.

**NOTE**: Interconversions between similar units of measurement (eg. Gram and Kilogram, Feet and inches etc) has not been handled in this submission. We plan to incorporate this as a part of the final product.

