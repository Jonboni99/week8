# week8

A) Oldest Victoria Users (Name, Age)
	1. moutaineer2525 54
	2. codexmas 46
	3. Omid Zamani 45
	4. MarcClintDion 43
	5. Chalk Talk 40
	6. literaphile 35
	7. robru 33
	8. brandonscript 32
	9. logan 31
	10. acorscadden 31
AA) Code: 
select DisplayName, age
from users
where (Location like 'Victoria, BC')
order by age desc

B) Top 10 highest reputation users in Victoria (Name, Reputation)
	1. brandonscript 28442
	2. logan 2647
	3. robru 965
	4. Aliweb 876
	5. Romanulus 799
	6. thattyson 548
	7. Jeffery Guenther 538
	8. iamronak 496
	9. Eric 450
	10. Bob Warwick 201
BB)Code:
select DisplayName, reputation
from users
where (Location like 'Victoria, BC')
order by reputation DESC

C) Top 5 Victoria developers by accepted answer percentage
	1. nemesv 90.82%
	2. Alive to Die 89%
 	3. Stephen Muecke 83.69%
	4. Luksprog 81.32%
	5. Martin R 81.01%
CC) Code:
SELECT TOP ##MaxUsers?5##
        a.OwnerUserId AS [User Link],
        Count(a.Id) AS [Total Answers],
        Sum(CASE q.AcceptedAnswerId WHEN a.Id THEN 1 ELSE 0 END) AS [Accepted Answers],  
        Round(Sum(CASE q.AcceptedAnswerId WHEN a.Id THEN 1 ELSE 0 END) * 100.0 / Count(a.Id), 2) AS [Percentage Accepted],
        Round(CAST(Sum(CASE q.AcceptedAnswerId WHEN a.Id THEN 1 ELSE 0 END) AS FLOAT) * (CAST(Sum(CASE q.AcceptedAnswerId WHEN a.Id THEN 1 ELSE 0 END) AS FLOAT) / Count(a.Id)), 2) AS Weighting
FROM    Posts AS a
   JOIN Posts AS q
     ON a.ParentId = q.Id
WHERE
        q.postTypeId = 1
    AND a.postTypeId = 2
GROUP BY
        a.OwnerUserId
ORDER BY
        PercentageAccepted DESC

D) Top 10 Victoria developers by accepted answer percentage on questions with the tag javascript