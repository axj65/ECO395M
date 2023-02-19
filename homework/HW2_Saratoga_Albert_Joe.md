## 1. Saratoga House Prices

<br/>

### a. Linear Model to Predict Price

<br/>

The goal of this exercise is to build a linear model with the lowest
RMSE. The first thing to do is to explore the data in order to guide the
initial selection of variables for the model. You can find these plots
in Appendix 1. I will show three models in this exercise. The first is
the model from class, used as a reference. The second is a model with
hand-selected variables. The third is a stepwise regression model with
all the varialbes included in the second model and their two-way
interactions.

<br/>

<br/>

The first model is the medium model from class to use as a reference and
consists of the following:

    ## lm(formula = price ~ lotSize + age + livingArea + bedrooms + 
    ##     fireplaces + bathrooms + rooms + heating + fuel + centralAir, 
    ##     data = SaratogaHouses)

<br/>

The second model is a model of my creation using exploratory data
analysis and tinkering with the formula. This model is also used as a
starting point for the stepwise regrsesion in the third model. In this
model, I did not include ‘newConstruction’ as it is captured in the
‘age’ variable. I also did not include ‘sewer’ as the boxplot showed no
noticeable affect on price. The second model consists of the following:

    ## lm(formula = price ~ lotSize + age + landValue + livingArea + 
    ##     pctCollege + bedrooms + fireplaces + bathrooms + rooms + 
    ##     heating + fuel + waterfront + centralAir, data = SaratogaHouses)

<br/>

The third model runs stepwise regression with all the variables from the
second model and their 2-way interactions. The result of the stepwise
regression results in the following formula:

    ## lm(formula = price ~ lotSize + age + landValue + livingArea + 
    ##     pctCollege + bedrooms + fireplaces + bathrooms + rooms + 
    ##     heating + fuel + waterfront + centralAir + livingArea:centralAir + 
    ##     landValue:livingArea + age:landValue + livingArea:fuel + 
    ##     bathrooms:heating + landValue:pctCollege + pctCollege:fireplaces + 
    ##     livingArea:fireplaces + bedrooms:fireplaces + landValue:fireplaces + 
    ##     landValue:bathrooms + fireplaces:waterfront + lotSize:waterfront + 
    ##     fuel:centralAir + age:centralAir + age:pctCollege + lotSize:age + 
    ##     livingArea:pctCollege + lotSize:landValue + landValue:fuel + 
    ##     age:bathrooms + rooms:heating + bedrooms:heating, data = SaratogaHouses)

<br/>

I now use K-fold cross validation (5 folds) to compare all the models.
The following shows the average RMSE for the 3 models:

    ## Model 1 (Medium Linear Model)- Mean RMSE: 66907.27

    ## Model 2 (Hand Selected Linear Model)- Mean RMSE: 59378.08

    ## Model 3 (Stepwise Linear Model)- Mean RMSE: 57702.23

<br/>

### b. KNN Model to Predict Price

<br/>

In order to conduct KNN, I first used my exploratory data analysis plots
to guide selection of initial variables. I then used Z-score scaling to
scale all the parameters. Lastly, I added and removed variables to test
which models returned the lowest RMSE. I also found that the optimal k
value for KNN Regression in this model was k=9.

<br/>

    ## Using k=9 and K-fold cross validation with 5 folds, I got an average RMSE of: 61841.08

<br/>

### c. Tax Authority Report

<br/>

Overall, the Stepwise Regression Model performed the best in terms of
the root mean-squared error (RMSE) with an average RMSE of 57702.23. A
hand-selected linear model without any interactions placed second with
an average RMSE of 59378.08. The K-Nearest Neighbors (KNN) Regression
performed the worst with an average RMSE of 60802.39. So what do these
results mean for tax purposes?

<br/>

If the tax authority wants the most accurate prediction for property
prices, the Stepwise Regression Model clearly outperforms the other
models. However, this model is hardly interpretable due to the many
interactions among the various attributes of the home. When homeowners
protest the value of their home in order to lower property taxes, this
model would be extremely difficult to explain to the court authorities
determining whether to decrease the value of a home. Consequently, I
recommend doing further analysis on and possibly using the hand-selected
linear model. The difference between the average RMSE is only
approximately 1700, whereas the decrease in property values after a
homeowner protests have sometimes been greater than 50,000. I purposely
hand-selected a model without transformations and interactions because
this model is highly interpretable. In other words, the tax authority
can point to specific aspects of the home and state the aggregate affect
of the various aspects of the home on the price. However, I would need
to do more analysis in regards to the assumptions of linearity,
independence, homoscedasticity, and normality. At this point in the
analysis, the KNN model has the best interpretability as one can just
say we used the following variables and chose the houses that most
resembled the homeowner’s house in those aspects. In short, use the
stepwise model if the only goal is to lower RMSE. Look more into the
hand selected model if the goal is to know the affect of each parameter
of the house price. Use KNN if the model needs to be interpretable and
is needed immediately to evaluate home prices.

<br/>

Lastly, I do recommend collecting additional data as this will allow for
better models and lower RMSEs. In particular, I noticed that there is no
neighborhood/zip-code data. For example, downtown properties are usually
worth more than other areas. Or there may be particularly affluent
zip-codes etc. It is my intuition that this kind of data would
significantly improve the KNN model as well as improve the linear
models. Furthermore, how many stories a house has, whether the property
has a garage, and whether the property is in a school district could be
particularly helpful.

<br/>

## 2. Classification and Retrospective Sampling

<br/>

### a. Make a bar plot of default probability by credit history

We can see in the bar plot below that in this dataset, people with good
credit history has the highest probability of default and people with
terrible credit history had the lowest probability of default. This is
likely due to the way the bank chose to sample the data.

<br/>

![](HW2_Saratoga_Albert_Joe_files/figure-markdown_strict/chunk13-1.png)

<br/>

### b. Build a logistics regression model for predicting default probability

Using the variables specified on the homework assignment, I created a
logistic regression model. The logistics regression model returns
coefficients in log odds. I have converted the coefficients back to odds
in the output below. As can be seen from the output below, those with
poor history and terrible history in this model actually reduce the
probability that a given person would default.

<br/>

    ##         (Intercept)            duration              amount         installment 
    ##               0.319               1.024               1.000               1.408 
    ##                 age         historypoor     historyterrible          purposeedu 
    ##               0.977               0.289               0.144               2.006 
    ## purposegoods/repair       purposenewcar      purposeusedcar       foreigngerman 
    ##               1.152               3.290               0.506               0.256

Now taking a look at the confusion matrix (setting the threshhold at
0.5), we can see that the model does not perform very well using this
data. Below shows the results of a confusion matrix on the out of sample
predictions. Especially concerning is the fact that out of the 56 people
who actually defaulted on their loan, this model predicted that 46 of
those would not default.

    ##    yhat
    ## y     0   1
    ##   0 132  12
    ##   1  46  10

    ## Using just one train-test split, the out of sample accuracy is: 0.71

    ## Using 5 folds, the average out of sample accuracy is 0.729

<br/>

We can see from the ‘history’ variable in this logistic regression model
that having a poor credit history reduces the odds of defaulting by a
factor of more than 3, and having a terrible credit score reduces the
odds of default by a factor of more than 6. This is because bank
substantially oversampled the population of people who defaulted on the
loan. Consequently, this dataset would not be appropriate in building a
predictive model because the dataset is not representative of the
population of people who borrow from this bank. This data may be helpful
during exploratory data analysis to see what factors may possible
contribute to defaults on loans.

<br/>

Since the bank collects data on all of its customers, I would recommend
that the bank use the population or a randomly selected subset of the
population to design a predictive model.
