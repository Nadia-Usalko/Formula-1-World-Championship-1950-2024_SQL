## Formula-1-World-Championship-1950-2024

Content
The dataset consists of all information on the Formula 1 races, drivers, constructors, qualifying, circuits, lap times, pit stops, championships from 1950 till the latest 2024 season.

_Acknowledgements: The data is compiled from http://ergast.com/mrd/_

_Retrieved: 9/14/2024 from https://www.kaggle.com/datasets/rohanrao/formula-1-world-championship-1950-2020/data_

Let's analyze this dataset. We all heard of the drivers who made history in F1, how many victories they actually had?

```
SELECT results.driverId,
		COUNT(results.position) AS number_of_victories,
		drivers.forename AS driver_first_name,
		drivers.surname AS driver_last_name
FROM results
JOIN drivers
	ON results.driverId = drivers.driverId
WHERE results.position = 1
GROUP BY results.driverId
ORDER BY number_of_victories DESC
```

The first line of output shows Lewis Hamilton with his outstanding 104 victories, followed by legendary Michael Schumacher with 91.

Let's get more specific of the area we want to research. Between 2014 - 2021 there used to be a regular Russian GP. What about victories on Sochi Autodrom Circuit?
```
SELECT  COUNT(results.driverId) AS number_of_victories,
		results.position,
		results.driverId,
		drivers.forename AS driver_first_name,
		drivers.surname AS driver_last_name,
		races.circuitId,
		circuits.name AS circuit_name
FROM results
JOIN races	
	ON results.raceId = races.raceId
JOIN drivers
	ON results.driverId = drivers.driverId
JOIN circuits
	ON races.circuitId = circuits.circuitId
WHERE races.name = 'Russian Grand Prix'
	AND position = 1
GROUP BY results.driverId
ORDER BY number_of_victories DESC
```

The fastest lap at Russian GP:
```
SELECT MIN(lap_times.time) AS 'the_fastest_lap',
	lap_times.driverId,
	drivers.forename AS driver_first_name,
	drivers.surname AS driver_last_name,
	circuits.name AS circuit_name
FROM lap_times
JOIN drivers
	ON lap_times.driverId = drivers.driverId
JOIN races
	ON lap_times.raceId = races.raceId
JOIN circuits
	ON races.circuitId = circuits.circuitId
WHERE circuits.country = 'Russia'
```

Average pit-stop time on Sochi AUtodrom Circuit by year:
```
SELECT AVG(pit_stops.duration) AS average_pit_stop_duration,
	circuits.name AS circuit_name,
	pit_stops.raceId,
	races.year
FROM pit_stops
JOIN races
	ON pit_stops.raceId = races.raceId
JOIN circuits
	ON races.circuitId = circuits.circuitId
WHERE circuits.country = 'Russia'
GROUP BY pit_stops.raceId
```


