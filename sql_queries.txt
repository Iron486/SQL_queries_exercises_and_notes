select *
select first_name, last_name
from employees
where department='Furniture';
where department like '%nitu%';
where salary >= 100000;
where salary < 100000;
where department ='Clothing'
and salary > 90000
and region_id = 2
or salary > 90000
and (department='Clothing'
or department='Pharmacy');


select *
from employees 
where not department = 'Sports'
where not department != 'Sports'
where not department <> 'Sports'
where email = NULL
where NULL = NULL
where not email is NULL
where email is not NULL
where department in ('Sports','First Aid', 'Toys')
where salary between 80000 and 100000





select first_name, email from employees
where department='Tools'
and salary > 110000 
and gender='F';

--second exercise
select first_name, hire_date from employees
where (department='Sports'
and gender='M')
or salary > 165000 ;

--third exercise

select first_name, hire_date from employees
where hire_date between '2002-01-01' and  '2004-01-01';
--alternatively, you can use > and <


-- fourth exercise	   
select * from employees
where (department='Automotive' 
and gender='M'
and salary between 40000 and 100000)
or ( gender='F'
and department='Toys' );
	   
select * from employees
order by employee_id --order from smallest to largest
order by employee_id desc--order from largest to smallest   
order by department --alphabetical order
-- alternatively   'order by department asc'


select distinct department 
from employees 
-- we have all the departments without repeating

select distinct department 
from employees 
order by 1 --alternatively, write department instead of 1
-- now they are ordered in alphabetical order

select distinct department 
from employees 
order by 1 
limit 10 -- it shows the top 10 records

select distinct department 
from employees 
order by 1 
fetch first 10 rows only -- it shows the top 10 records


select first_name, last_name as "Last Name", salary as "Yearly Salary"
from employees  -- to rename columns
	   
	 




--assignments
select student_name from students
where age between 18 and 20


select * from students


select * from students
where student_name like '%ch%' 
or student_name like '%nd' 

select student_name from students
where (student_name like '%ae%' 
or student_name like '%ph' )
and not age=19;


select student_name from students
order by age desc

select student_name, age from students
order by age desc
limit 4

select * from students
where (((student_no between 3 and 5) or student_no=7) 
and age <= 20) 
and (age > 20 and student_no >= 4)




select upper(first_name) --upper case first_name
from employees

select lower(department) --lower case first_name
from employees

select length(first_name) --length of first_name
from employees


select trim('     HELLO THERE    ')  --TO TRIM SPACES

select length(trim('     HELLO THERE    '))

select first_name || last_name 
from employees -- concatenate the values of the 2 columns

select first_name ||' '|| last_name 
from employees -- concatenate the values of the 2 columns
--adding a space btw columns

select first_name ||' '|| last_name full_name,department
from employees  --we also rename the coliumn in that case

select first_name ||' '|| last_name full_name,(salary>140000) is_highly_paid
from employees --it displays as true if salary >140000 and renames the column as 'is_highly_paid'
order by salary desc



select department, ('Clothing' in (department,first_name))
from employees


select department, (department like '%oth%')
from employees





select * from employees


select 'This is test data' test_data --to create data

select substring('This is test data' from 7 for 4) test_data_extracted
-- extract from position 7 for 4 characters
--we can do it even for an entire column

select substring('This is test data' from  4) test_data_extracted
---- extract everything from position 4 

select department, 
replace(department,'Clothing','Attire') modified_data,
-- replace Clothing with Attire
department || ' department'  as "Complete Department Name" --double quotes when there are spaces in the string
from departments
--it adds department at each data and rename the column

select position('@' in email) 
from employees --position in the string where @ is in email column

select substring(email,position('@' in email)+1 ) formatted_text
from employees --position in the string where @ is in email column
-- +1 increment the position of 1, selecting all the email
-- from one position after @


select coalesce(email,'NONE') as email
--when it sees a null, we can replace null with
--another string ('none in this case')
from employees


select upper(first_name),lower(first_name)
from employees

--group functions (group data together)
select max(salary)
from employees
select min(salary)
from employees
select round(avg(salary))
from employees
select count(employee_id) --it doesn't count null values
from employees
select count(*) --it counts considering all the columns
from employees
select sum(salary) --it counts considering all the columns
from employees
where department='Clothing'



--1
select last_name || ' works in the ' || department ||' department'  as "where they work"
from professors
limit 1

--2
select 'It is ' || (salary>95000) || ' that professor ' || last_name || ' is highly paid 'as "where they work"
from professors

--3
select last_name, substring(UPPER(department) from 1 for 3) formatted_text,  salary, hire_date
from professors

--4
select max(salary) as highest_salary, min(salary) as lowest_salary
from professors
where last_name != 'Wilson'

--5
select min(hire_date)
from professors


create table cars(make varchar(10))
select * from cars
--insert data
insert into cars values ('honda'); --insert semicolumn!!!
insert into cars values ('honda');
insert into cars values ('honda');
insert into cars values ('toyota');
insert into cars values ('toyota');
insert into cars values ('nissan');


insert into cars values (NULL);
insert into cars values (NULL);
insert into cars values (NULL);
insert into cars values (NULL);

select * from cars
--how many of each group we have
select count(*), make
from cars
group by make


select department, sum(salary)
from employees
where 1=1 --it's going to return true
group by department --groupby is after where

select department, sum(salary)
from employees
where region_id in (4,5,6,7) --it sums and consider only salaries in 4,5,6,7
group by department --groupby is after where


--it counts employees per department
select department, count(*) total_number_employees,
round(avg(salary)) avg_sal,min(salary)min_sal,
max(salary) max_sal
from employees
where salary > 70000
group by department --groupby is after where
order by total_number_employees desc --it should be at the end


-- any non aggregate column in the select statement,
-- must be mentioned even in the group by statement
select department, gender, count(*) 
from employees
group by department,gender 
order by department

select department, count(*) 
from employees
group by department
having count(*)>35 -- to filter groupped data
order by department

select first_name, count(first_name)
from employees
group by first_name
having count(*)>1

select substring(email,position('@' in email)+1 ) as email_domain, count(email)
from employees
group by email_domain 
order by count desc

select gender, region_id, min(salary) as min_salary,
max(salary) as max_salary,
round(avg(salary)) as avg_salary
from employees
group by gender, region_id 
order by gender desc ,region_id asc



CREATE TABLE fruit_imports
(
	id integer,
	name varchar(20),
	season varchar(10),
	state varchar(20),
	supply integer,
	cost_per_unit decimal
);

insert into fruit_imports values(1, 'Apple', 'All Year', 'Kansas', 32900, 0.22);
insert into fruit_imports values(2, 'Avocado', 'All Year', 'Nebraska', 27000, 0.15);
insert into fruit_imports values(3, 'Coconut', 'All Year', 'California', 15200, 0.75);
insert into fruit_imports values(4, 'Orange', 'Winter', 'California', 17000, 0.22);
insert into fruit_imports values(5, 'Pear', 'Winter', 'Iowa', 37250, 0.17);
insert into fruit_imports values(6, 'Lime', 'Spring', 'Indiana', 40400, 0.15);
insert into fruit_imports values(7, 'Mango', 'Spring', 'Texas', 13650, 0.60);
insert into fruit_imports values(8, 'Orange', 'Spring', 'Iowa', 18000, 0.26);
insert into fruit_imports values(9, 'Apricot', 'Spring', 'Indiana', 55000, 0.20);
insert into fruit_imports values(10, 'Cherry', 'Summer', 'Texas', 62150, 0.02);
insert into fruit_imports values(11, 'Cantaloupe', 'Summer', 'Texas', 8000, 0.49);
insert into fruit_imports values(12, 'Apricot', 'Summer', 'Kansas', 14500, 0.20);
insert into fruit_imports values(13, 'Mango', 'Summer', 'Texas', 17000, 0.68);
insert into fruit_imports values(14, 'Pear', 'Fall', 'Nebraska', 30500, 0.12);
insert into fruit_imports values(15, 'Grape', 'Fall', 'Illinois', 72500, 0.35);

select *
from fruit_imports

--1
select state
from fruit_imports
group by state
order by  sum(supply) desc
limit 1

--2
select season, max(cost_per_unit) cost_per_unit
from fruit_imports
group by season


--3
select state
from fruit_imports
group by state, name
having count(name)>1
--4
 
select season, count(name) as count
from fruit_imports
group by season
having count(name)=3 or count(name)=4

--5
select state, sum(supply*cost_per_unit) total_cost
from fruit_imports
group by state
order by sum(supply*cost_per_unit) desc
limit 1

--6

CREATE table fruits (fruit_name varchar(10));
INSERT INTO fruits VALUES ('Orange');
INSERT INTO fruits VALUES ('Apple');
INSERT INTO fruits VALUES (NULL);
INSERT INTO fruits VALUES (NULL);


SELECT COUNT(COALESCE(fruit_name, 'SOMEVALUE'))
FROM fruits;




select first_name,last_name, * 
from employees -- repeat first_name and last_name twice

select employees.department
from employees,departments -- department is both in employees and department, so I have
--to specify the table name before the column name

select employees.department
from employees,departments -- department is both in employees and department, so I have
--to specify the table name before the column name

select e.department
from employees e, departments d --using aliases

select * from employees
where department not in (select department from departments)
--returns everything but the department column

select *
from (select * from employees where salary >150000) a -- we MUST give an alias

select a.employee_name, a.yearly_salary --employee_name and yearly_salary
--not first_name and salary because we have renamed it in the next row
from (select first_name employee_name, salary yearly_salary
	  from employees where salary >150000) a
	  
select a.employee_name, a.yearly_salary --employee_name and yearly_salary
--not first_name and salary because we have renamed it in the next row
from (select first_name employee_name, salary yearly_salary
	  from employees where salary >150000) a,	
	  (select department employee_name from departments) b
--use aliases to be more clear

-- pay attention when using subqueries in select clause
select first_name last_name, salary, (select first_name
									  from employees limit 1)
									  -- it's gonna return only one employee
from employees 

select * from employees
where department in (select department from departments where division='Electronics')

select * from departments

select * from regions
	 
	 
select * from employees
where region_id in (select region_id from regions
					where country in ('Asia','Canada'))
				   and salary>130000


select first_name,department,
(select max(salary) from employees)-salary 
from employees
where region_id in (select region_id from regions
					where country in ('Asia','Canada'))




select * from regions


select * from employees
where region_id in (select region_id 
				 from regions 
				 where country='United States')
-- we use in or  not in because they are a 
--lot of values

select * from employees
where region_id > any(select region_id 
				 from regions 
				 where country='United States')
-- returns true if any of the subquery values
--meet the conditions

select * from employees
where region_id > all(select region_id 
				 from regions 
				 where country='United States')
-- returns true if all the subquery values
--meet the conditions


select * from employees
where department in  (select department from departments
					  where division='Kids') 
and hire_date > all(select hire_date from employees
										  where department='Maintenance')


select salary from employees
group by salary
having count(*) >= all(select count(*) 
					   from employees
					  group by salary)
order by salary desc
limit 1 





create table dupes (id integer, name varchar(10));

insert into dupes values (1,'FRANK');
insert into dupes values (2,'FRANK');
insert into dupes values (3,'ROBERT');
insert into dupes values (4,'ROBERT');
insert into dupes values (5,'SAM');
insert into dupes values (6,'FRANK');
insert into dupes values (7,'PETER');

select * from dupes

select name,max(id) 
from dupes
group by name

delete from dupes
where id not in( select min(id) 
				from dupes 
				group by name)
--delete what is in the where clause


drop table dupes --drop the entire table



select * from employees

select round(avg(salary)) from employees
where salary not in ((select min(salary) from employees),
(select max(salary) from employees))



select student_name from students


select student_enrollment.course_no,student_enrollment.student_no, students.student_name
from (select *
	  from student_enrollment,students,courses)
					   

select student_name from students
where students.student_no in (select student_enrollment.student_no 
							  from student_enrollment
							  where student_enrollment.course_no in
							  (select courses.course_no from courses
							   where courses.course_title='Physics' or
							  courses.course_title='US History')	
select student_name from students
where students.student_no in (select student_enrollment.student_no
from student_enrollment
group by student_no
order by count(course_no) desc
limit 1 )
	


select student_name from students
where age in (select max(age)
				from students) 

select first_name,salary,
case --a conditional expression
when salary <100000 then 'UNDER PAID'
when salary >100000 and salary < 160000 then 'PAID WELL'
when salary >160000 then 'EXECUTIVE'
else 'UNPAID' --if both previous conditions are false
end as category --name of case column
from employees
order by salary desc

select count(*),category from 
(select first_name,salary,
case --a conditional expression
when salary <100000 then 'UNDER PAID'
when salary >100000 and salary < 160000 then 'PAID WELL'
when salary >160000 then 'EXECUTIVE'
else 'UNPAID' --if both previous conditions are false
end as category --name of case column
from employees
order by salary desc ) as a
group by a.category 

select sum(case when salary<100000 then 1 else 0 end) as under_paid,
sum(case when salary>100000 and salary<150000 then 1 else 0 end) as paid_well,
sum(case when salary>150000 then 1 else 0 end) as executive
from employees
--it sums all the values with one



select department, count(*)
from employees
where department in ('Sports', 'Tools','Clothing','Computers')
group by department

select sum(case when department='Sports' then 1 else 0 end) as Sports,
sum(case when department='Tools' then 1 else 0 end) as Tools,
sum(case when department='Clothing' then 1 else 0 end) as Clothing,
sum(case when department='Computers' then 1 else 0 end) as Computers
from employees



select sum(case when department='Sports' then 1 else 0 end) as Sports,
sum(case when department='Tools' then 1 else 0 end) as Tools,
sum(case when department='Clothing' then 1 else 0 end) as Clothing,
sum(case when department='Computers' then 1 else 0 end) as Computers
from employees

select first_name, 
case when region_id=1 then (select country from regions 
							where region_id=1) end region1,
case when region_id=2 then (select country from regions 
							where region_id=2) end region2,
case when region_id=3 then (select country from regions 
							where region_id=3) end region3,
case when region_id=4 then (select country from regions 
							where region_id=4) end region4,
case when region_id=5 then (select country from regions 
							where region_id=5) end region5,
case when region_id=6 then (select country from regions 
							where region_id=6) end region6,
case when region_id=7 then (select country from regions 
							
							
							
select USA + Asia + Canada from(							
select count(a.region1)+count(a.region2)+count(a.region3) as USA
							,count(a.region4)+count(a.region5) as Asia,count(a.region6)
							+count(a.region7) as Canada					
							from(select 
case when region_id=1 then (select country from regions 
							where region_id=1) end region1,
case when region_id=2 then (select country from regions 
							where region_id=2) end region2,
case when region_id=3 then (select country from regions 
							where region_id=3) end region3,
case when region_id=4 then (select country from regions 
							where region_id=4) end region4,
case when region_id=5 then (select country from regions 
							where region_id=5) end region5,
case when region_id=6 then (select country from regions 
							where region_id=6) end region6,
case when region_id=7 then (select country from regions											
							where region_id=7) end region7
from employees ) as a) as b



select name,sum,
case 
when a.sum <= 20000 then 'LOW'
when a.sum >20000 and a.sum<= 50000 then 'ENOUGH'
when a.sum >50000 then 'FULL'
end as category 
from (select name,sum(supply) from FRUIT_IMPORTS group by name) as a


SELECT SUM(CASE WHEN season = 'Winter' THEN total_cost end) as Winter_total,

SUM(CASE WHEN season = 'Summer' THEN total_cost end) as Summer_total,

SUM(CASE WHEN season = 'Spring' THEN total_cost end) as Spring_total,

SUM(CASE WHEN season = 'Fall' THEN total_cost end) as Spring_total,

SUM(CASE WHEN season = 'All Year' THEN total_cost end) as Spring_total

FROM (

select season, sum(supply * cost_per_unit) total_cost

from fruit_imports

group by season

    ) a



select department, count from
(select department,count(first_name)
from employees
group by department) as a
where count > 38

select * from employees

--or
 select department,(select max(salary) from employees where 
				   department=d.department) --get max salary for each department
 from departments d
 where 38< (select count(*) from employees e2
		   where d.department=e2.department)

select department, (select name, max(salary) from employees where 
				   department=d.department)
 

(select first_name,
case when salary >= all(select salary from employees where department=a.department)  
then 'HIGHEST SALARY'
when salary <= all(select salary from employees where department=a.department)  
then'LOWEST SALARY' 
end as salary_department
from employees as a) 

where salary_department='null'
group by department


select 
select department,
case when salary >= all(select salary from employees where department=a.department)  
then 'HIGHEST SALARY'
when salary <= all(select salary from employees where department=a.department)  
then'LOWEST SALARY' 
end as salary_department,
case when salary >= all(select salary from employees where department=a.department)  
then (select salary from employees where salary=a.salary )
when salary <= all(select salary from employees where department=a.department)  
then (select salary from employees where salary=a.salary)
end as salary_department
from employees as a



select first_name,country from employees,regions
where employees.region_id= regions.region_id
--choose the colummns across different tables
--based on different region_id

select first_name, email, department
from employees,regions
where employees.region_id=regions.region_id
and email is not null

select first_name, email, department
from employees,regions
where employees.region_id=regions.region_id
and email is not null



select first_name, email, e.department,division,country
from employees e,departments d,regions r
where e.department=d.department
and e.region_id=r.region_id
and email is not null
--use alias when we have the same column among different tables


select country, count()
from 



select country,count(*) 
from employees e,regions r
where e.region_id=r.region_id
group by country



select first_name,country
from employees inner join regions
on employees.region_id=regions.region_id
--instead of where clause before



select first_name,email,division, country
from employees inner join departments --tables to join
on employees.department=departments.department --common column
inner join regions 

on employees.region_id=regions.region_id--we are adding another inner join
--we are joining the table obtained with the previous result, with regions
where email is not null



select distinct department from employees
--27 departments

select distinct department from departments
--24 departments

select distinct employees.department,
departments.department
from employees inner join departments
on employees.department=departments.department
--only give us the matching department (23)
--also a department in the department table
--not used in employees

select distinct employees.department employees_department,
departments.department departments_department
from employees left join departments
on employees.department=departments.department
--all the departments from 
--employees table regardless they exist
--in department table
--right join does the same thing  with 
--department table

select distinct employees.department employees_department,
departments.department departments_department
from employees full outer join departments
on employees.department=departments.department 



select department from employees
union
select department
from departments

--it stacks the departments and ELIMINATES 
--the duplicates
--n. of columns must match and also data type.
--we cannot put another column

select department from employees
union all
select department
from departments
union select country
from regions
order by department --at the end of the query
--it stacks the departments and DOES NOT ELIMINATE 
--the duplicates


select distinct department from employees
except 
select department
from departments
--all the departments found in the 
--employees table that do not exist
--in the departments table


select distinct employees.department employees_department,
departments.department departments_department
from employees full outer join departments
on employees.department=departments.department 


select department, count(department) from employees
group by department
union all
select 'TOTAL',count(department) as g from employees



select * from employees a,employees b
--every single combinations is returned
--(cartesian product)

select * from employees a cross join departments b
--another option


select a.first_name,a.department, a.hire_date,regions.country from (
select first_name,department
,hire_date,region_id from employees
where hire_date >= all(select hire_date
					  from employees)					  
union all
select first_name,
department,hire_date,region_id from employees
where hire_date <= all(select hire_date
					  from employees)) as a inner join regions
on a.region_id=regions.region_id

select hire_date,salary,
(select sum(salary) from employees e2
where e2.hire_date between e.hire_date-90
and e.hire_date) as spending_pattern
from employees e
order by hire_date





create view v_employee_information as
--it creates a view, a query
--saved in the database
select first_name,email,
e.department,salary,division,region,country
from employees e, departments d,regions r
where e.department=d.department
and e.region_id=r.region_id


select * from v_employee_information

select * 
from (select * from departments) a
--inline view)
-------------------------------------------------------------------------------------

select first_name,department,
(select count(*) from employees e1
where e1.department=e2.department)
from employees e2
group by department,first_name 

--we want to combine grouping columns
--with non grouping columns

select first_name,department,
count(*) over (partition by department ) 
from employees e2
--we want to combine grouping columns
--with non grouping columns
--in this case if we don't put anthing inside over,
--we get the entire count of all the employees
--we put partition by department and we obtain the total
--count for each department

select first_name,department,
sum(salary) over ( ) 
from employees e2

select first_name,department,
count(*) over (partition by department ) dept_count,
region_id,
count(*) over (partition by region_id ) region_count
from employees e2
--instead of 32 correlated subqueries

select first_name,department,
count(*) over () 
from employees
where region_id=3
--we can add a where clause

--1 from clause
--2 where clause
--3 select clause


select first_name,hire_date,salary ,
sum(salary) over (order by hire_date
				 range between unbounded preceding
				 and current row) as running
from employees
--running total
--sums all the rows preceding the current row

select first_name,hire_date,salary ,
sum(salary) over (partition by department order by hire_date
	) as running_total
from employees

select first_name,hire_date,salary ,
sum(salary) over ( order by hire_date rows between 3 preceding
				  and current row
	) as running_total
from employees
--after ordering by hire_date, sum the salary by 3row
--that precedes the current row and the current

select * from(
select first_name,email,department,salary,
rank() over (partition by department order by salary desc)
from employees) a
where rank=8
--employees in the eighth position
--based on their salaries


select first_name,email,department,salary,
ntile(5) over (partition by department order by salary desc) salary_brack
from employees
--splits each department into 5 equal groups of salary

select first_name,email,department,salary,
first_value(salary) over (partition by department
						  order by salary desc) first_value
from employees
--first salary of each department

select first_name,email,department,salary,
nth_value(salary,5) over (partition by department
						  order by salary desc) nth_value
from employees
--chooses the fifth employee salary

select first_name, last_name,salary,
lead(salary) over() next_salary
from employees
--it gives us the next salary

select first_name, last_name,salary,
lag(salary) over() previous_salary
from employees
--it gives us the previous salary

select department, last_name,salary,
lag(salary) over(partition by department order by salary desc) closest_higher_salary
from employees
--the closest highest salary in each department


CREATE TABLE sales
(
	continent varchar(20),
	country varchar(20),
	city varchar(20),
	units_sold integer
);

INSERT INTO sales VALUES ('North America', 'Canada', 'Toronto', 10000);
INSERT INTO sales VALUES ('North America', 'Canada', 'Montreal', 5000);
INSERT INTO sales VALUES ('North America', 'Canada', 'Vancouver', 15000);
INSERT INTO sales VALUES ('Asia', 'China', 'Hong Kong', 7000);
INSERT INTO sales VALUES ('Asia', 'China', 'Shanghai', 3000);
INSERT INTO sales VALUES ('Asia', 'Japan', 'Tokyo', 5000);
INSERT INTO sales VALUES ('Europe', 'UK', 'London', 6000);
INSERT INTO sales VALUES ('Europe', 'UK', 'Manchester', 12000);
INSERT INTO sales VALUES ('Europe', 'France', 'Paris', 5000);

select * from sales
order by continent,country,city


select continent, sum(units_sold)
from sales
group by continent

select city, sum(units_sold)
from sales
group by city

select continent, country,city,sum(units_sold)
from sales
group by grouping sets(continent,country,city,())

--breakdown by each group separately
--() the total sum when we are not grouping by anything

select continent, country,city,sum(units_sold)
from sales
group by rollup(continent,country,city)
--we don't need ()
--in the first set of data, the sum is obtaining
--considering that we group by all three columns
--in the second set of data, the sum is obtaining
--considering that we group by the first 2 columns
--in the third set of data, the sum is obtaining
--considering that we group by the first column
--at the beginning the first row shows if we are grouping
--by no columns

select continent, country,city,sum(units_sold)
from sales
group by cube(continent,country,city)
--all the possible combinations				
	
select department,first_name,salary,salary_department from(
select department,first_name, salary,
case when salary >= all(select salary from employees where department=a.department)  
then 'HIGHEST SALARY'
when salary <= all(select salary from employees where department=a.department)  
then'LOWEST SALARY' 
end as salary_department
from employees as a) as b
where salary_department != '[null] '
order by department,salary_department





select student_name,student_enrollment.course_no, teach.last_name
from students left join student_enrollment
on students.student_no=student_enrollment.student_no
join teach on teach.course_no=student_enrollment.course_no
order by course_no



select student_name,course_no,min(last_name)--, student_name
from (select student_name,student_enrollment.course_no, teach.last_name
from students left join student_enrollment
on students.student_no=student_enrollment.student_no
join teach on teach.course_no=student_enrollment.course_no
order by course_no) a
group by course_no,student_name--, last_name--,student_name

select first_name,salary from employees
where salary > (select round(avg(salary)) from employees)


select student_name,course_no from students
left join student_enrollment
on student_enrollment.student_no=students.student_no



SELECT * FROM students

WHERE student_no NOT IN (

    SELECT student_no

    FROM student_enrollment

    WHERE course_no = 'CS180'

    ) 
order by student_name




SELECT * FROM students

WHERE student_no IN (

    SELECT student_no

    FROM student_enrollment

    WHERE course_no = 'CS110' or course_no='CS107'
	
    ) and student_no not in (SELECT student_no

    FROM student_enrollment

    WHERE course_no = 'CS110' and course_no='CS107')
order by student_name


SELECT s.*

FROM students s, student_enrollment se

WHERE s.student_no = se.student_no

AND se.course_no IN ('CS110', 'CS107')

AND s.student_no NOT IN ( SELECT a.student_no

                          FROM student_enrollment a, student_enrollment b

                          WHERE a.student_no = b.student_no

                          AND a.course_no = 'CS110'

                          AND b.course_no = 'CS107')



SELECT course_no FROM students s, student_enrollment se 
where s.student_no=se.student_no


select course_no,s.student_no,se.student_no from students s join student_enrollment se 
 on s.student_no=se.student_no
 
 
SELECT s.*

FROM students s, student_enrollment se

WHERE s.student_no = se.student_no

AND s.student_no NOT IN ( SELECT student_no

                          FROM student_enrollment

                          WHERE course_no != 'CS220')
 
 
SELECT student_name, count(se.course_no)

FROM students s, student_enrollment se

WHERE s.student_no = se.student_no
 
group by student_name

having count(se.course_no)<3


select * from student_enrollment

select * from professors
select * from students 
select * from courses
select * from teach



select distinct student_name, rank,age from (
SELECT student_name,
rank() over(order by age),age
FROM students s) as a
where a.rank <=3
order by age


SELECT s1.*

FROM students s1

WHERE 2 >= (SELECT count(*)

                FROM students s2

                WHERE s2.age < s1.age)


 
group by student_name

having count(se.course_no)<3




SELECT s.*

FROM students s, student_enrollment se

WHERE s.student_no = se.student_no

AND s.student_no NOT IN ( SELECT student_no

                          FROM student_enrollment

                          WHERE course_no != 'CS220')


