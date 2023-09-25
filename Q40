WITH DateRange AS (
    SELECT DISTINCT visited_on
    FROM Customer
    WHERE visited_on >=  (select dateadd(day,6,min(visited_on)) from Customer)
)
, Amounts AS (
    SELECT c1.visited_on
           ,SUM(c2.amount) AS total_amount
    FROM DateRange c1
    LEFT JOIN Customer c2 ON c2.visited_on BETWEEN DATEADD(day, -6, c1.visited_on) AND c1.visited_on
   GROUP BY c1.visited_on
)
SELECT d.visited_on,
       a.total_amount AS amount,
       ROUND(cast( a.total_amount  as decimal)/ 7, 2) AS average_amount
FROM DateRange d
LEFT JOIN Amounts a ON d.visited_on = a.visited_on;
