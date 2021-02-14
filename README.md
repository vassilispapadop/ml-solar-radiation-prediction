# Install dependencies

```python
pip install numpy
pip install pandas
pip install sklearn
pip install matplotlib
pip install seaborn
```

# Launch jupyter
```python
jupyter notebook nasa_solar_radiation_prediction.ipynb
```

# Dataset

Period: 4 months, September - December 2016, Haiwai
Observation interval: per 5 minutes
Features: Radiation, Temperature, Humidity, Pressure, Wind Direction, Wind Speed, TimeSunRise, TimeSunSet

## Describe
| UNIXTime | Data | Time | Radiation | Temperature | Pressure | Humidity | WindDirection(Degrees) | Speed | TimeSunRise | TimeSunSet |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| 1475229326 | 9/29/2016 12:00:00 AM | 23:55:26 |   1.21 |       48 |             30.46 |      59 |         177.39 |  5.62 |   06:13:00 |  18:13:00 |
| 1475229023 | 9/29/2016 12:00:00 AM |  23:50:23 |   1.21 |       48 |             30.46 |      58 |         176.78 | 3.37 |   06:13:00 |       18:13:00 |
| 1475228726 | 9/29/2016 12:00:00 AM |  23:45:26 |   1.23 |       48 |             30.46 |      57 |         158.75 | 3.37 |   06:13:00 |       18:13:00 |
| 1475228421 | 9/29/2016 12:00:00 AM |  23:40:21 |   1.21 |       48 |             30.46 |      60 |         137.71 | 3.37 |   06:13:00 |       18:13:00 |
| 1475228124 | 9/29/2016 12:00:00 AM |  23:35:24 |   1.17 |       48 |             30.46 |      62 |         104.95 | 5.62 |   06:13:00 |       18:13:00 |



# Feature Engineering

## method-1, rel_time
```python
def relativeTimeFeature(self):
    print('Creating feature:', self.featureCase)
    #Converting sunrise and sunset times into timestamp
    self.df['sunrise_timestamp'] = self.df.apply(lambda row: datetime.timestamp(row['sunrise_time']), axis = 1)
    self.df['sunset_timestamp'] = self.df.apply(lambda row: datetime.timestamp(row['sunset_time']), axis = 1)

    #Creating a column containing the number of daily light hours
    self.df['Daylight_duration'] = (self.df['sunset_timestamp'] - self.df['sunrise_timestamp'])/60/60

    #Creating column describing current time relative to sunrise/sunset
    self.df['Rel_time'] = (self.df['UNIXTime']- self.df['sunrise_timestamp'])/(self.df['sunset_timestamp']-self.df['sunrise_timestamp'])

    #Removing unnecessary features/columns
    self.dropColumns(['UNIXTime','sunrise_timestamp', 'sunset_timestamp', 'sunset_time', 'sunrise_time'])
```
| Date | Radiation | Temperature | Pressure | Humidity | WindDirection(Degrees) | Speed | Daylight_duration | Rel_time |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |							
|2016-09-29 23:55:26-10:00|	1.21|	48|	30.46|	59|	177.39|	5.62|	12.0|	1.475602|
|2016-09-29 23:50:23-10:00|	1.21|	48|	30.46|	58|	176.78|	3.37|	12.0|	1.468588|
|2016-09-29 23:45:26-10:00|	1.23|	48|	30.46|	57|	158.75|	3.37|	12.0|	1.461713|
|2016-09-29 23:40:21-10:00|	1.21|	48|	30.46|	60|	137.71|	3.37|	12.0|	1.454653|
|2016-09-29 23:35:24-10:00|	1.17|	48|	30.46|	62|	104.95|	5.62|	12.0|	1.447778|


## method-2, sun_is_up
```python
def daylight(self, current_time, rising_time, set_time):
    return (rising_time < current_time) and (current_time < set_time)

def sunIsUp(self):
    print('Creating feature', self.featureCase)
    sun_is_up = [self.daylight(self.df.index[index], self.df["sunrise_time"][index], self.df["sunset_time"][index]) for index in range(self.df.shape[0])]
    sun_is_up = np.array(sun_is_up, dtype = int)
    self.df["sun_is_up"] = sun_is_up
    
    proportion = round(sum(self.df["sun_is_up"]/self.df.shape[0]*100), 2)
    print("Proportion of record with the sun up : {0}%".format(proportion))
```
| Date | Radiation | Temperature | Pressure | Humidity | WindDirection(Degrees) | Speed | sun_is_up |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |						
|2016-09-29 18:10:52-10:00|	6.63|	53|	30.44|	59|	118.82|	5.62|	1|
|2016-09-29 18:05:22-10:00|	10.96|	54|	30.44|	59|	154.16|	4.50|	1|
|2016-09-29 18:00:22-10:00|	19.42|	55|	30.44|	57|	58.42|	6.75|	1|
|2016-09-29 17:55:22-10:00|	27.14|	55|	30.44|	53|	47.86|	4.50|	1|
|2016-09-29 17:50:19-10:00|	33.75|	56|	30.44|	52|	74.56|	2.25|	1|


# Models

## Multivariate Linear Regression
## Random Forest
```python
tree_based_estimators = [100, 300, 500, 800]
min_samples_leaf: [0.075, 0.05, 0.025]
max_depth': [5, 6, 7]
```
## Gradient Boosting
```python
tree_based_estimators = [100, 300, 500, 800]
min_samples_leaf: [0.075, 0.05, 0.025]
max_depth': [5, 6, 7]
```
# Results
## Best best model
Grandient Boost with 'rel_time' feature extraction
train r^2 = 0.92
test r^2 = 0.91
