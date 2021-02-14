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
    Radiation	Temperature	Pressure	Humidity	WindDirection(Degrees)	Speed	Daylight_duration	Rel_time
Date								
2016-09-29 23:55:26-10:00	1.21	48	30.46	59	177.39	5.62	12.0	1.475602
2016-09-29 23:50:23-10:00	1.21	48	30.46	58	176.78	3.37	12.0	1.468588
2016-09-29 23:45:26-10:00	1.23	48	30.46	57	158.75	3.37	12.0	1.461713
2016-09-29 23:40:21-10:00	1.21	48	30.46	60	137.71	3.37	12.0	1.454653
2016-09-29 23:35:24-10:00	1.17	48	30.46	62	104.95	5.62	12.0	1.447778


## method-2, sun_is_up
	Radiation	Temperature	Pressure	Humidity	WindDirection(Degrees)	Speed	sun_is_up
Date							
2016-09-29 18:10:52-10:00	6.63	53	30.44	59	118.82	5.62	1
2016-09-29 18:05:22-10:00	10.96	54	30.44	59	154.16	4.50	1
2016-09-29 18:00:22-10:00	19.42	55	30.44	57	58.42	6.75	1
2016-09-29 17:55:22-10:00	27.14	55	30.44	53	47.86	4.50	1
2016-09-29 17:50:19-10:00	33.75	56	30.44	52	74.56	2.25	1


# Models

## Multivariate Linear Regression
## Random Forest
## Gradient Boosting


# Results
## Best best model
Grandient Boost with 'rel_time' feature extraction
train r^2 = 0.92
test r^2 = 0.91


# test
| Attempt | #1 | #2 | #3 | #4 | #5 | #6 | #7 | #8 | #9 | #10 | #11 | #12 |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| Seconds | 301 | 283 | 290 | 286 | 289 | 285 | 287 | 287 | 272 | 276 | 269 | 254 |