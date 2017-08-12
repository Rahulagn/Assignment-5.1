# Assignment-5.1
Exploring Pig Assignment
load at local mode:

//execute below cmd at concole:
pig -x local;

a= load '/home/cloudera/employee_dtl.txt';
dump a;
b= load '/home/cloudera/employee_exp.txt';
dump b;


Ques :1
a1 = foreach a generate $0,$1,$3;
a2 = order a1 by $2,$1 DESC;

a2 = order a1 by $2,$1 ASC;
a3 = limit a2 5;

============================
Ques :2
a1 = foreach a generate $0,$1,$2;
a2 = order a1 by $2 deSC;
a3 = limit a2 3;

================
Ques :3

a= load '/home/cloudera/employee_dtl.txt' using PigStorage (',') as (eid:int,empname:chararray,salary:int, rating:int);
describe a;

b= load '/home/cloudera/employee_exp.txt' using PigStorage (',') as (eid:int,empexp:int);
describe b;

emp = join a by eid, b by eid;
emp1 = emp

foreach_data = FOREACH emp1 GENERATE empname,empexp;

C = FOREACH emp1 GENERATE empname,empexp;
D = GROUP C ALL;
E = FOREACH D GENERATE MAX(C.empexp) as P;
F = FILTER C BY empexp == (int)E.P;
E= order F by empname,empexp;
DUMP E;
===================================>
Ques :4
emp = join a by eid, b by eid;
dump emp;

(101,Amitabh,20000,1,101,100)
(101,Amitabh,20000,1,101,200)
(102,Shahrukh,10000,2,102,400)
(102,Shahrukh,10000,2,102,100)
(104,Anubhav,5000,4,104,300)
(105,Pawan,2500,5,105,100)
(110,Priyanka,2000,5,110,400)
(114,Madhuri,2000,2,114,200)


Ques :5
emp = join a by eid left outer, b by eid;
dump emp;

(101,Amitabh,20000,1,101,100)
(101,Amitabh,20000,1,101,200)
(102,Shahrukh,10000,2,102,400)
(102,Shahrukh,10000,2,102,100)
(103,Akshay,11000,3,,)
(104,Anubhav,5000,4,104,300)
(105,Pawan,2500,5,105,100)
(106,Aamir,25000,1,,)
(107,Salman,17500,2,,)
(108,Ranbir,14000,3,,)
(109,Katrina,1000,4,,)
(110,Priyanka,2000,5,110,400)
(111,Tushar,500,1,,)
(112,Ajay,5000,2,,)
(113,Jubeen,1000,1,,)
(114,Madhuri,2000,2,114,200)
