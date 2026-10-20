# SQL PL/SQL Practicals

This repository contains SQL and PL/SQL practical exercises covering variables, control statements, loops, cursors, procedures, functions, triggers, exceptions, and sequence handling.

---

## Prac 1

### Q1: Display a number entered by the user

```sql
SET SERVEROUTPUT ON;
declare
x int;
begin
x := &x;
dbms_output.put_line('Your number is = '||x);
end;
/
```

### Q2: Display a message entered by the user

```sql
SET SERVEROUTPUT ON;
declare
x varchar2(30);
begin
x := '&x';
dbms_output.put_line('Your message is = '||x);
end;
/
```

### Q3: Area of a rectangle

```sql
SET SERVEROUTPUT ON;
declare
length int;
breadth int;
begin
length := &length;
breadth := &breadth;
dbms_output.put_line('Area of rectangle is = ' ||(length*breadth));
end;
/
```

### Q4: Sum of first 10 natural numbers

```sql
SET SERVEROUTPUT ON;
declare
i integer;
s integer;
begin
s := 0;
for i in 1..10 loop
s := s+i;
end loop;
dbms_output.put_line('Sum = '||s);
end;
/
```

---

## Prac 2

### Q2: Sum of first 10 odd numbers

```sql
SET SERVEROUTPUT ON;
declare
i int := 1;
total int := 0;
begin
while i<=19 loop
total := total+i;
i := i+2;
end loop;
dbms_output.put_line('Sum : '|| total);
end;
/
```

### Q3: Insert area of circles into table `AOC`

```sql
declare
sno int := 1;
rad int := 1;
area float;
begin
while rad<10 loop
area := 3.14*rad*rad;
insert into aoc values(sno, rad, area);
sno := sno+1;
rad := rad+1;
end loop;
end;
/
```

### Q4: Factorial of a number

```sql
SET SERVEROUTPUT ON;
declare
n1 int := 13;
factorial int := 1;
begin
while n1>0 loop
factorial := factorial * n1;
n1 := n1-1;
end loop;
dbms_output.put_line('Factorial : '||factorial);
end;
/
```

---

## Prac 3

### Q1: CASE statement for owner name

```sql
SET SERVEROUTPUT ON;
declare
username varchar(10) := '&username';
begin
case username
when 'SYS' then dbms_output.put_line('The Owner is SYS');
when 'SYSTEM' then dbms_output.put_line('The Owner is SYSTEM');
when 'HR' then dbms_output.put_line('The Owner is HR');
when 'SCOTT' then dbms_output.put_line('The Owner is SCOTT');
else dbms_output.put_line('Invalid Choice');
end case;
end;
/
```

### Q2: Check whether a number is greater than 100

```sql
SET SERVEROUTPUT ON;
declare
n int;
begin
n := &n;
if n<100 then
dbms_output.put_line('Number is smaller than 100.');
else
dbms_output.put_line('Number is greater than 100.');
end if;
end;
/
```

### Q3: Check salary range for employee 7900

```sql
SET SERVEROUTPUT ON;
declare
s int;
begin
select sal into s from emp where empno=7900;
if s>=1000 and s<=5000 then
dbms_output.put_line('Salary: '||s);
dbms_output.put_line('Salary lies in range 1000-5000');
else
dbms_output.put_line('Salary: '||s);
dbms_output.put_line('Salary does not lie in range 1000-5000');
end if;
end;
/
```

### Q4: Check whether a character is a vowel

```sql
SET SERVEROUTPUT ON;
declare
a char(1) := '&a';
begin
case a
when 'a' then dbms_output.put_line('This alphabet is a vowel');
when 'e' then dbms_output.put_line('This alphabet is a vowel');
when 'i' then dbms_output.put_line('This alphabet is a vowel');
when 'o' then dbms_output.put_line('This alphabet is a vowel');
when 'u' then dbms_output.put_line('This alphabet is a vowel');
when 'A' then dbms_output.put_line('This alphabet is a vowel');
when 'E' then dbms_output.put_line('This alphabet is a vowel');
when 'I' then dbms_output.put_line('This alphabet is a vowel');
when 'O' then dbms_output.put_line('This alphabet is a vowel');
when 'U' then dbms_output.put_line('This alphabet is a vowel');
else dbms_output.put_line('This alphabet is not a vowel');
end case;
end;
/
```

---

## Prac 4

### Q1: Sequence with `CYCLE`, `ALTER SEQUENCE`, and insert values

```sql
create sequence s maxvalue 20 cycle cache 6;

alter sequence s
increment by 3
maxvalue 20
cache 5;

create table sequence(s int);

insert into sequence values(s.nextval);
insert into sequence values(s.nextval);
insert into sequence values(s.nextval);
insert into sequence values(s.nextval);
insert into sequence values(s.nextval);
insert into sequence values(s.nextval);
insert into sequence values(s.nextval);
insert into sequence values(s.nextval);
insert into sequence values(s.nextval);
insert into sequence values(s.nextval);
insert into sequence values(s.nextval);

select * from sequence;
```

### Q2: Sequence generating 10, 20, 30 ... 100 in table `product`

```sql
create sequence ps
start with 10
maxvalue 100
increment by 10;

create table product(productno int, product_name varchar(10));

insert into product values(ps.nextval, 'Apple');
insert into product values(ps.nextval, 'Google');
insert into product values(ps.nextval, 'IBM');
insert into product values(ps.nextval, 'Verizon');
insert into product values(ps.nextval, 'Supercell');
insert into product values(ps.nextval, 'Tencent');
insert into product values(ps.nextval, 'Alibaba');
insert into product values(ps.nextval, 'Samsung');
insert into product values(ps.nextval, 'Nike');
insert into product values(ps.nextval, 'Adidas');

select * from product;
```

---

## Prac 5

### Q1: Update salary by 500 using an implicit cursor

```sql
SET SERVEROUTPUT ON;
declare
dno int := &dno;
begin
update emp
set sal = sal+500
where deptno = dno;
if sql%found then
dbms_output.put_line('Number of rows updated: '||sql%rowcount);
else
dbms_output.put_line('No Records Updated');
end if;
end;
/
```

### Q2: Display employee names and salaries using a cursor with `WHILE`

```sql
SET SERVEROUTPUT ON;
declare
cursor c2 is select * from emp;
erec emp%rowtype;
begin
open c2;
fetch c2 into erec;
while c2%found loop
dbms_output.put_line(erec.ename||' '||erec.sal);
fetch c2 into erec;
end loop;
close c2;
end;
/
```

### Q7: Employee name and hire date using `FOR` loop

```sql
SET SERVEROUTPUT ON;
declare
cursor c2 is select * from emp;
begin
for erec in c2 loop
dbms_output.put_line(erec.ename||' '||erec.hiredate);
end loop;
end;
/
```

### Q10: Parameterized cursor for department-wise employee names

```sql
SET SERVEROUTPUT ON;
declare
d int;
cursor c1(dno int) is select * from emp where deptno = dno;
begin
d := &dno;
for erec in c1(d) loop
dbms_output.put_line(erec.ename);
end loop;
end;
/
```

---

## Prac 6

### Q1: Create and replace an empty procedure and call it

```sql
SET SERVEROUTPUT ON;
CREATE OR REPLACE PROCEDURE PROC1
AS
BEGIN
NULL;
END;
/

CREATE OR REPLACE PROCEDURE PROC1(MSG IN OUT VARCHAR)
AS
BEGIN
DBMS_OUTPUT.PUT_LINE(MSG);
END;
/

DECLARE
MSG VARCHAR(20) := '&MSG';
BEGIN
PROC1(MSG);
END;
/
```

### Q2: Procedure to display the square of a number

```sql
SET SERVEROUTPUT ON;
CREATE OR REPLACE PROCEDURE SQU(A IN OUT INT)
AS
BEGIN
DBMS_OUTPUT.PUT_LINE(A*A);
END;
/

DECLARE
A INT := 12;
BEGIN
SQU(A);
END;
/
```

### Q3: Procedure to swap two numbers

```sql
SET SERVEROUTPUT ON;
CREATE OR REPLACE PROCEDURE SWAP(A IN OUT INT, B IN OUT INT)
AS
C INT;
BEGIN
C := A;
A := B;
B := C;
DBMS_OUTPUT.PUT_LINE('A IS NOW: '||A);
DBMS_OUTPUT.PUT_LINE('B IS NOW: '||B);
END;
/

DECLARE
X INT := 5;
Y INT := 10;
BEGIN
SWAP(X, Y);
END;
/
```

---

## Prac 7

### Q1: Function to display the square of a number

```sql
CREATE OR REPLACE FUNCTION FUNC1
RETURN INT
AS
A INT := 24;
BEGIN
RETURN A*A;
END;
/

SELECT FUNC1 FROM DUAL;
```

### Q2: Function to swap two numbers

```sql
CREATE OR REPLACE FUNCTION FUNC2
RETURN VARCHAR
AS
A INT := 24;
B INT := 32;
C INT;
BEGIN
C := A;
A := B;
B := C;
RETURN ('A IS NOW: '||A||' '||'AND B IS NOW: '||B);
END;
/

SELECT FUNC2 FROM DUAL;
```

### Q3: Function to display the greatest among two numbers

```sql
CREATE OR REPLACE FUNCTION FUNC3
RETURN VARCHAR
AS
A INT := 12;
B INT := 24;
BEGIN
IF (A > B) THEN
RETURN (A||' IS GREATER THAN '||B);
ELSE
RETURN (B||' IS GREATER THAN '||A);
END IF;
END;
/

SELECT FUNC3 FROM DUAL;
```

---

## Prac 8

### Setup: Create tables and insert data

```sql
SET SERVEROUTPUT ON;
CREATE TABLE PROJECT(PNO INT PRIMARY KEY, PNAME VARCHAR(30), THRS INT);

CREATE TABLE EMPS(ENO INT PRIMARY KEY, NAME VARCHAR(30), HRS INT, SALARY INT, PNO INT REFERENCES PROJECT(PNO));

INSERT INTO PROJECT VALUES(1,'AA',0);
INSERT INTO PROJECT VALUES(2,'BB',0);
INSERT INTO PROJECT VALUES(3,'CC',0);
INSERT INTO PROJECT VALUES(4,'DD',0);
INSERT INTO PROJECT VALUES(5,'EE',0);

INSERT INTO EMPS VALUES(1111,'ABC',4,2000,1);
INSERT INTO EMPS VALUES(2222,'DEF',6,5000,3);
INSERT INTO EMPS VALUES(3333,'GHI',8,7000,3);
INSERT INTO EMPS VALUES(4444,'JKL',2,1000,4);
INSERT INTO EMPS VALUES(5555,'MNO',11,21000,5);

SELECT * FROM EMPS;
SELECT * FROM PROJECT;
```

### Q1: Update total project hours when employee hours are updated

```sql
CREATE OR REPLACE TRIGGER TRG_TIME
AFTER UPDATE
ON EMPS
FOR EACH ROW
BEGIN
UPDATE PROJECT
SET THRS = THRS + :NEW.HRS
WHERE PNO = :OLD.PNO;
END;
/

UPDATE EMPS
SET HRS = HRS - 1;

SELECT * FROM PROJECT;
```

### Q2: Delete employees when their project is deleted

```sql
CREATE OR REPLACE TRIGGER TRG_DEL
AFTER DELETE ON PROJECT
FOR EACH ROW
BEGIN
DELETE FROM EMPS
WHERE PNO = :OLD.PNO;
END;
/

DELETE FROM PROJECT
WHERE PNO = 1;

SELECT * FROM EMPS;
```

### Q3: Insert employee name in uppercase

```sql
CREATE OR REPLACE TRIGGER TRG_UPPER
BEFORE INSERT
ON EMPS
FOR EACH ROW
BEGIN
:NEW.NAME := UPPER(:NEW.NAME);
END;
/

INSERT INTO EMPS VALUES(6600,'MNO',2,6060,5);

SELECT * FROM EMPS;
```

### Q4: Show old salary, new salary, and the difference

```sql
SET SERVEROUTPUT ON;
CREATE OR REPLACE TRIGGER TRG_DIFF
AFTER UPDATE
ON EMPS
FOR EACH ROW
BEGIN
DBMS_OUTPUT.PUT_LINE('OLD SALARY: '||:OLD.SALARY||' NEW SALARY: '||:NEW.SALARY||' DIFFERENCE: '||(:NEW.SALARY - :OLD.SALARY));
END;
/

UPDATE EMPS
SET SALARY = 4000
WHERE NAME = 'DEF';
```

---

## Prac 9

### Q1: Raise an exception when an employee name does not start with 'A'

```sql
SET SERVEROUTPUT ON;
declare
a exception;
cursor c1 is select * from emp;
begin
for erec in c1 loop
dbms_output.put_line(erec.ename);
if not erec.ename like 'A%' then
raise a;
end if;
end loop;
exception
when a then
dbms_output.put_line('Employee name does not start with A.');
end;
/
```

### Q2: Raise an exception when divisor is 0

```sql
SET SERVEROUTPUT ON;
declare
a int := &a;
b int := &b;
ans int;
zd exception;
begin
if b = 0 then
raise zd;
end if;
ans := a/b;
dbms_output.put_line(ans);
exception
when zd then
dbms_output.put_line('b must be >0.');
end;
/
```

---

## Summary

This project covers:

- PL/SQL basics and variable declaration
- Decision-making with `IF` and `CASE`
- Control structures using loops
- `SEQUENCE` and `CURSOR` usage
- `PROCEDURE`, `FUNCTION`, and `TRIGGER` implementation
- Exception handling in Oracle SQL

For Oracle SQL/PLSQL execution, use SQL Developer, SQL*Plus, or any Oracle-compatible environment.
