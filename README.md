# Sea-Level-Predictor

You will anaylize a dataset of the global average sea level change since 1880. You will use the data to predict the sea level change through year 2050.

Use the data to complete the following tasks:

Use Pandas to import the data from epa-sea-level.csv.

Use matplotlib to create a scatter plot using the "Year" column as the x-axis and the "CSIRO Adjusted Sea Level" column as the y-axix.

Use the linregress function from scipy.stats to get the slope and y-intercept of the line of best fit. 

Plot the line of best fit over the top of the scatter plot. 

Make the line go through the year 2050 to predict the sea level rise in 2050.

Plot a new line of best fit just using the data from year 2000 through the most recent year in the dataset. 

Make the line also go through the year 2050 to predict the sea level rise in 2050 if the rate of rise continues as it has since the year 2000.

The x label should be "Year", the y label should be "Sea Level (inches)", and the title should be "Rise in Sea Level".

```Python
import pandas as pd
import matplotlib.pyplot as plt
from scipy.stats import linregress

def draw_plot():
    # Read data from file
    df = pd.read_csv("epa-sea-level.csv")
    y = df["CSIRO Adjusted Sea Level"]
    x = df["Year"]

    # Create scatter plot
    fig, ax = plt.subplots()
    plt.scatter(x,y)

    # Create first line of best fit
    res = linregress(x, y)
    x_pred = pd.Series([i for i in range(1880,2051)])
    y_pred = res.slope*x_pred + res.intercept
    plt.plot(x_pred, y_pred, "r")

    # Create second line of best fit
    new_df = df.loc[df['Year'] >= 2000]
    new_x = new_df['Year']
    new_y = new_df['CSIRO Adjusted Sea Level']
    res_2 = linregress(new_x, new_y)
    x_pred2 = pd.Series([i for i in range(2000,2051)])
    y_pred2 = res_2.slope*x_pred2 + res_2.intercept
    plt.plot(x_pred2, y_pred2, "green")


    # Add labels and title
    ax.set_xlabel("Year")
    ax.set_ylabel("Sea Level (inches)")
    ax.set_title("Rise in Sea Level")
    
    # Save plot and return data for testing (DO NOT MODIFY)
    plt.savefig('sea_level_plot.png')
    return plt.gca()
```
