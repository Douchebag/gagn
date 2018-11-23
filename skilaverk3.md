# Skilaverkefni 3

```sql
--------------- 1
create database 0102992099_company;
use 0102992099_company;

create table dept
(
  dept_no int not null,
  dept_name varchar(100) not null,
  dept_location varchar(100) not null,
  primary key (dept_no)
);
create table employee 
(
  emp_id int not null,
  emp_name varchar(100) not null,
  mgr_emp_id int,
  dept_no int not null,
  salary  double  not null,
  primary key (emp_id),
  key employee_mgr_emp_id (mgr_emp_id),
  foreign key fk_employee_dept_dept_no (dept_no) references dept (dept_no) on delete no action on update no action
);

insert into dept values 
(1, 'Dept-1', 'Chicago'), 
(2, 'Dept-2', 'London'),
(3, 'Dept-3', 'Reykjavik'),
(4, 'Dept-4', 'Rabat');

insert into employee values 
(1, 'Clark Mgr', null, 1, 450000),
(2, 'Cameron Emp', 2, 1, 300000),
(3, 'Charlie Emp', 3, 1, 500000),
(4, 'Layton Emp', null, 2, 250000),
(5, 'Linda Emp', null, 2, 370000),
(6, 'Mikel Mor', null, 3, 290000),
(7, 'Mic Coleman', null, 3, 400000),
(8, 'Doud Valantino', null, 3, 300000);

--------------- 2
create table deptsal(dept_no int not null, totalsalary int, foreign key (dept_no) references dept(dept_no));

insert into deptsal 
values
(1, 0),
(2, 0),
(3, 0),
(4, 0);

--------------- 3
delimiter //
create procedure updateSalary (deptNum int)
	begin
    update deptsal
    set totalsalary = (select sum(salary) from employee where dept_no = deptNum)
    where dept_no = deptNum;
    end//
    
delimiter ;

call updateSalary(1);
call updateSalary(2);
call updateSalary(3);
call updateSalary(4);
    
select * from deptsal;

--------------- 4
SHOW PROCEDURE STATUS where db = '0102992099_company';

--------------- 5
drop procedure updateSalary;

--------------- 6
update deptsal
set totalsalary = 0;

--------------- 7
delimiter //

create procedure updateSalaryWhile ()
begin
    declare counter int;
    set counter = 1;
    while counter <= (select count(*) from deptsal) DO
		update deptsal
		set totalsalary = (select sum(salary) from employee where dept_no = counter)
		where dept_no = counter;
		set counter = counter +1;
    end while;
end//

call updateSalaryWhile();

--------------- 8
delimiter //
create procedure uSalaryCurs ()
begin
	declare finished integer;
	declare deptNumCur integer;
    declare totalSalCur integer;
	declare updateSalaryCursor cursor for
		select dept_no, sum(salary) from employee group by dept_no;
	declare continue handler 
	for not found set finished = 1;

	open updateSalaryCursor;
	repeat
		fetch updateSalaryCursor into deptNumCur, totalSalCur;
        update deptsal set totalsalary = totalSalCur where dept_no = deptNumCur;
		until finished = 1
	end repeat;
	close updateSalaryCursor;
end//

drop procedure uSalaryCurs;
call uSalaryCurs();

--------------- 9
delimiter //
create procedure tenPercIncr ()
begin
    declare counter int;
    set counter = 1;
    while counter <= (select count(*) from employee) DO
		update employee
		set salary = salary + (salary * 0.10)
		where emp_id = counter;
		set counter = counter +1;
    end while;
end//

call tenPercIncr();

--------------- 10

--------------- a
delimiter //
create trigger update_salary
after insert on employee
for each row 
begin      
	 if new.dept_no is not null then		  
			update deptsal           
			set totalsalary = totalsalary + new.salary          
			where dept_no = new.dept_no;	  
	 end if;      
end//

insert into employee values (9, 'Fred', null, 1, 350000);

--------------- b
delimiter //
create trigger update_salary_delete
after delete on employee
for each row 
begin      
	 if old.dept_no is not null then		  
			update deptsal           
			set totalsalary = totalsalary - old.salary          
			where dept_no = old.dept_no;	  
	 end if;      
end//

delete from employee where emp_id = 9;
```
