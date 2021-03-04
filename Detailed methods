# Detailed methods

Copy and paste relevant columns (Currency Code, Spend, Impressions, StartDate, EndDate, and CountryCode) in a new tab called “Relevant Columns.”

## Single Regression

In cell N1, type the word “Unique”. 
In cell N2, type the equation =INDEX(A2:A660,MATCH(0,COUNTIF($N$1:N1,A2:A660),0)). A2:A660 should be the column for currency. Hit Ctrl+Shift+Enter. This finds all the unique currencies in the dataset.
Drag the equation from N2 downward until you no longer see unique currency values (you might see 0 or #VALUE or another error).
Insert a new column to the right of the column “Spend.” Label it “Ad Spend in USD.”
Use the unique values to write a nested IF statement for this column to convert the ad spend to USD. The equation should look like this: =IF(A2="USD",B2, IF(A2="CAD", B2*0.79, IF(A2="EUR", B2*1.21, IF(A2="GBP", B2*1.39, IF(A2="AUD", B2*0.77))))). 
Drag the equation down through the dataset.
Copy and paste Ad Spend in USD and Impressions into a new tab called Single Linear Regression.
Find the quartile boundaries for Impressions using the QUARTILE function in Excel. 
Subtract the third quartile from the first quartile to find the IQR. 
Add 1.5 times the IQR to the third quartile to find the upper boundary, and subtract 1.5 times the IQR from the first quartile to find the boundaries.
In a new column called “Impressions Outlier?”, use an IF statement to determine whether or not this number of impressions is an outlier. The equation should look like this: =IF(A2>$H$21, "yes", "no") (the lower boundary is neglected because it is negative). 
Repeat steps 9-12 for Ad Spend outliers.
In a new column called “Either outlier?”, use an if statement to determine if either the ad spend or the impressions of an ad are outliers in their category. The equation should look like this: =IF(OR(C2="yes", D2="yes"), "yes", "no").
Plot all impressions against all ad spend, showing a trendline, trendline equation, and R-squared value.
Sort the data sheet by the “Either outlier?” column.
In a new graph, plot only the data points that have “no” in the “Either outlier?” column. Show a trendline, trendline equation, and R-squared value.

## Multiple Regression

Insert two new columns next to EndDate in the Relevant Columns tab.
Use the equation =SUBSTITUTE(E2, "Z", "") in the first new column to cut off the “Z” from the “StartDate” values. Drag the equation down. Do the same thing for “EndDate” values in the second new column. Call these two columns “StartDateNew” and “EndDateNew”. 
Insert a new column called “Time Running.”
In this column, subtract the StartDateNew value from the EndDateNew value. Drag this equation down. This gives you the time in between the dates in days.
Insert a column to the right of CountryCode called “united states.” 
Write an IF statement that determines if the CountryCode is “united states” or not. The equation should look like this: =IF($J2=K$1, 1, 0). 
Copy and paste the columns “Ad Spend in USD,” “Time Running”, “united states”, and “Impressions” into a new tab called “Multiple Regression Columns.”
Sort by “Time Running”.
Delete the values with #VALUE in “Time Running.”
Use the Regression tool in the Data Analysis add-on to perform Multiple Linear Regression on this dataset. Check the “labels” option, and write the analysis into a tab called “Multiple Regression Analysis.”
