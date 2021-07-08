# SQL

## Table Description 

There are two tables at play 
1. Worker table ( Main Employee table )
   - Worker_id ( Auto Incrementing, Not null, PK )
   - First_name
   - Last_nam
   - Salary
   - Joining date ( DATETIME )
   - Department 

2. Title ( Contains job descriptions of emps )
   - Worker_Ref_id ( Foreign key references (worker_id) )
   - Worker_title  
   - Affected_from ( DATETIME )

## Queries 

1. **Fetch name as an alias "woker_name"** <br/><br/>
```Select FIRST_NAME AS WORKER_NAME from Worker; ```

2. **Fetch name in upper case** <br/><br/>
```Select UPPER(First_name) from Worker; ```

3. **Query to fetch unique department values** <br/><br/>
```SELECT distinct Department from Worker;  ```

4. **Query to fetch first three characters from a name** <br/><br/>
```SELECT substring(First_name, 1, 3) from Worker;  ```

5. **Fetch names from worker table and order it in ascending order** <br/><br/>
```SELECT First_name from Worker order by First_name asc;  ```

6. **Order by name ascending and department descending** <br/><br/>
```SELECT First_name, Department order by First_name asc, Department dsc ; ```

7. **Fetch detials of workers whose salary lie between x and y** <br/><br/>
```SELECT * from Worker WHERE salary between x and y;  ```

8. **Query to get number of workers of each depatment in descending order** <br/><br/>
```SELECT Department, count(Department) from Worker Group by Department Order by count(Department); ```
<br/><br/>
Now in here when we use group by on an attribute (x), we can only mention that attribute following the select query or certain other aggregate functions only and nothing else. Also condition is specified using ```HAVING```

9. **Print Wokrer detials who are also managers** <br/><br/>
```SELECT w.First_name, w.Salary from Worker w INNER JOIN Title t on w.Woker_id = t.Woker_ref_id and t.title = manager  ```
<br/><br/>
Always make it a rule of thub to mention the select preceeding statements with an instance of the table when implementing a join

10. **Query to display only odd rows** <br/><br/>
```SELECT * from Worker where MOD(Woker_id, 2) <> 0;  ```
<br/><br/>
We use worker_id to perform certain operations as it is auto incrementing

11. **Query to show only even rows** <br/><br/>
```Select * from Worker where MOD(Worker_id, 2) = 0;  ```

12. **Clone Woker to another table "CloneWorker"** <br/><br/>
```SELECT * INTO CloneWorker FROM Worker  ```

13. **Fetch Intersecting records** <br/><br/>
```(SELECT * from Woker) INTERSECT (SELECT * from Worker)  ```

14. **Query to show records from one table that another table does not have** <br/><br/>
```(SELECT * from Worker) MINUS (SELECT * from Title) ```

15. **Show current date and time** <br/><br/>
```SELECT CURDATE();```

16. **Show TOp (n) records in a table** <br/><br/>
```SELECT * from WokerOrder by salary Desc LIMIT 10 ```

17. **Query to get Nth Highest Salary** <br/><br/>
```SELECT * from Worker w1 where n - 1 in (SELECT Count(distinct w2.Salary) from Worker w2 where w2.salary >= w1.salary); ```

18. **Query to fetch list of emps with same salary** <br/><br/>
```SELECT w1.First_name, w1.salary from Worker w1, Worker w2 where w2.salary == w1.salary AND w1.Worker_id != w2.Worker_id```

19. **Query to display one row twice** <br/><br/>
```( SELECT * from Worker W where W.Department = "HR" ) UNION ALL ( SELECT * from worker W2 where W2.Department = "HR")```

20. **Query to fetch first 50 % records** <br/><br/>
```SELECT * from Worker where Worker_id <= (SELECt count(Worker_id)/2 from Worker);```

21. **Query to fetch departments which have less than 5 memebers** <br/><br/>
```SELECT Deparment, count(Department) from Wokrer Group by Deparment Having count(Department) <= 5;```

22. **Show all deparmtnets by number of people in them** <br/><br/>
```SELECT Department, count(Department) AS Number from Worker group by Department```

23. **Fetch first row** <br/><br/>
```SELECT * from Worker where Worker_id = (Select min(Worker_id) from Worker);```

24. **Fetch Last row** <br/><br/>
```SELECT * from Worker where Worker_id = (SELECt max(Worker_id) from Worker); ```

25. **Select the middle row** <br/><br/>
```SELECT * from Woker Where Worker_id = (Select count(Worker_id)/2 from Worker); => Works when there is a perfect middle row ( Even case )``` 
<br/><br/>
For universal numbers 
<br/><br/>
``` SELECT * from Worker where Worker_id <= (SELECT Count(Worker_id)/2 from Worker) MINUS SELECT * from Woker Where Worker_id < (SELECT Count(Worker_id)/2 from Worker);```

26. **Query to Print name of Employees having highest salary in each department** <br/><br/>
```SELECT w.First_name, w.Salary, w.Department from (SELECT max(Salary) as TotalSal, Department from Worker group by Department) as SalaryTable INNER JOIN Worker w on w.Department = SalaryTable.Department and w.Salary = SalaryTable.Salary ;```
<br/><br/>
The breakdown of the above is as follows : First we need to get a table which contains Department wise highest salaries. That is done using the inner subquery and that table is called as SalaryTable. Now this is Inner Joined with Worker table where worker department = Salary table department 

27. **Query to fetch three highest salaries** <br/><br/>
```SELECT * from Worker W1 Where 3 in (Select Count(Distinct(salary)) from Worker W2 where w2.Salary >= W1.Salary) Order By Salary Desc;```

28. **Department alogside total salaries paid for them** <br/><br/>
```SELECT Department, Sum(salary) from Worker Order By Department ; ```

29. **Last 5 records from a table** <br/><br/>
```SELECT * from Worker where Worker_id > (Select max(Worker_id) - f from Worker) ; ```
