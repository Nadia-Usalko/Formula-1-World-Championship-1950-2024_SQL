# $\color{red}{\textsf{Formula 1 World Championship 1950-2024}}$ :oncoming_automobile:

*Content:*
The dataset consists of all information on the Formula 1 races, drivers, constructors, qualifying, circuits, lap times, pit stops, championships from 1950 till the latest 2024 season.

_Acknowledgements: The data is compiled from http://ergast.com/mrd/_

_Retrieved: 9/14/2024 from https://www.kaggle.com/datasets/rohanrao/formula-1-world-championship-1950-2020/data_

*To complete this project I worked in:*

-DB Browser for SQLite

-Tableau Public


### 
We all heard of the drivers who made history in F1, how many victories they actually had?

```ruby
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
LIMIT 10
```
Output:

![image](https://github.com/user-attachments/assets/b3300d89-819b-476f-80ee-6acc5ffa6e0d)

The first line of output shows Lewis Hamilton with his outstanding 104 victories, followed by legendary Michael Schumacher with 91.



Let's get more specific of the area we want to research. Between 2014 - 2021 there used to be a regular Russian GP. What about victories on Sochi Autodrom Circuit?
```ruby
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
Output:

![image](https://github.com/user-attachments/assets/63913608-c6be-4f98-82cd-cb2b223fd677)

Lewis Hamilton, Valtteri Bottas and Nico Rosberg are confident winners.



The fastest lap in history of the Russian GP:
```ruby
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
Output:

![image](https://github.com/user-attachments/assets/70558945-a9cf-43b0-8a6c-043fa8163f1c)

1:35:761 is a record lap speed set by Lewis Hamilton.



It can be important for constructors and mechanichs to analyze the circuit and its specifics. Let's calculate average pit-stop duration on Sochi Autodrom Circuit by year:
```ruby
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
Output:

![image](https://github.com/user-attachments/assets/00785a40-1cb5-4aea-82d9-f33a8922bdc0)


Data can tell us a lot of stories and I hope my research was interesting. 
Feel free to [follow me on Linked-In](https://www.linkedin.com/in/Nadia-usalko/).
