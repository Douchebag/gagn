#Skilaverkefni 2

##Basic Queries

1.
```sql
select ProductName, QuantityPerUnit from products;
```

2.
```sql
select ProductID, ProductName from products order by productID asc;
```

3.
```sql
select ProductID, ProductName from products where Discontinued = True order by productID asc;
```

4.
```sql
select ProductName, UnitPrice from products order by UnitPrice asc;
```

5.
```sql
select ProductID, ProductName, UnitPrice from products where UnitPrice < 20.0000 order by productID asc;
```

6.
```sql
select ProductID, ProductName, UnitPrice from products where UnitPrice between 15.0000 and 25.0000  order by productID asc;
```

7.
```sql
select ProductName, UnitPrice from products where UnitPrice > (select avg(UnitPrice) from products) order by UnitPrice asc;
```

8.
```sql
select ProductName, UnitPrice from products order by UnitPrice desc limit 10;
```

9.
```sql
select Discontinued, count(Discontinued) from products group by Discontinued;
```

10.
```sql
select ProductName, UnitsOnOrder, UnitsInStock from products where UnitsInStock < UnitsOnOrder order by UnitsInStock asc;
```

##Sub-Queries

1. 
```sql
select first_name, last_name, salary from employees where salary > (select salary from employees where last_name = "Bull") order by salary desc;
```

2. 
```sql
select first_name, last_name from employees where department_id = (select department_id from departments where department_name = "IT");
```

3. 
```sql
select first_name, last_name from employees where manager_id != 0 and department_id in (select department_id from departments where location_id in (select location_id from locations where country_id = "US"));
```

4. 
```sql
select first_name, last_name from employees where employee_id in (select manager_id from employees);
```

5. 
```sql
select first_name, last_name from employees where salary > (select avg(salary) from employees);
```

##Join

1.
```sql
select department_name, location_id, street_address, city, state_province, country_id
from departments
natural join locations;
```
2.
```sql
select first_name, last_name, department_id, department_name
from employees
natural join departments;
```
3.
```sql
select first_name, last_name, jobs.job_title, departments.department_id, departments.department_name
from employees
inner join jobs
on employees.job_id = jobs.job_id
inner join departments
on employees.department_id = departments.department_id
order by department_id asc;
```
4.
```sql
select e.employee_id, e.last_name, e.manager_id, m.last_name
from employees e
join employees m
where e.manager_id = m.employee_id
```
5.
```sql

```
6.
```sql

```
