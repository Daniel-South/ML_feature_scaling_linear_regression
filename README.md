# ML_feature_scaling_linear_regression
The Effect of Feature Scaling on Coefficients in Machine Learning Algorithms
Daniel R. South  
2026-05-20  

A real estate agent requests a tools to predict home prices in her area based on square footage and the number of bathrooms. They're willing to neglect other features such as area and age, because most of the houses were built in similar developments in the same town at about the same time.  

Ideally, they want a formula:  

price = B0 + B1 * square_footage + B2 * number_of_bathrooms  

Your model will supply coefficients, B0, B1, and B2 that will return a reasonable estimate of a house's price when the agent plugs in the area and number of bathrooms.  

The agent shares recent home pricing data in a CSV file. It looks as though the data can be modeled with linear regression, but notice a potential issue: the number of bathrooms is in single digits, while the square feet are in thousands.  

In order to prevent the model from giving more weight to the larger square footage numbers, you'll first need to scale the data set so that all features have similar ranges of values. You can use min/max scaling and map all of the values in ranges between 0 and 1, or you can use standard scaling which sets the mean value to 0 and the variance to 1.  

This seems straightforward, but you pause to reflect on how scaling will impact the coefficients. You reflect on a simplified version of the model:  

price = B1 * square_footage  

If a 2500 square foot home costs $250,000 in this neighborhood, the value of B1 would be 100.  

250,000 = 100 * 2500  

But if after you scale the data with min/max scaling, 2500 square feet maps to a value of 0.5, then B1 would have to be 500,000, a much larger value.  

250,000 = 500,000 * 0.5  

If you give this value of B1 to your real estate agent client and they try to price a 3,000 square foot home, the price of the home will be ridiculously overestimated:  

price = B1_scaled * square_footage = 500,000 * 3,000 = 1,500,000,000  

A billion and a half dollars is clearly the wrong answer.  

We are left to conclude the following:  

If we used scaled data to train the model, the coefficients will need to be scaled back to the original dimensions before we can use them.  

To do this, we first have to determine how much the data was scaled.  

To scale the 2500 square feet down to .5, we applied a 5000 times reduction. 2500/5000 = 0.5  

As a result, coefficient B1 is 5,000 time larger than it should be for use with actual home size values. We can rescale the coefficient by dividing it by this same factor.  

B1 = B1_scaled / 5,000 = 100  

The client will receive the rescaled value of B1, which they can use as follows (using the simplified formula for illustration):  

price = B1 * 3000 = 100 * 3000 = $300,000  


The attached notebook demonstrates how to rescale coefficients from a model built on scaled data. To simplify the illustration, only one feature (square footage) was used to forecast home prices.  
