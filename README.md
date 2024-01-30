

# Boston University Applied Business Analytics Hackathon Fall 2023

## Introduction
In the Applied Business Analytics Hackathon for Fall 2023, student teams tackled three challenges: data analysis and modeling, business case analysis, and a technical interview simulation, all revolving around a health insurance dataset. Our team's mission was to derive precise, personalized insurance quotes, ensuring our mock company's profitability and customer retention.

## Data and Methods
The dataset featured seven variables: age, sex, BMI, children, smoking status, region, and charges. Our analysis involved data cleaning, examining for missing values, converting categorical variables to binary, and checking for multicollinearity. We discovered significant influences of 'Smoker,' 'Age,' and 'BMI' on insurance charges and proceeded to employ various predictive modeling techniques, including multilevel regression models, to forecast charges accurately.
Also, we developed an interactive R Shiny App that provides real-time estimation of insurance quotes based on the model to enhance data-driven decision-making for users.

- Shiny App URL:
https://ol0sjn-jiun-lee.shinyapps.io/Insurance_Quote_Prediction/

## Model Development and Evaluation

### Initial Model (Model 1)
Our initial foray into predictive modeling started with a multilevel linear model with varying intercepts for smokers and non-smokers:
```r
model_1 <- lmer(charges ~ age*bmi + region + children + female + (1 | smoker), data = train.data)
```
This model included an interaction term between age and BMI to account for covariance, enhancing performance.

### Enhanced Model (Model 2)
Upon further analysis, recognizing the differential impact of BMI on charges for smokers versus non-smokers, we progressed to a more sophisticated model with both varying slopes and intercepts:
```r
model_2 <- lmer(charges ~ age*bmi + region + children + female + (1 | smoker) + (0 + bmi | smoker), data = train.data)
```
### Performance Evaluation
We rigorously compared these models using the test set's Mean Absolute Error (MAE), Root Mean Squared Error (RMSE), and Mean Absolute Percentage Error (MAPE). The second model demonstrated superior performance with significantly lower error metrics:

Mean Absolute Error (MAE): A reduction of 34.3%, from 3,967.960 to 2,281.568.
Root Mean Squared Error (RMSE): A reduction of 44.5%, from 5,162.848 to 2,863.047.
Mean Absolute Percentage Error (MAPE): An improvement of 41.7%, from 39.49422% to 23.01002%.

## Results and Discussion
Our multilevel regression model with varying slopes and intercepts (Model 2) outperformed the baseline model, indicating an adeptness in capturing the nuances of how smoking status and BMI affect insurance costs. The model achieved a conditional R-squared of 0.906, signifying that about 90.6% of the variance was explained by our model.

Still, there are some questions about whether we can conclude that this model performs well. A low error on the test set can be a positive sign. However, a high error on the validation set and a low error on the test set relative to the training set may indicate the need for further review of the distribution or quality of the data set and possible overfitting issues.

It is possible that oversampling the smoker data affected the error metrics in the training, validation, and test sets. Oversampling causes certain data classes to be used repeatedly, which can cause the model to overfit these repeating patterns. In this case, the model may perform well on the training data but may not generalize well to new data, i.e., validation and test sets. So, oversampling can only be applied to training and validation sets. The test set should reflect the real-world data distribution as much as possible and should not contain oversampled data, considering the importance of the representativeness of the test set.

## Conclusion
Though not perfect, represents the best solution within the Hackathon's tight timeframe. It highlighted the significant effects of smoking and BMI on insurance costs. This experience honed our skills in rapid model optimization and provided valuable insights into data-driven decision-making under pressure.

## Team Members
- Danya Zhang
- Mansi Chaudhary
- Shriansh Nauriyal
- Priam Dinesh Vyas

