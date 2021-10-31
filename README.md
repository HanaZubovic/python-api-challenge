# 🌩️Python Weather API Challenge: What's the Weather Like?

## Background

Whether financial, political, or social -- data's true power lies in its ability to answer questions definitively. So let's take what you've learned about Python requests, APIs, and JSON traversals to answer a fundamental question: "What's the weather like as we approach the equator?"

Now, we know what you may be thinking: _"Duh. It gets hotter..."_

But, if pressed, how would you **prove** it?

![Equator](Images/equatorsign.png)

## Part I - WeatherPy

In this example, you'll be creating a Python script to visualize the weather of 500+ cities across the world of varying distance from the equator. To accomplish this, you'll be utilizing a [simple Python library](https://pypi.python.org/pypi/citipy), the [OpenWeatherMap API](https://openweathermap.org/api), and a little common sense to create a representative model of weather across world cities.

The first requirement is to create a series of scatter plots to showcase the following relationships:

* Temperature (F) vs. Latitude
* ![image](https://github.com/HanaZubovic/python-api-challenge/blob/76db4f96ef8fdf9a3db2ac081ce1f1222a48c832/Images/Northern%20Hemisphere%20-%20Max%20Temp%20vs.%20Latitude%20Linear%20Regression.png)
* Humidity (%) vs. Latitude
* ![image](https://github.com/HanaZubovic/python-api-challenge/blob/76db4f96ef8fdf9a3db2ac081ce1f1222a48c832/Images/Northern%20Hemisphere%20-%20Humidity%20(%25)%20vs.%20Latitude%20Linear%20Regression.png)
* Cloudiness (%) vs. Latitude
* ![image](https://github.com/HanaZubovic/python-api-challenge/blob/76db4f96ef8fdf9a3db2ac081ce1f1222a48c832/Images/Northern%20Hemisphere%20-%20Cloudiness%20(%25)%20vs.%20Latitude%20Linear%20Regression.png)
* Wind Speed (mph) vs. Latitude
* ![image](https://github.com/HanaZubovic/python-api-challenge/blob/76db4f96ef8fdf9a3db2ac081ce1f1222a48c832/Images/Northern%20Hemisphere%20Temp%20vs.%20Latitude%20Linear%20Regression.png)

After each plot, add a sentence or two explaining what the code is analyzing.

The second requirement is to run linear regression on each relationship. This time, separate the plots into Northern Hemisphere (greater than or equal to 0 degrees latitude) and Southern Hemisphere (less than 0 degrees latitude):

**Northern Hemisphere - Temperature (F) vs. Latitude**

- R is valued at -0.87, there is quite a strong negative correlation.

**Southern Hemisphere - Temperature (F) vs. Latitude**

 - R is valued at 0.67, Above .5, r is considered to be moderately correlated. Since this is closer to .7 which is considered strong,    I would surmize that there is actually a pretty strong correlation.

**Northern Hemisphere - Humidity (%) vs. Latitude**
 
 - R is valued at .15, here we have little to no correlation between these two factors.

**Southern Hemisphere - Humidity (%) vs. Latitude**

- R is valued at .25, because of the proximity to .3 there is almost a sign of some correlation here though very weak at best.

**Northern Hemisphere - Cloudiness (%) vs. Latitude**

- R is .1, No correlations here. 

**Southern Hemisphere - Cloudiness (%) vs. Latitude**

- R is valued at .21, another two factors that are below the .3 threshold for minimum correlation.

**Northern Hemisphere - Wind Speed (mph) vs. Latitude**

- R is valued at .29, a weak correlation here at best between the wind speed in the northern hemisphere and the latitude.

**Southern Hemisphere - Wind Speed (mph) vs. Latitude**

- R is valued at -.37, because of the negative integer, here we can say there is a weak negative correlation.

After each pair of plots, take the time to explain what the linear regression is modeling. For example, describe any relationships you notice and any other analysis you may have.

Your final notebook must:

* Randomly select **at least** 500 unique (non-repeat) cities based on latitude and longitude.
* Perform a weather check on each of the cities using a series of successive API calls.
* Include a print log of each city as it's being processed with the city number and city name.
* Save a CSV of all retrieved data and a PNG image for each scatter plot.

### Part II - VacationPy

Now let's use your skills in working with weather data to plan future vacations. Use jupyter-gmaps and the Google Places API for this part of the assignment.

To complete this part of the assignment,you will need to do the following:

* Create a heat map that displays the humidity for every city from Part I.

  ![heatmap](Images/heatmap.png)
```
gmap_fig = gmaps.figure(center=(22.0, -1.0), zoom_level = 2)
heat_layer = gmaps.heatmap_layer(lat_long, weights = humidity, 
                                 dissipating = False, max_intensity = np.max(humidity),
                                 point_radius = 4)
gmap_fig.add_layer(heat_layer)
```

* Narrow down the DataFrame to find your ideal weather condition. For example:

  * A max temperature lower than 80 degrees but higher than 70.

  * Wind speed less than 10 mph.

  * Zero cloudiness.

  * Drop any rows that don't contain all three conditions. You want to be sure the weather is ideal.

  * **Note:** Feel free to adjust to your specifications but be sure to limit the number of rows returned by your API requests to a reasonable number.

* Using Google Places API to find the first hotel for each city located within 5000 meters of your coordinates.

* Plot the hotels on top of the humidity heatmap with each pin containing the **Hotel Name**, **City**, and **Country**.
```
droppedna_cities_df = cities_df.dropna()
filter_cities_df = droppedna_cities_df.loc[(droppedna_cities_df["Cloudiness"] == 0) &
                                           (droppedna_cities_df["Max Temp"] >= 70)&
                                           (droppedna_cities_df["Max Temp"] <= 80)&
                                           (droppedna_cities_df["Wind Speed"] < 10)
                                          ]
filter_cities_df.head()
```
### Pack your bags! 

![giphy](https://user-images.githubusercontent.com/16246354/139566303-89e17f27-7798-47c0-b419-cce5a944d6ea.gif)![200](https://user-images.githubusercontent.com/16246354/139566477-b97a2819-574e-4baa-bdde-ef332712a46e.gif)


