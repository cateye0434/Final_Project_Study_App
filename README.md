# Final_Project_Study_App
Final Project Information Systems:  versatile learning app, flash card style 


To use this app install SQLserver and run the following queries:

1) create database StudyApp
2) use StudyApp
go

IF OBJECT_ID('[User]') IS NOT NULL
  DROP TABLE [User];
GO


IF OBJECT_ID('Session') IS NOT NULL
  DROP TABLE Session;
GO

IF OBJECT_ID('Subject') IS NOT NULL
  DROP TABLE Subject;
GO

IF OBJECT_ID('Item') IS NOT NULL
  DROP TABLE Item;
GO

IF OBJECT_ID('Item_Session') IS NOT NULL
  DROP TABLE Item_Session;
GO




CREATE TABLE [User] (
[User_ID] INT IDENTITY PRIMARY KEY,
[User_Name] varchar(100) NOT NULL,
Hash varchar(100) NOT NULL,
Salt varchar(100) NOT NULL,
);


CREATE TABLE Session (
Session_ID INT IDENTITY PRIMARY KEY,
Session_Date DATETIME  NOT NULL, 
Session_Points DECIMAL(5,2) NOT NULL,
[User_ID] int,
CONSTRAINT fk_session_user FOREIGN KEY ([User_ID]) REFERENCES [User]([User_ID])
ON DELETE CASCADE,
);

CREATE TABLE Subject (
Subject_ID INT IDENTITY PRIMARY KEY,
Subject_Name varchar(100),
);

Create Table Item (
Item_ID int IDENTITY PRIMARY KEY,
Item_Name varchar(100),
Item_Content varchar(100) NOT NULL,
Subject_ID int,
CONSTRAINT fk_item_subject FOREIGN KEY (Subject_ID) REFERENCES Subject(Subject_ID)
ON DELETE CASCADE,
);


CREATE TABLE ItemSession(
    Item_ID int NOT NULL,
	CONSTRAINT item_subject FOREIGN KEY (Item_ID) REFERENCES Item(Item_ID)
	on delete CASCADE,
    Session_ID int NOT NULL,
    CONSTRAINT item_session FOREIGN KEY (Session_ID) REFERENCES Session(Session_ID)
	on delete CASCADE,
    UNIQUE (Item_ID, Session_ID)
	);

--
Test data insertion via SQL query:

use StudyApp
go

insert into subject(Subject_Name)values('TV Shows');
insert into subject(Subject_Name)values('Programmierung');
insert into subject(Subject_Name)values('BWL');
insert into Subject(Subject_Name)values('Filme');
insert into Subject(Subject_Name)values('Musik');
insert into Subject(Subject_Name)values('Deutsch');
insert into Subject(Subject_Name)values('Englisch');
insert into Subject(Subject_Name)values('Französisch');
insert into Subject(Subject_Name)values('Biologie');


insert into [User]([User_Name],Hash,Salt)values('a','sio5738hYXGDN5E2u7QspCsgLI23Dm0xhJBdu/TakCA=','cYUTWAMkYcM=');
insert into [User]([User_Name],Hash,Salt)values('c','aRnnzYvmnXco+/nNiMJ2OY7xHaMPmq5RSxREoTBtVTw=','ikCssgDUGgw=');
insert into [User]([User_Name],Hash,Salt)values('g','X2XJ7tZUeeiOX0QcLLUOywccwiEwq2tf4aAggubErvc=','e0yG6jNhCK4=');

insert into item(Item_Name, Item_Content, Subject_ID) values('The X-Files', 'TrustNo1', 1);
insert into item(Item_Name, Item_Content, Subject_ID) values('Star Trek', 'Live Long And Prosper', 1);
insert into item(Item_Name, Item_Content, Subject_ID) values('House MD', 'Everybody Lies', 1);
insert into item(Item_Name, Item_Content, Subject_ID) values('Game of Thrones', 'Valar Morghulis', 1);
insert into item(Item_Name, Item_Content, Subject_ID) values('Game of Thrones', 'Not Today', 1);
insert into item(Item_Name, Item_Content, Subject_ID) values('The 100','Jus Drein Jus Daun', 1);
insert into Item(Item_Name, Item_Content, Subject_ID)values('Malapert','frech',7);
insert into Item(Item_Name, Item_Content, Subject_ID)values('Grandiloquent','übertrieben',7);
insert into Item(Item_Name, Item_Content, Subject_ID)values('Flibbertigibbet','Luftikus',7);
insert into Item(Item_Name, Item_Content, Subject_ID)values('Curmudgeon','Griesgram',7);
insert into Item(Item_Name, Item_Content, Subject_ID)values('Sesquipedalian','schwülstig',7);
insert into Item(Item_Name, Item_Content, Subject_ID)values('Blatherskite','Termin',7);

insert into Session(Session_Date,Session_Points,User_ID)values('2021-02-06','20',1);
insert into Session(Session_Date,Session_Points,User_ID)values('2021-02-06','45',1);
insert into Session(Session_Date,Session_Points,User_ID)values('2021-02-06','82',1);
insert into Session(Session_Date,Session_Points,User_ID)values('2021-02-06','17',1);
insert into Session(Session_Date,Session_Points,User_ID)values('2021-02-06','33',1);
insert into Session(Session_Date,Session_Points,User_ID)values('2021-02-06','53',1);

insert into ItemSession(Item_ID,Session_ID)values(1,3);
insert into ItemSession(Item_ID,Session_ID)values(2,3);
insert into ItemSession(Item_ID,Session_ID)values(5,1);
insert into ItemSession(Item_ID,Session_ID)values(3,3);
insert into ItemSession(Item_ID,Session_ID)values(1,2);
insert into ItemSession(Item_ID,Session_ID)values(4,2);

--

<b>UML use case</b>:
<p>
  <img width="806" height="516" alt="UseCaseGen" src="https://github.com/user-attachments/assets/cc5a3d45-a56f-4ce6-8805-385963acee72" />
</p>



<b>Database design</b>:
<p>
  <img width="772" height="486" alt="DBDesign" src="https://github.com/user-attachments/assets/5c9faaef-ea80-4e8b-ae0a-bae78a0075b6" />
</p>



<b>GUI example</b>:
<p>
  <img width="795" height="457" alt="RegistrierungScreen" src="https://github.com/user-attachments/assets/3b2fcece-51c9-4cdb-bb9c-ef3ef42c7ef6" />
  
  <img width="823" height="427" alt="EingabeTextBoxScreen2" src="https://github.com/user-attachments/assets/ff7029f1-8037-4ba5-80ea-1cb65bd2f8e5" />
  
  <img width="749" height="428" alt="AbfrageStart" src="https://github.com/user-attachments/assets/1e5ff401-f2d4-4f40-8b64-d440e46885d5" />

  <img width="754" height="431" alt="AbrageScreen" src="https://github.com/user-attachments/assets/4be8cfa8-53f3-42c7-87dc-a7e8cef1b032" />
  
  <img width="835" height="446" alt="AbfrageLösung" src="https://github.com/user-attachments/assets/a627f2d9-763b-4037-ac5d-3b984ff8dc5e" />

  <img width="835" height="446" alt="ChartScreen" src="https://github.com/user-attachments/assets/15be7da4-0188-44a3-bc3e-14e22e851cab" />

</p>
