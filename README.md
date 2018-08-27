CREATE TABLE TransactionType(
TypeID int NOT NULL PRIMARY KEY IDENTITY(1,1),
Name_TT varchar(100) UNIQUE
)
DROP TABLE TransactionType

CREATE TABLE AccountType(
AccountType_ID int NOT NULL PRIMARY KEY IDENTITY(1,1), 
Name_AT varchar(100) UNIQUE
)
DROP TABLE AccountType

CREATE TABLE Users(
User__ID int NOT NULL PRIMARY KEY IDENTITY(1,1),
FirstName varchar(200),
LastName varchar(200),
IIN char (12) UNIQUE,
TelNumer char(11) UNIQUE,
DocNumber varchar(20) UNIQUE
)
DROP TABLE Users

CREATE TABLE Accounts(
Accounts_ID int NOT NULL PRIMARY KEY IDENTITY(1,1),
BIN varchar(30) UNIQUE,
Type_Account int REFERENCES AccountType(AccountType_ID),
isActive varchar(30),
Sum_Account decimal (10,3),
User__ID int NOT NULL REFERENCES Users(User__ID),
)
DROP TABLE Accounts

CREATE TABLE Transactions(
Transactions_ID int PRIMARY KEY IDENTITY(1,1),
Account_ID int NOT NULL REFERENCES Accounts(Accounts_ID),
Sum_Transactions decimal (10,3),
Type_Transactions int NOT NULL REFERENCES TransactionType(TypeID)
)
DROP TABLE Transactions


SELECT * FROM Accounts
SELECT * FROM Users
SELECT * FROM AccountType
SELECT * FROM Transactions
SELECT * FROM TransactionType
INSERT INTO Users(FirstName,LastName,IIN,TelNumer,DocNumber) values('Василий','Васильев',123456789000,77080000000,'9876543210' )
INSERT INTO Users(FirstName,LastName,IIN,TelNumer,DocNumber) values('Алексей','Алексеевич',123456789001,77080000001,'9876543211' )
INSERT INTO Users(FirstName,LastName,IIN,TelNumer,DocNumber) values('Арай','Саин',123456789010,77080000002,'9876543212' )
INSERT INTO Users(FirstName,LastName,IIN,TelNumer,DocNumber) values('Бори','Андреев',123456789100,NULL,'9876543213' )
INSERT INTO AccountType(Name_AT) values('Карточный счет')
INSERT INTO AccountType(Name_AT) values('Кредитный')
INSERT INTO AccountType(Name_AT) values('Депозит')
INSERT INTO Accounts(BIN,Type_Account,isActive,Sum_Account,User__ID) values('KZ00000001',1,0,1000,1 )
INSERT INTO Accounts(BIN,Type_Account,isActive,Sum_Account,User__ID) values('KZ00000002',3,1,1500,2 )
INSERT INTO Accounts(BIN,Type_Account,isActive,Sum_Account,User__ID) values('00000000002',1,1,500,2 )
INSERT INTO Accounts(BIN,Type_Account,isActive,Sum_Account,User__ID) values('00000000001',2,0,0,3 )
INSERT INTO Accounts(BIN,Type_Account,isActive,Sum_Account,User__ID) values('01000000000',3,1,5200,1 )
INSERT INTO Accounts(BIN,Type_Account,isActive,Sum_Account,User__ID) values('02000000001',1,1,200,3)
INSERT INTO Accounts(BIN,Type_Account,isActive,Sum_Account,User__ID) values('02333333333',2,1,3300,2)
INSERT INTO TransactionType(Name_TT) values('Онлайн оплата')
INSERT INTO TransactionType(Name_TT) values('Погашение')
INSERT INTO TransactionType(Name_TT) values('Пополнение')
INSERT INTO Transactions(Account_ID,Sum_Transactions,Type_Transactions) values(2,1000,3)
INSERT INTO Transactions(Account_ID,Sum_Transactions,Type_Transactions) values(1,1000,3)
INSERT INTO Transactions(Account_ID,Sum_Transactions,Type_Transactions) values(1,1500,3)
INSERT INTO Transactions(Account_ID,Sum_Transactions,Type_Transactions) values(4,5000,2)

/* 1. Сделать выборку всех пользователей в алфавитном порядке по фамилии*/
SELECT LastName FROM Users ORDER BY LastName;
/* 2. Сделать выборку всех карт по убыванию текущей суммы*/
SELECT * FROM Accounts ORDER BY Sum_Account DESC;
/* 3. Сделать выборку по фамилии и имени*/
SELECT LastName+' '+FirstName FROM Users;
/* 4. Сделать выборку сумм транзакций*/
SELECT Sum_Transactions FROM Transactions;
/* 5. Сделать выборку сумм транзакций без повторений*/
SELECT DISTINCT Sum_Transactions FROM Transactions;
/* 6. Сделать выборку активных счетов */
SELECT * FROM Accounts WHERE isActive=1;
/* 7.Сделать выборку активных счетов, на которых сумма больше двух тысяч*/
SELECT * FROM Accounts WHERE isActive=1 AND Sum_Account>2000;
/* 8. Сделать выборку счетов, на которых сумма больше 1000, но меньше 5000*/
SELECT * FROM Accounts WHERE Sum_Account BETWEEN 1000 AND 5000;
/* 9. Сделать выборку счетов, на которых сумма меньше 1000 и больше 3000*/
SELECT * FROM Accounts WHERE Sum_Account<1000 OR Sum_Account>3000;
/* 10. Сделать выборку счетов, на которых сумма не больше 500 и не меньше 4000*/
SELECT * FROM Accounts WHERE Sum_Account!<4000;
/* 11. Вывести имя и фамилию пользователя, как колонку ‘FullName’*/
SELECT LastName+' '+FirstName AS FullName FROM Users;
/* 12. Вывести все номера, отличающиеся последним символом*/
SELECT TelNumer FROM Users WHERE TelNumer LIKE '7708000000_';
/* 13.Вывести все карточные и депозитные счета*/
SELECT * FROM Accounts WHERE Type_Account!=2;
SELECT * FROM Accounts WHERE Type_Account IN (1,3);
/* 14. Вывести пользователей, у которых неизвестен номер*/
SELECT * FROM Users WHERE TelNumer IS NULL;
/* 15. Вывести пользователей, в чьих фамилиях есть сочетание букв «ев»*/
SELECT * FROM Users WHERE LastName LIKE '%ев%';
/* 16. Поменяйте статус активности счета неактивным счетам*/
UPDATE Accounts SET isActive = 1 WHERE isActive!=1 ; 
