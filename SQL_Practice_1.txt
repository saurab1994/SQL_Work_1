use bhati;                          --database name

select * from pets;           -- to fetch all  data from pets data

--To fetch unique values of “Age” field
select distinct age from pets;

--To fetch unique combinations of Gender and Age column
select distinct age, gender from pets;

--To fetch the names of the pets whose name contains letter “u” in the name
select name from pets
where name like '%u%';

--To fetch count of rows for each “Kind” present in the table
select kind,count(kind) as 'Kind_count' from pets
group by kind;

--To find the average age of each “Kind” of pets
select kind,avg(age) as 'avg_age' from pets
group by kind;

--To print all records where Gender = “Female” and Kind = “Dog”
select * from pets
where kind='Dog' and gender ='female';

-- To find the count of records for a combination of “Kind” and “Gender”
select kind,gender,count(kind) from pets
group by kind,gender
order by kind;

--To fetch all the “Kind” values that have maximum age greater than 13
select kind, max(age) from pets
group by kind
having max(age)>13;

--To fetch the 15 records from the table
select top(15) * from pets;

--To fetch the names that have 5 letters in their name
select name from pets
where name like '_____';

-- To fetch the count of distinct “Age” in the table
select count(distinct(age)) from pets;

--To fetch the records where Age is between 5 and 15
select * from pets
where age between 5 and 15;


select * from employees;        --loading another dataset

-- Find the length of field email
select len(email) from employees;

--Find count of employees in each department_id
select department_id,count(department_id) as 'count'
from employees
group by department_id;

--To fetch the no. of years each employee has served the company till today
select concat(first_name,' ',last_name) as
'name',datediff(year,hire_date,CURRENT_TIMESTAMP) as 'year'
from employees;

--create a salary bucket of low, medium and high
select *,
case when salary<=7000 then 'low'
when salary >20000 then 'high'
 else 'medium'
 end as 'salary_bucket'
from employees;

--To replace “sqltutorial.org” with “abccompany.com” present in Email column
select replace(email,'sqltutorial.org','abccompany.com')
from employees;

--Create table Emp1 from the table by filtering records where salary between 7000 and 16000 
select * into emp1 from employees where salary between 7000 and 16000;
select * from emp1;

--Create table Emp2 from the table by filtering records where manager_id is in 100 and 114
select * into emp2 from employees where manager_id in (100,114);
select * from emp2;

--Fetch the employee_id, first_name and last_name from both the tables(Emp1 and--Emp2, ) which are present in Emp1 but not in Emp2.
select employee_id,first_name,last_name
from emp1
where employee_id not in (select employee_id from emp2);