## Formula-1-World-Championship-1950-2024

Content
The dataset consists of all information on the Formula 1 races, drivers, constructors, qualifying, circuits, lap times, pit stops, championships from 1950 till the latest 2024 season.

_Acknowledgements: The data is compiled from http://ergast.com/mrd/_

_Retrieved: 9/14/2024 from https://www.kaggle.com/datasets/rohanrao/formula-1-world-championship-1950-2020/data_

Let's analyze this dataset 

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

