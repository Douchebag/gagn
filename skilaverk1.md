# Skilaverkefni 1

1. 
![alt text](https://github.com/Douchebag/gagn/blob/master/skilaverk%201.PNG?raw=true "Spurning 1")

2. 
```sql
CREATE DATABASE 0102992099_SaleCo;

USE 0102992099_SaleCo;

CREATE TABLE Customer (
	cus_code int(5) PRIMARY KEY NOT NULL,
    cus_lname VARCHAR(20) NOT NULL,
    cus_fname VARCHAR(20) NOT NULL,
    cus_initial char(1) NOT NULL,
    cus_areacode int(4) DEFAULT 0181,
    cus_phone INT(7),
    cus_balance DECIMAL(18, 2) DEFAULT 0.00
);

ALTER TABLE Customer AUTO_INCREMENT=10010;

CREATE TABLE Invoice (
	inv_number INT(4) PRIMARY KEY NOT NULL,
    cus_code INT(5) NOT NULL,
    inv_date date,
    FOREIGN KEY (cus_code) REFERENCES Customer(cus_code) ON UPDATE CASCADE
);

ALTER TABLE Invoice AUTO_INCREMENT=1001;

CREATE TABLE Line (
	inv_number INT(4) NOT NULL,
	lin_num INT(4) NOT NULL,
    prod_code VARCHAR(8),
    line_units DECIMAL(18, 2) DEFAULT 0.00,
    line_price DECIMAL(18, 2) DEFAULT 0.00
);

CREATE TABLE Product (
	prod_code VARCHAR(8) PRIMARY KEY NOT NULL,
    prod_descript VARCHAR(50) NOT NULL,
    prod_price DECIMAL(18, 2) NOT NULL,
    prod_on_hand INT(10),
    vend_code INT(5) NOT NULL,
    FOREIGN KEY (vend_code) REFERENCES Vendor(vend_code)
);

CREATE TABLE Vendor (
	vend_code INT(5) PRIMARY KEY NOT NULL,
    vend_contact VARCHAR(20) NOT NULL,
    vend_areacode INT(4) NOT NULL,
    vend_phone INT(7) NOT NULL
);
```
3. 
```sql
// other pk/fk constraints were added upon creating the tables
alter table Line add constraint inv_number foreign key (inv_number) references Invoice (inv_number) ON DELETE CASCADE;
alter table Line add constraint prod_code foreign key (prod_code) references Product (prod_code) ON UPDATE SET NULL;
```
4. Added defaults upon creation of the tables
5.
```sql
INSERT INTO Customer(cus_code, cus_lname, cus_fname,cus_initial,cus_areacode, cus_phone, cus_balance)
VALUES 
(10010,'Ramas','Alfred','A','0181','8442573',0),
(10011,'Dunne','Leona','K','0161','8941238',0),
(10012,'Smith','Kathy','W','0181','8942285',345.86);

INSERT INTO Invoice
VALUES 
(1001,10010,'2008-01-16'),
(1002,10011,'2008-01-16'),
(1003,10012,'2008-01-16');

INSERT INTO Vendor
VALUES
(21225, 'Smithson', '0181', '2233234'),
(21226, 'Flushing', '0113', '2158995'),
(21231, 'Singh', '0181', '2283245');

INSERT INTO Product(prod_code, prod_descript, prod_price, prod_on_hand, vend_code)
VALUES
('11QER/31','Power painter, 15 psi., 3-nozzle', 109.99, 5, 21225),
('13-Q2/P2','7.25-cm. pwr. saw blade', 14.99, 15, 21226),
('14-Q1/L3','9.00-cm. pwr. saw blade', 17.49, 12, 21231);

INSERT INTO Line
VALUES
(1001, 1,'13-Q2/P2', 1, 14.99),
(1001, 2,'13-Q2/P2', 1, 9.95),
(1002, 1,'14-Q1/L3', 2, 4.99);
```
6.
```sql
CREATE TABLE Employees(
	EMP_NUM INT(5) PRIMARY KEY AUTO_INCREMENT NOT NULL, 
    EMP_TITLE CHAR(10) NOT NULL, 
    EMP_LNAME VARCHAR(15) NOT NULL, 
    EMP_FNAME VARCHAR(15) NOT NULL, 
    EMP_INITIAL CHAR(1) NOT NULL, 
    EMP_DOB DATETIME,
    EMP_HIR_DATE DATETIME,
    EMP_AREACODE CHAR(5) NOT NULL,
    EMP_PHONE CHAR(8),
    EMP_MGR INT
);


alter table Customer add emp_num int(5);
alter table Customer add constraint emp_num foreign key (emp_num) references Employees (EMP_NUM);

alter table Product add emp_num int(5);
alter table Product add constraint emp_num1 foreign key (emp_num) references Employees (EMP_NUM);
```
