# snapchat-2018-ad-impressions

## Background and Intro

Social media advertising is a growing industry. Given the importance of social media in a consumer’s daily life, over [90% of advertisers are willing to advertise on social media.](https://www.statista.com/statistics/736971/social-media-ad-spend-usa/) By 2022, companies are projected to spend over [$56 billion](https://www.statista.com/statistics/736971/social-media-ad-spend-usa/) on social media advertising. This trend is also reflected in the political sphere. In 2016, political candidates spent [$1.4 billion](https://www.americanbar.org/groups/crsj/publications/human_rights_magazine_home/voting-in-2020/political-advertising-on-social-media-platforms/) on social media advertising, compared to just $22.5 million just 8 years prior. Given this heavy investment in social media advertising, political campaigns need to ensure that they are optimizing their ad approach for the greatest reach. 

## Business Question

What factors most heavily impact a political ad’s ability to gain impressions on Snapchat?

## Data Sources

All data was extracted from Snap’s [database of its political advertisements in 2018.](https://www.snap.com/en-US/political-ads) [This is the raw dataset.](https://github.com/vchen19/snapchat-2018-ad-impressions/blob/main/PoliticalAds.csv)

## Methods

More detailed methods are listed [here](https://github.com/vchen19/snapchat-2018-ad-impressions/blob/main/Detailed_methods.md). 

### Single Linear Regression

Single linear regression analysis was used to measure the relationship between ad spend in USD (independent variable) and number of impressions (dependent variable). All ad spend entries were converted to USD using nested IF statements. Then, impressions were plotted against ad spend. To attempt to improve the R-squared value, outliers in both ad spend and impressions were found using the [1.5 IQR rule](https://www.thoughtco.com/what-is-the-interquartile-range-rule-3126244). These entries were eliminated from the data and plotted in a separate graph. 

### Multiple Linear Regression

Multiple linear regression analysis was used to measure the impact that ad spend, time of ad run, and whether or not the ad was in the United States had on the number of impressions. To find the amount of time that the ad ran, the end date was subtracted from the start date (both columns had to be edited to remove the “Z” at the end using Excel’s SUBSTITUTE function). Ad entries were assigned a “1” if the Country Code was “united states” and “0” if the Country Code was not “united states”. The Regression tool in the Data Analytics add-on was used to determine how these factors impact impressions. 

## Results

![Single Linear Regression](https://github.com/vchen19/snapchat-2018-ad-impressions/blob/main/Single%20Linear%20Regression.png)
![Multiple Linear Regression](https://github.com/vchen19/snapchat-2018-ad-impressions/blob/main/Multiple%20Linear%20Regression.png)

Even after the outliers were removed, the R-squared value for impressions vs. ad spend was only 0.6896, though there is visually a clear positive trend between the two variables. This shows that while ad spend may be important in predicting impressions, it does not tell the full story. 

On the other hand, the multiple linear regression showed very low P-values (less than 0.05) when analyzing the impact of ad spend, time running, and country on impressions. This shows that increasing ad spend and amount of time running will increase impressions, while being in the United States will decrease impressions.

This shows that we can predict impressions based on the equation __impressions = 108885.39 + 344.55*(ad spend in USD) + 4291.67*(time running) - 263180.76*(whether or not US)__.

## Discussion

Multiple regression analysis shows that the amount of time that the ad runs and money spent on the ad have a positive impact on impressions, while the ad being from the United States appears to have a negative impact on impressions. This is useful for companies as proof that these factors have a significant impact on an ad’s success. The next steps would be to analyze more closely how these factors impact the number of impressions. For example, could it eventually be cost-ineffective to run an ad for too long? Additionally, the ads from this dataset are overwhelmingly from the United States, which could have led to skewed results in this category. In the future, it would be interesting to analyze data among all years so that the dataset is larger and the potential of the different sample sizes to skew the data is smaller.

## *NEW* Python Analysis

After analyzing political advertisement impressions on Snapchat using Excel, I performed a similar analysis in Python. By taking advantage of the enhanced visualization techniques available in Plotly, we are able to see the relationships between multiple variables in a single plot: 

![Unzoomed Impressions](https://github.com/vchen19/snapchat-2018-ad-impressions/blob/main/Unzoomed%20Impressions.png)

In this figure, it is difficult to see general trends because there are outliers. Plotly allows figures to be viewed dynamically, meaning that we can zoom in on the plot to get a better sense of what the trends are: 

![Zoomed Impressions](https://github.com/vchen19/snapchat-2018-ad-impressions/blob/main/Zoomed%20Impressions.png)

From this figure, it is a bit easier to make guesses about what the relationships between variables are. For example, it is more clear that there are larger bubbles in the upper portion of the graph, indicating that there could be a positive relationship between length of ad run and impressions. Additionally, there is a small cluster of red/orange bubbles that appear to sit above the line of best fit, indicating that there could be a positive relationship between whether or not an ad runs in Canada and the number of impressions. I tested this hypothesis with a multiple regression in Python: 

![Python Multiple Regression](https://github.com/vchen19/snapchat-2018-ad-impressions/blob/main/Python%20Multiple%20Regression.png)

Spend and time running predict impressions positively and strongly, as given by their positive coefficients and low p-values. While my guess that an ad that runs in Canada is likely to have more impressions seems to be reflected by its positive coefficient, its p-value is rather high at 0.483. This indicates to me that this correlation is not strong enough to say that there is definitively a relationship between an ad running in Canada and the number of impressions.

Overall, there were several ways that Python was helpful in this analysis. It simplified some of the data cleaning by having a built-in function to drop data points with missing values. The dynamic viewing option of Plotly was very helpful, as you don't have to manually change axes and you can see the statistics of each data point by hovering over it. This is helpful for political campaigns to gain a general sense of what trends are outside of outliers. Importantly, Python allowed me to easily incorporate many variables into one plot with the size and color options. This is helpful for political campaigns that want to make hypotheses but don't know where to start. The ability to view multiple variables in one plot, compared to the ability to only view two variables in Excel, allows campaigns to make guesses about what factors might best increase impressions without having to run through the multiple regressions for all possible combinations of factors. With regards to the findings of this project, political campaigns might be able to use 
