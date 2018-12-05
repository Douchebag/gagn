```sql
create database kt_MovieCo;
use kt_MovieCo;

------------- CREATE TABLES --------------

-- 1
create table membership (
    mem_num int primary key not null auto_increment,
    mem_fname varchar(40) not null,
    mem_lname varchar(40),
    mem_street varchar(60) not null,
    mem_city varchar(20) not null,
    mem_state varchar(60) not null, 
    mem_zip int(5) not null,
    mem_balance decimal(4, 2) not null
);
alter table membership auto_increment = 102;

create table rental (
    rent_num int primary key not null auto_increment,
    rent_date date not null,
    mem_num int not null,
    foreign key (mem_num) references membership(mem_num)                
);
alter table rental auto_increment = 1001;

create table price (
    price_code int primary key auto_increment,
    price_description varchar(70),
    price_rentfee decimal(4, 2) not null,
    price_dailylatefee decimal(4, 2) not null
);
 
create table movie (
    movie_num int primary key not null auto_increment,
    movie_title varchar(55) not null,
    movie_year int(4) not null,
    movie_cost decimal(4, 2) not null,
    movie_genre varchar(20) not null,
    price_code int(1) not null,
    foreign key (price_code) references price(price_code)            
);
alter table movie auto_increment = 1234;

create table video (
    vid_num int primary key not null,
    vid_indate date not null,
    movie_num int not null,
    foreign key (movie_num) references movie(movie_num)             
);

create table detailRental (
    rent_num int not null,
    vid_num int not null,
    detail_fee decimal(4,1) not null,
    detail_duedate date not null,
    detail_returndate date,
    detail_dailylatefee int not null,
    primary key (rent_num, vid_num),
    foreign key (rent_num) references rental(rent_num),
    foreign key (vid_num) references video(vid_num)    
);

-------- DROP ---------
drop table video;
drop table movie;
drop table price;
drop table membership;
drop table rental;
drop table detailrental;
-----------------------

------------------------------ INSERT --------------------------------

-- 2
insert into membership
values
(102, 'Tami', 'Dawson', '2632 Takli Circle', 'Norene', 'TN', 37136, 11), 
(103, 'Curt', 'Knight', '4025 Cornell Court', 'Flatgap', 'KY', 41219, 6),
(104, 'Jamal', 'Melendez', '788 East 145th Avenue', 'Quebeck', 'TN', 38579, 0),
(105, 'Iva', 'Mcclain', '6045 Musket Ball Circle', 'Summit', 'KY', 42783, 15), 
(106, 'Miranda', 'Parks', '4469 Maxwell Place', 'Germantown', 'TN', 38183, 0),
(107, 'Rosario', 'Elliott', '7578 Danner Avenue', 'Columbia', 'TN', 38402, 5), 
(108, 'Mattie', 'Guy', '4390 Evergreen Street', 'Lily', 'KY', 40740, 0), 
(109, 'Clint', 'Ochoa', '1711 Elm Street', 'Greeneville', 'TN', 37745, 10), 
(110, 'Lewis', 'Rosales', '4524 Southwind Circle', 'Counce', 'TN', 38326, 0), 
(111, 'Stacy', 'Mann', '2789 East Cook Avenue', 'Murfreesboro', 'TN', 37132, 8),
(112, 'Luis', 'Trujillo', '7267 Melvin Avenue', 'Heiskell', 'TN', 37754, 3) ,
(113, 'Minnie', 'Gonzales', '6430 Vasili Drive', 'Williston', 'TN', 38076, 01); 


insert into rental
values
(1001, '2009-1-03', 103),
(1002, '2009-1-03', 105),
(1003, '2009-2-03', 102),
(1004, '2009-2-03', 110),
(1005, '2009-2-03', 111),
(1006, '2009-2-03', 107),
(1007, '2009-2-03', 104),
(1008, '2009-3-03', 105),
(1009, '2009-3-03', 111);

insert into price
values
(1, 'Standard', 2, 1),
(2, 'New Release', 3.5, 3),
(3, 'Discount', 1.5, 1),
(4, 'Weekly Special', 1, 0.5);

insert into movie
values
(1234, 'The Cesar Family Christmas', 2007, 39.95, 'FAMILY', 2),
(1235, 'Smokey Mountain Wildlife', 2004, 59.95, 'ACTION', 1),
(1236, 'Richard Goodhope', 2008, 59.95, 'DRAMA', 2),
(1237, 'Beatnik Fever', 2007, 29.95, 'COMEDY', 2),
(1238, 'Constant Companion', 2008, 89.95, 'DRAMA', 2),
(1239, 'Where Hope Dies', 1998, 25.49, 'DRAMA', 3),
(1245, 'Time to Burn', 2005, 45.49, 'ACTION', 1),
(1246, 'What He Doesnt Know', 2006, 58.29, 'COMEDY', 1);

insert into video
values
    (54321, '2008-6-18', 1234),
    (54324, '2008-6-18', 1234),
    (54325, '2008-6-18', 1234),
    (34341, '2007-1-22', 1235),
    (34342, '2007-1-22', 1235),
    (34366, '2009-3-02', 1236),
    (34367, '2009-3-02', 1236),
    (34368, '2009-3-02', 1236),
    (34369, '2009-3-02', 1236),
    (44392, '2008-10-21', 1237),
    (44397, '2008-10-21', 1237),
    (59237, '2009-2-14', 1237),
    (61388, '2007-1-25', 1239),
    (61353, '2006-1-28', 1245),
    (61354, '2006-1-28', 1245),
    (61367, '2008-7-30', 1246),
    (61369, '2008-7-30', 1246);


insert into detailrental
values
(1001, 34342, 2, '2009-3-04', '2009-3-02', 1),
(1001, 61353, 2, '2009-3-04', '2009-3-03', 1),
(1002, 59237, 3.5, '2009-3-04', '2009-3-04', 3),
(1003, 54325, 3.5, '2009-3-04', '2009-3-09', 3),
(1003, 61369, 2, '2009-3-06', '2009-3-09', 1),
(1003, 61388, 0, '2009-3-06', '2009-3-09', 1),
(1004, 44392, 3.5, '2009-3-05', '2009-3-07', 3),
(1004, 34367, 3.5, '2009-3-05', '2009-3-07', 3),
(1004, 34341, 2, '2009-3-07', '2009-3-07', 1),
(1005, 34342, 2, '2009-3-07', '2009-3-05', 1),
(1005, 44397, 3.5, '2009-3-05', '2009-3-05', 3),
(1006, 34366, 3.5, '2009-3-05', '2009-3-04', 3),
(1006, 61367, 2, '2009-3-07', null, 1),
(1007, 34368, 3.5, '2009-3-05', null, 3),
(1008, 34369, 3.5, '2009-3-05', '2009-3-05', 3),
(1009, 54324, 3.5, '2009-3-05', null, 3),
(1001, 34366, 3.5, '2009-3-04', '2009-3-02', 3);
```
```sql
-------------- SELECT STATEMENTS ---------------

-- 3
select movie_title, movie_year, movie_cost
from movie
where movie_title like '%hope%'
order by movie_title asc;
```
![](https://github.com/Douchebag/gagn/blob/master/pics/3.PNG)
```sql
-- 4
select movie_title, movie_genre, movie_year
from movie
where movie_genre like 'ACTION';
```
![](https://github.com/Douchebag/gagn/blob/master/pics/4.PNG)
```sql
-- 5
select movie_num, movie_title, movie_cost
from movie
where movie_cost > 40;
```
![](https://github.com/Douchebag/gagn/blob/master/pics/5.PNG)
```sql
-- 6
select movie_num, movie_title, movie_cost, movie_genre
from movie
where movie_cost < 50 and movie_genre = 'ACTION' or movie_cost < 50 and movie_genre = 'COMEDY'
order by movie_genre asc;
```
![](https://github.com/Douchebag/gagn/blob/master/pics/6.PNG)
```sql
-- 7
select movie_num, concat(movie_title, ' (', movie_year, ') ', movie_genre) as "Movie Description"
from movie;
```
![](https://github.com/Douchebag/gagn/blob/master/pics/7.PNG)
```sql
-- 8
select movie_genre, count(movie_genre)
from movie
group by movie_genre;
```
![](https://github.com/Douchebag/gagn/blob/master/pics/8.PNG)
```sql
-- 9
select avg(movie_cost) as "Avg Movie Price"
from movie;
```
![](https://github.com/Douchebag/gagn/blob/master/pics/9.PNG)
```sql
-- 10
select round(avg(movie_cost), 2) as "Avg Movie Price", movie_genre
from movie
GROUP BY movie_genre;
```
![](https://github.com/Douchebag/gagn/blob/master/pics/10.PNG)
```sql
-- 11
select movie_title, movie_genre, price.price_description as 'description', price.price_rentfee as 'rentfee'
from movie
inner join price on (movie.price_code = price.price_code);
```
![](https://github.com/Douchebag/gagn/blob/master/pics/11.PNG)
```sql
-- 12
select movie_genre, round(avg(price.price_rentfee), 2) as 'avg rentfee'
from movie
inner join price on movie.price_code = price.price_code
group by movie_genre;
```
![](https://github.com/Douchebag/gagn/blob/master/pics/12.PNG)
```sql
-- 13
select movie_title, movie_year, round((movie_cost/price.price_rentfee), 2) as 'Breakeven Rentals'
from movie
inner join price on (movie.price_code = price.price_code);
```
![](https://github.com/Douchebag/gagn/blob/master/pics/13.PNG)
```sql
-- 14
select movie_title, movie_year
from movie
where price_code;
```
![](https://github.com/Douchebag/gagn/blob/master/pics/14.PNG)
```sql
-- 15
select movie_title, movie_year, movie_cost
from movie
where movie_cost between 44.99 and 49.99;
```
![](https://github.com/Douchebag/gagn/blob/master/pics/15.PNG)
```sql
-- 16
select movie_title, movie_year, price.price_description as price_description, price.price_rentfee as price_rentfee, movie_genre
from movie
inner join price on (movie.price_code = price.price_code)
where movie_genre like 'family' or movie_genre like 'comedy' or movie_genre like 'drama';
```
![](https://github.com/Douchebag/gagn/blob/master/pics/16.PNG)
```sql
-- 17
select min(mem_balance) as 'minimum balance', max(mem_balance) as 'maximum balance', avg(mem_balance) as 'average balance'
from membership;
```
![](https://github.com/Douchebag/gagn/blob/master/pics/17.PNG)
```sql
-- 18
select concat(mem_fname, ' ', mem_lname) as 'membership name', concat(mem_street, ' ', mem_city, ' ', mem_state, ' ', mem_zip) as 'membership address'
from membership;
```
![](https://github.com/Douchebag/gagn/blob/master/pics/18.PNG)
```sql
-- 19
select rental.rent_num, rental.rent_date, video.vid_num, movie.movie_title as movie_title, detailrental.detail_duedate
as due_date, detailrental.detail_returndate as return_date
from rental
inner join detailrental on (detailrental.rent_num = rental.rent_num)
inner join video on (video.vid_num = detailrental.vid_num)
inner join movie on (video.movie_num = movie.movie_num)
where detailrental.detail_returndate > detailrental.detail_duedate;
```
![](https://github.com/Douchebag/gagn/blob/master/pics/19.PNG)
```sql
-- 20
select rental.rent_num, rent_date, detailRental.vid_num, movie.movie_title, detailrental.detail_duedate, detailrental.detail_returndate, datediff(detailrental.detail_returndate, detailrental.detail_duedate) as 'days past due'
from rental
inner join detailrental on (detailrental.rent_num = rental.rent_num)
inner join video on (video.vid_num = detailrental.vid_num)
inner join movie on (video.movie_num = movie.movie_num)
order by rental.rent_num, movie.movie_title;
```
![](https://github.com/Douchebag/gagn/blob/master/pics/20.PNG)
```sql
-- 21
select rental.rent_num as rent_num, rental.rent_date as rent_date,movie.movie_title as movie_title, detailrental.detail_fee as detail_fee
from rental
inner join detailrental on (detailrental.rent_num = rental.rent_num)
inner join video on (video.vid_num = detailrental.vid_num)
inner join movie on (video.movie_num = movie.movie_num)
where detailrental.detail_returndate <= detailrental.detail_duedate;
```
![](https://github.com/Douchebag/gagn/blob/master/pics/21.PNG)
```sql
-- 22
select m.mem_num, m.mem_lname, m.mem_fname, sum(detailrental.detail_fee) 
from membership m
inner join rental on (rental.mem_num = m.mem_num)
inner join detailrental on (detailrental.rent_num = rental.rent_num)
group by m.mem_num;
```
![](https://github.com/Douchebag/gagn/blob/master/pics/22.PNG)
```sql
-- 23
select a.movie_num, a.movie_genre, a.movie_cost, b.avg_cost,
       (a.movie_cost - b.avg_cost) / b.avg_cost * 100 as percentage_diff
from movie a
inner join (
    select movie_genre, avg(movie_cost) as avg_cost from movie
    group by movie_genre
) b
using (movie_genre);
```
![](https://github.com/Douchebag/gagn/blob/master/pics/23.PNG)
```sql
-- 24
alter table detailrental add detail_dayslate int(3);
```
![](https://github.com/Douchebag/gagn/blob/master/pics/24.PNG)
```sql
-- 25
alter table video add vid_status char(4) not null default 'IN' check (vid_status in ('IN', 'OUT', 'LOST'));
```
![](https://github.com/Douchebag/gagn/blob/master/pics/25.PNG)
```sql
-- 26
update video 
set vid_status = 'out'
where vid_num in (select vid_num from detailrental where detail_returndate is null);
```
![](https://github.com/Douchebag/gagn/blob/master/pics/26.PNG)
```sql
-- 27
alter table price add column price_rentdays int(2) not null default 3;
```
![](https://github.com/Douchebag/gagn/blob/master/pics/27.PNG)
```sql
-- 28
update price 
set price_rentdays = 5
where price_code in (1, 3);
update price 
set price_rentdays = 7
where price_code = 4;
```
![](https://github.com/Douchebag/gagn/blob/master/pics/28.PNG)
```sql
-- 29
delimiter //
create procedure prc_new_rental (m_num int)
begin
	declare mem_num_count int; 
	declare prev_mem_balance decimal(4, 2);
	select count(*)
	into mem_num_count
	from membership
	where mem_num = m_num;
	if mem_num_count = 0 then

		select 'membership does exist';

	else
		select mem_balance
		into prev_mem_balance
		from membership
		where mem_num = m_num;
		select concat('previous balance: ', prev_mem_balance) as 'previous membership balance';
		insert into rental (rent_date, mem_num)
		values 
		(sysdate(), m_num);
	end if;
end//

call prc_new_rental(102);
```
![](https://github.com/Douchebag/gagn/blob/master/pics/29.PNG)
