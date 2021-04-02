# Real Estate Investment - Rental Analysis

![San Francisco Park Reading](Images/san-francisco-park-reading.jpg)

*[San Francisco Park Reading by Juan Salamanca](https://www.pexels.com/photo/park-san-francisco-reading-61109/) | [Free License](https://www.pexels.com/photo-license/)*

## Background

Harold's company has just started a new Real Estate Investment division to provide customers with a broader range of portfolio options. Harold was tasked with building a prototype dashboard. The real estate team wants to trial this initial offering with investment opportunities for the San Francisco market. If the new service is popular, then they can start to expand to other markets.

The goal of this dashboard is to provide charts, maps, and interactive visualizations that help customers explore the data and determine if they want to invest in rental properties in San Francisco.

In this homework assignment, you will help Harold accomplish the following tasks:

1. [Rental analysis](#Rental-Analysis)

2. [Dashboard of interactive visualizations to explore the market data](#Dashboard)

---

## Packages Used

* Plotly Express
* Hvplot
* Panel - Holoviz (For creating Dashboard)
* Mapbox Token


## Files

* [sfo_neighborhoods_census_data.csv](Starter_Code/Data/sfo_neighborhoods_census_data.csv)
* [neighborhoods_coordinates.csv](Starter_Code/Data/neighborhoods_coordinates.csv)
* [Rental Analysis Starter Jupyter Notebook](Starter_Code/rental_analysis.ipynb)
* [Dashboard Starter Jupyter Notebook](Starter_Code/dashboard.ipynb)


## Rental Analysis

The first step to building the rental analysis is to work out all of the calculations and visualizations in an analysis notebook.  Use the `rental_analysis.ipynb` to complete the following:

#### Housing Units Per Year

Calculate the average number of housing units per year and visualize the results as a bar chart using the Pandas plot function.

1. Calculate the `average number of housing units per year` in San Fransciso

  ```python
    housing_unit = sfo_data.groupby('year')['housing_units'].mean()
    housing_unit.plot.bar()
  ```


Visualization as a Bar chart using Pandas Plot

  ![scaled-bar.png](Images/scaled-bar.png)


#### Average Gross Rent in San Francisco Per Year

Visualize the average gross rent per year to better understand the trends for rental income over time. You will visualize the average (mean) gross rent per year and visualize it as a line chart.

1. Calculate the mean `gross rent` for each year

  ```python
    sfo_data.groupby('year')['gross_rent'].mean().plot()
  ```
  
  
2. Visualization as a Line Chart

  ![gross-rent.png](Images/gross-rent.png)

#### Average Sales Price Per Year

Determine the average sales price per year to better understand the sales price of the rental property over time. For example, a customer will want to know if they should expect an increase or decrease in the property value over time so they can determine how long to hold the rental property. 

1. Calculate the mean `sales_price_sqr_foot` for each year.

    ```python
        sfo_data.groupby('year')['sales_price_sqr_foot'].mean().plot()
    ```


2. Visualization as a Line Chart

  ![average-sales.png](Images/average-sales.png)

#### Average Prices By Neighborhood

In this section, Compare the average prices by neighborhood.

1. Group the data by year and by neighborhood and calculate the average (mean) `sales_price_sqr_foot`.

    ```python
        neighborhood_df = sfo_data.groupby(['year','neighborhood']).mean().reset_index()
        neighborhood_df.hvplot(label='Average Price per Square feet by year ',
                               x='year',
                               y='sale_price_sqr_foot', 
                               groupby='neighborhood')
    ```
    
    
2. Visualize with the neighborhood as a dropdown selector

  ![avg-price-neighborhood.png](Images/avg-price-neighborhood.png)

#### Top 10 Most Expensive Neighborhoods

1. Calculate the mean sale price for each neighborhood and then sort the values to obtain the top 10 most expensive neighborhoods on average. Plot the results as a bar chart.

   ```python
   avg_values_neighborhood = neighborhood_df.drop(columns=['year']).groupby('neighborhood').mean()
   top_expensive_neighborhood = avg_values_neighborhood.sort_values("sale_price_sqr_foot", ascending = False).head(10)
   ```
    
2. Visualization as a Bar Chart

  ![top-10-expensive-neighborhoods.png](Images/top-10-expensive-neighborhoods.png)
  

#### Parallel Coordinates and Parallel Categories Analysis

Use plotly express to create parallel coordinates and parallel categories visualizations so that investors can interactively filter and explore various factors related to the sales price of the neighborhoods.

Using the DataFrame of Average values per neighborhood (calculated above), created the following visualizations:

1. Parallel Coordinates Plot

  ![parallel-coordinates.png](Images/parallel-coordinates.png)

2. Parallel Categories Plot

  ![parallel-categories.png](Images/parallel-categories.png)

#### Neighborhood Map

Using Scatter Mapbox object from plotly express, Geographical visualization of the neighborhood location data and information about the average prices per neighborhood.

Remember that in order to create maps visualizations using Plotly Express, you will need to create an account at [mapbox](https://www.mapbox.com/) and [create an access token](https://docs.mapbox.com/help/how-mapbox-works/access-tokens/#creating-and-managing-access-tokens).

  ![neighborhood-map.png](Images/neighborhood-map.png)

## Dashboard

Now that we have worked out all of the code and analysis, We will use the Panel library to build an interactive dashboard for all of the visualizations in `Dashboard.ipynb`. 


#### Steps to execute the Dashboard.ipynb:

    1. Open terminal
    2. activate your envrionment where your packages are installed
    3. Makesure your `MAP_KEY` added in the environment variable
    4. Goto the path where the Dashboard.ipynb is located
    5. Execute the below command to run the file
    
   ```python
   panel serve --show dashboard.ipynb
   ```

  ![dashboard-demo.gif](Images/dashboard-demo.gif)


    
- - -
