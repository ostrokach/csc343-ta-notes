drop schema if exists University cascade;
create schema University;
set search_path to University;

create domain Grade as smallint 
	default null
	check (value>=0 and value <=100);
	
create domain CGPA as numeric(10,2)
	default 0
	check (value>=0 and value <=4.0);

create domain Campus as varchar(4)
	not null
	check (value in ('StG', 'UTM', 'UTSC'));
	
create domain Department as varchar(20)
	default null
	check (value in ('ANT', 'EEB', 'CSC', 'ENG', 'ENV', 'HIS'));

create table Student(
	sID integer primary key,
	firstName varchar(15) not null,
	surName varchar(15) not null,
	campus Campus,
	email varchar(25),
	cgpa CGPA);

create table Course(
	cNum integer,			-- E.g., 343
	name varchar(40) not null, 	-- E.g., 'Introduction to Databases'
	dept Department,		-- E.g., 'CSC'
	breadth boolean,	
	primary key (cNum, dept));
	
create table Offering(
	oID integer primary key,
	cNum integer,
	dept Department,
	term integer not null,
	instructor varchar(40),	
	foreign key (cNum, dept) references Course);
	
create table Took(
	sID integer,
	oID integer,
	grade Grade,	
	primary key (sID, oID),	
	foreign key (sID) references Student,
	foreign key (oID) references Offering);
