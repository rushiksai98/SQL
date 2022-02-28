#SQL
#SQL code for Advanced Database Projects using Oracle SQL Developer App
-- Problem 1: Create tables with appropriate primary key and foreign keys

-- Restaurant table
create table restaurant (
    rID int,
    rName varchar(30),
    StrAddress varchar(30),
    Zip number,
    primary key (rID)
    );
    
-- Driver table
create table driver (
    dID int,
    dFname varchar(30),
    dLname varchar(30),
    primary key (dID)
    );

-- Customer table    
create table customer (
    cID int,
    cFname varchar(30),
    cLname varchar(30),
    StrAddress varchar(30),
    Zip number,
    primary key (cID)
    );
 
-- Orders table   
create table orders (
    oID int,
    rID int,
    cID int,
    amount decimal,
    dID int,
    primary key (oID),
    foreign key (rID) references restaurant(rID),
    foreign key (cID) references customer(cID),
    foreign key (dID) references driver(dID));

-- Tips table    
create table tips (
    tipID int,
    oID int,
    dID int,
    tip decimal(4,2),
    primary key (tipID),
    foreign key (oID) references orders(oID),
    foreign key (dID) references driver(dID));
    
-- Problem 2 : INSERT statements

-- 2a) Insert restaurant
insert into restaurant
values(1,'Good Food','100 Main St',21250);

insert into restaurant
values(2,'Happy Belly','101 Main St',21043);

insert into restaurant
values(3,'Little Italy','200 Plum St',21250);

insert into restaurant
values(4,'American','210 Plum St',21250);

-- 2b) Insert driver
insert into driver
values(100,'Jack','Quick');

insert into driver
values(101,'Joe','Fast');

insert into driver
values(102,'Marie','Bay');

insert into driver
values(103,'Pam','White');

insert into driver
values(105,'Kumar','Patel');

-- 2c) Insert customer
insert into customer
values(500,'Mary','Slim','10 Main St',21043);

insert into customer
values(510,'Jude','Bigbelly','20 Plenty St',21042);

insert into customer
values(520,'Pamela','Reddy','20 Main St',21043);

insert into customer
values(530,'Ann','Phat','101 Main St',21250);

-- 2d) Insert orders
insert into orders
values(700,1,500,72.80,100);

insert into orders
values(701,1,510,99,102);

insert into orders
values(702,1,530,150.60,103);

insert into orders
values(703,2,530,80,105);

insert into orders
values(704,3,530,90,102);

insert into orders
values(705,4,520,100,101);

insert into orders
values(706,4,510,134,100);

insert into orders
values(707,4,530,66.20,100);

-- 2e) Insert tips

insert into tips
values(1,700,100,14.56);

insert into tips
values(2,701,102,19.8);

insert into tips
values(3,702,103,30.12);

insert into tips
values(4,703,105,16);

insert into tips
values(5,704,102,18);

insert into tips
values(6,705,101,20);

insert into tips
values(7,706,100,26.8);

insert into tips
values(8,707,100,13.24);

-- Problem 3: SQL Query

-- Names of Restaurants located in zip 21250
select rName
from restaurant
where Zip='21250';

-- Name of restaurants Jude placed order at
select rName
from restaurant,customer, orders
where cFname= 'Jude' and customer.cID = orders.cID and restaurant.rID = orders.rID;

-- Total tip of each drivers in descending order with their first and last names
select dFname, dLname, sum(tip) as total_tip
from driver, tips
where driver.dID = tips.dID
group by dFname, dLname
order by sum(tip) desc;

drop table tips;
drop table orders;
drop table customer;
drop table driver;
drop table restaurant;
