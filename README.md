### UdacityProject-DataVisualization
This is the programs repository for Udacity project after lesson 5 (Data Visualization): Communicate Data Findings


#  Loan Data Exploration
## by Xiaohua Chen


## Dataset

This data set contains 113,937 loans with 81 attributes on each loan, including loan amount, borrower rate (or interest rate), current loan status, borrower income, etc. The years span from 2005 to 2014.

The data is hosted at:
https://s3.amazonaws.com/udacity-hosted-downloads/ud651/prosperLoanData.csv.
Documentation of the data fields is provided at:
https://docs.google.com/spreadsheets/d/1gDyi_L4UvIrLTEC6Wri5nbaMmkGmLQBk-Yx3z0XDEtI/edit#gid=0



## Summary of Findings

The dataset contains much more features than I need to conduct the investigation. Starting from 81 attributes, I trimmed it down to 10, through the course of data exploration. 

Features of key interests are: 
* BorrowerRate
* LoanStatus
Borrowing rate ranges from 0 to 0.5 with a multimodal distribution, which peaks at around 0.15 and 0.31.
Loan Status takes the values from: completed, current, chargedoff, defaulted, past due with various periods. In order to facilitate further analysis, Loan status values are consolidated to: completed, current, default, past due. The highest proportion belongs to 'current' loans. About 15% of loans are defaulted.

Features of supporting roles and their properties are: 
* Term: 1, 3 or 5 years. 3 is the most common
* ListingCategory: 'debt consolidation' is the most common category, followed by 'home improvement' and 'business'
* IsBorrowerHomeowner: about half of the loans are by home owners
* CreditScoreRangeLower: mainly distributed from 400 to 880, with peak around 680
* DebtToIncomeRatio: mainly distributed from 0 to 0.8, with peak around 0.18
* StatedMonthlyIncome: mainly distributed from 800 to 12000, with peak around 4000~5000
* LoanOriginalAmount: varies between 1000 to 35000
* MonthlyLoanPayment: varies between 0 to 2252

There are some anomaly data points. StatedMonthlyIncome < 1 dollar, and DebtToIncome ration > 2 are replaced with Nan. Among these variables, MonthlyLoanPayment is highly correlated with LoanOriginalAmount. 

Correlation matrix plot and individual pairplots, for BorrowerRate vs. other variables, show that:
* BorrowerRate is negatively correlated with CreditScore.
* BorrowerRate is negatively correlated with LoanOriginalAmount: this is curious
* BorrowerRate is positively correlated with DebtToIncomeRatio

Pairplots between LoanStatus and other variables show that:
- Completed or Current loans have lower BorrowerRate
- Current loans have higher LoanOriginalAmount
- Current loans have higher MonthlyLoanPayment (consistent with the previous point)
- Default loans have lower CreditScore
- Default loans have lower StatedMonthlyIncome
- Debt consolidation loans are more likely to be in 'current' status, compared to Home improvement or Business loans
- home owners are more likely to have 'current' loan, and less likely to have 'default' or 'completed' loan
- 60 month loans are least likely to be 'completed', while 12 month loans most likely to be 'completed'. 36 month loans are more likely to be 'default' than loans of other terms are.

Investigations on relationships between other variables reveal that:
- Higher LoanOriginalAmount is only possible with higher CreditScore
- CreditScore tends to be higher with homeowner as borrower
- Longer Terms associate with higher Loan Amounts

Multivariate explorations show that:
- When looking within each credit score range, loan amount does not necessarily show negative correlation with interest rate. This means that larger loans does not tend to have lower interest rate, when the effect of credit score is removed.
- Higher income and higher credit score can reduce loan default probability at the same time.
 

## Key Insights for Presentation

The steps of the presentation are:

1. Perform all the data trimming, cleaning and converting at the begining, before going into variable descriptions. 8 variables are retained: Term, LoanStatus, BorrowerRate, IsBorrowerHomeowner, CreditScoreRangeLower, DebtToIncomeRatio, StatedMonthlyIncome, LoanOriginalAmount

2. Illustrate distributions of the key variables 'BorrowerRate', 'LoanStatus', and one supporting variable 'MonthlyIncome'.

3. Correlation matrix map of 'BorrowerRate' and supporting variables suggest correlated variable pairs.

4. BorrowerRate and other variables' relationship:
- BorrowerRate is lower with higher CreditScore
- BorrowerRate is lower with lower DebtToIncomeRatio
- BorrowerRate is lower with higher StatedMonthlyIncome
- BorrowerRate is lower with Home owners 

5. LoanStatus and other variables' relationship:
- Default loans have lower CreditScore
- Default loans have lower StatedMonthlyIncome
- Current loans have higher LoanOriginalAmount

6. Other variables' relationship: How much the Loan Original Amount can be is limited by Credit Score.

7. Loan Default Rate vs. Income and Credit Rating: lower loan-default probability is associated with higher credit score and higher income at the same time.

