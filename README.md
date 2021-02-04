# ml-solar-radiation-prediction

Period: 4 months, September - December 2016, Haiwai
Observation interval: per 5 minutes
Features: Radiation, Temperature, Humidity, Pressure, Wind Direction, Wind Speed, TimeSunRise, TimeSunSet

# dataset example
UNIXTime,   Data,                   Time,       Radiation,  Temperature,    Pressure,   Humidity,   WindDirection(Degrees),Speed,   TimeSunRise,    TimeSunSet
1475229326, 9/29/2016 12:00:00 AM,  23:55:26,   1.21,       48,             30.46,      59,         177.39,                 5.62,   06:13:00,       18:13:00
1475229023, 9/29/2016 12:00:00 AM,  23:50:23,   1.21,       48,             30.46,      58,         176.78,                 3.37,   06:13:00,       18:13:00
1475228726, 9/29/2016 12:00:00 AM,  23:45:26,   1.23,       48,             30.46,      57,         158.75,                 3.37,   06:13:00,       18:13:00
1475228421, 9/29/2016 12:00:00 AM,  23:40:21,   1.21,       48,             30.46,      60,         137.71,                 3.37,   06:13:00,       18:13:00
1475228124, 9/29/2016 12:00:00 AM,  23:35:24,   1.17,       48,             30.46,      62,         104.95,                 5.62,   06:13:00,       18:13:00


# method-1, time feature engineering
Radiation	Temperature	Pressure	Humidity	WindDirection(Degrees)	Speed	Hours_of_light	Rel_time
Date								
2016-09-29 23:55:26-10:00	1.21	48	30.46	59	177.39	5.62	12.0	1.475602
2016-09-29 23:50:23-10:00	1.21	48	30.46	58	176.78	3.37	12.0	1.468588
2016-09-29 23:45:26-10:00	1.23	48	30.46	57	158.75	3.37	12.0	1.461713
2016-09-29 23:40:21-10:00	1.21	48	30.46	60	137.71	3.37	12.0	1.454653
2016-09-29 23:35:24-10:00	1.17	48	30.46	62	104.95	5.62	12.0	1.447778
